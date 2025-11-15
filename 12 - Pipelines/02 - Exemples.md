

# Exemplos práticos: CI / CD com Terraform e criação de um S3 Bucket via GitHub Actions

## Estrutura do repositório (sugerida)

```
.
├── .github/
│   └── workflows/
│       └── terraform-s3.yml
├── .gitignore
├── terraform/
│   ├── provider.tf
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
└── Jenkinsfile
```

---

## Arquivos Terraform (terraform/)

### provider.tf

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = var.aws_region
}
```

### variables.tf

```hcl
variable "aws_region" {
  description = "Região AWS"
  type        = string
  default     = "us-east-1"
}

variable "bucket_name" {
  description = "Nome do bucket S3 (deve ser globalmente único)"
  type        = string
  default     = "exemplo-bucket-ci-cd-terraform-12345"
}
```

### main.tf

```hcl
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name

  versioning {
    enabled = true
  }

  tags = {
    Name        = var.bucket_name
    Environment = "ci-cd-demo"
    ManagedBy   = "Terraform"
  }
}

# Optional: enable server-side encryption by default
resource "aws_s3_bucket_server_side_encryption_configuration" "this" {
  bucket = aws_s3_bucket.this.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}
```

### outputs.tf

```hcl
output "bucket_id" {
  description = "ID do bucket criado"
  value       = aws_s3_bucket.this.id
}
```

### .gitignore (sugerido)

```
.terraform/
*.tfstate
*.tfstate.backup
.terraform.lock.hcl
```

---

## GitHub Actions — Workflow exemplo (`.github/workflows/terraform-s3.yml`)

Este workflow executa `terraform init`, `plan` e `apply` em push na branch `main`. Assume que você configurou os *secrets* `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` e `AWS_REGION` no repositório.

```yaml
name: Terraform CI - Create S3 Bucket

on:
  push:
    branches:
      - main

jobs:
  terraform:
    name: Terraform Apply
    runs-on: ubuntu-latest
    env:
      TF_INPUT: "false"
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: 1.5.0

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Terraform Init
        working-directory: terraform
        run: terraform init -input=false

      - name: Terraform Format Check
        working-directory: terraform
        run: terraform fmt -check

      - name: Terraform Plan
        working-directory: terraform
        run: terraform plan -out=tfplan -input=false

      - name: Terraform Apply
        if: github.ref == 'refs/heads/main'
        working-directory: terraform
        run: terraform apply -input=false -auto-approve tfplan
```

**Observações:**

* Em pipelines reais, normalmente separa-se `plan` e `apply` em jobs diferentes e exige-se revisão/ aprovação manual antes de `apply`.
* Não use `-auto-approve` em ambientes críticos sem um gate/approval.
* Use roles temporárias (OIDC) quando possível para evitar armazenar chaves.

---

## GitLab CI — `.gitlab-ci.yml` (equivalente)

```yaml
stages:
  - validate
  - plan
  - apply

variables:
  TF_INPUT: "false"

terraform:validate:
  image: hashicorp/terraform:1.5.0
  stage: validate
  script:
    - cd terraform
    - terraform init -input=false
    - terraform fmt -check
    - terraform validate

terraform:plan:
  image: hashicorp/terraform:1.5.0
  stage: plan
  script:
    - cd terraform
    - terraform init -input=false
    - terraform plan -out=tfplan -input=false
  artifacts:
    paths:
      - terraform/tfplan
    expire_in: 1 hour

terraform:apply:
  image: hashicorp/terraform:1.5.0
  stage: apply
  script:
    - cd terraform
    - terraform init -input=false
    - terraform apply -input=false -auto-approve tfplan
  when: manual
  only:
    - main
```

**Observação:** no GitLab use variáveis de CI/CD (Settings → CI/CD → Variables) para `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION` e configure o job para exportá-las (ou configure via image com AWS CLI). Aqui se assume que runners têm acesso às variáveis.

---

## Jenkins — `Jenkinsfile` (Declarative pipeline)

Exemplo que usa `withCredentials` para recuperar duas credenciais do Jenkins (IDs: `aws_access_key_id` e `aws_secret_access_key`) e executa terraform dentro de um agente Linux.

```groovy
pipeline {
  agent any

  environment {
    TF_DIR = "terraform"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Init & Validate') {
      steps {
        withCredentials([
          string(credentialsId: 'aws_access_key_id', variable: 'AWS_ACCESS_KEY_ID'),
          string(credentialsId: 'aws_secret_access_key', variable: 'AWS_SECRET_ACCESS_KEY')
        ]) {
          sh '''
            cd ${TF_DIR}
            terraform init -input=false
            terraform fmt -check || true
            terraform validate || true
          '''
        }
      }
    }

    stage('Plan') {
      steps {
        withCredentials([
          string(credentialsId: 'aws_access_key_id', variable: 'AWS_ACCESS_KEY_ID'),
          string(credentialsId: 'aws_secret_access_key', variable: 'AWS_SECRET_ACCESS_KEY')
        ]) {
          sh '''
            cd ${TF_DIR}
            terraform plan -out=tfplan -input=false
          '''
        }
      }
    }

    stage('Apply') {
      when {
        branch 'main'
      }
      steps {
        input message: "Aprovar terraform apply na branch main?"
        withCredentials([
          string(credentialsId: 'aws_access_key_id', variable: 'AWS_ACCESS_KEY_ID'),
          string(credentialsId: 'aws_secret_access_key', variable: 'AWS_SECRET_ACCESS_KEY')
        ]) {
          sh '''
            cd ${TF_DIR}
            terraform apply -input=false -auto-approve tfplan
          '''
        }
      }
    }
  }

  post {
    always {
      echo "Pipeline finalizado"
    }
  }
}
```

**Observações Jenkins**

* Configure as credenciais no Jenkins (Credentials → System → Global credentials).
* `input` força aprovação manual antes do `apply`. Em produção, mantenha esse gate.

---

## Diagrama de fluxo (Mermaid)

Copie/cole este bloco em um renderer que suporte Mermaid (ex.: VSCode + extensão, GitLab, GitHub com preview mermaid):

```mermaid
flowchart TD
  A[Developer push para main] --> B[GitHub Actions: checkout]
  B --> C[Setup Terraform & AWS Credentials]
  C --> D[terraform init]
  D --> E[terraform plan]
  E --> F{Branch == main?}
  F -- yes --> G[terraform apply (auto-approve)]
  F -- no  --> H[Only plan (no apply)]
  G --> I[Bucket criado no AWS S3]
  I --> J[Notifier / Observability]
```

---

## Comparação rápida entre ferramentas (prós/cons)

| Ferramenta     |                       Tipo | Prós                                                                        | Contras                                                                       |
| -------------- | -------------------------: | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| GitHub Actions | SaaS / integrado ao GitHub | Integração nativa com repositório, marketplace de actions, fácil de começar | Custo se intensivo, limites de minutos para planos grátis                     |
| GitLab CI      |        Integrado ao GitLab | Pipelines poderosos, runners customizáveis, CI/CD integrado a issues        | Menos marketplace que GitHub Actions, runners self-hosted requer configuração |
| Jenkins        |                Self-hosted | Extremamente extensível, milhares de plugins, controle total                | Manutenção pesada, upgrade/segurança e configuração complexa                  |
| Argo CD / Flux |            GitOps para k8s | Excelente para Deploy declarativo em Kubernetes                             | Focado em k8s — não é um substituto direto para CI tradicional                |

---

## Boas práticas e recomendações de segurança

* **Não** comite chaves no repositório. Use secrets (GitHub Secrets / GitLab CI Variables / Jenkins Credentials).
* Prefira **roles iam com OIDC** (GitHub Actions → AWS OIDC) em vez de chaves estáticas quando possível.
* Use **least privilege**: política IAM para o user/role que só permita `s3:CreateBucket`, `s3:PutEncryptionConfiguration` etc. (evite políticas `*`).
* Separe `plan` e `apply` e exija aprovações para produção.
* Armazene o estado de Terraform de forma segura (ex.: S3 + DynamoDB lock) em equipes maiores.
* Use `terraform fmt` e `terraform validate` como jobs de qualidade.
* Habilite logging/monitoring e alertas (CloudTrail + AWS Config + GuardDuty, além de observabilidade do pipeline).
* Automatize rollback/feature flags para mitigar falhas de deploy.

---

## Exemplo de IAM mínimo (exemplo de política para a conta CI — JSON)

Exemplo ilustrativo de política IAM (apenas para criar bucket e configurar criptografia/versão). Ajuste conforme necessário e teste cuidadosamente.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3BucketOperationsForCI",
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:PutBucketVersioning",
        "s3:PutEncryptionConfiguration",
        "s3:PutBucketTagging",
        "s3:PutBucketAcl",
        "s3:ListAllMyBuckets",
        "s3:ListBucket",
        "s3:GetBucketLocation",
        "s3:DeleteBucket" 
      ],
      "Resource": "*"
    }
  ]
}
```

> Em produção limite o `Resource` ao arn do bucket esperado sempre que possível.

---

## Testando localmente antes de rodar no CI

1. Instale Terraform localmente.
2. Exporte variáveis AWS:

```bash
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...
export AWS_REGION=us-east-1
```

3. No diretório `terraform/`:

```bash
terraform init
terraform plan -out=plan.tf
terraform apply -auto-approve plan.tf
```

---

## Checklist rápido antes de ativar o pipeline no repositório

* [ ] Configurar GitHub Secrets (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`) ou OIDC.
* [ ] Testar `terraform plan` localmente.
* [ ] Garantir nome do bucket globalmente único ou parametrizar.
* [ ] Definir política IAM com privilégios mínimos.
* [ ] Configurar backend remoto para estado se necessário (S3 + DynamoDB lock).
* [ ] Habilitar logs e monitoramento.

---
> IMPORTANTE: **não** comite chaves/segredos no repositório. Use secrets do GitHub/GitLab/Jenkins com privilégios mínimos. Os exemplos abaixo usam `terraform apply -auto-approve` para fins didáticos — em produção prefira aprovações manuais ou gates.

---