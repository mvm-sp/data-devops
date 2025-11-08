
# Principais Práticas e Processos de Versionamento de Código

---

##  1. O que é Versionamento de Código

O **versionamento de código** é o processo de gerenciar as mudanças feitas em um projeto de software ao longo do tempo.
Ele permite **rastrear, comparar, restaurar e colaborar** de forma organizada no código-fonte.

A principal ferramenta para isso hoje é o **Git**, utilizada em plataformas como **GitHub**, **GitLab**, **Bitbucket**, **AWS CodeCommit**, entre outras.

---

##  2. Conceitos Fundamentais do Git

| Conceito   | Descrição                                                    | Exemplo                                      |
| ---------- | ------------------------------------------------------------ | -------------------------------------------- |
| **Commit** | Registro de uma mudança no repositório.                      | `git commit -m "Adiciona endpoint de login"` |
| **Branch** | Ramificação do código para desenvolvimento paralelo.         | `git checkout -b feature/login`              |
| **Merge**  | Junção de mudanças entre branches.                           | `git merge feature/login`                    |
| **Rebase** | Reorganização do histórico de commits.                       | `git rebase main`                            |
| **Tag**    | Marca um ponto específico da história (geralmente releases). | `git tag v1.0.0`                             |
| **Remote** | Repositório hospedado (ex: GitHub).                          | `git push origin main`                       |

---

##  3. Principais Fluxos (Workflows) de Versionamento

### 3.1. **Git Flow**

🔹 Estrutura tradicional e robusta para projetos grandes.

**Branches principais:**

* `main` → versão estável do código.
* `develop` → integração de novas features.

**Branches de suporte:**

* `feature/*` → novas funcionalidades.
* `release/*` → preparação de versões.
* `hotfix/*` → correções urgentes na produção.

**Exemplo de fluxo:**

```
main
 ├─ develop
 │   ├─ feature/login
 │   ├─ feature/cadastro
 │   └─ release/1.0.0
 └─ hotfix/1.0.1
```

Ideal para: times grandes, pipelines com release formal e múltiplos ambientes.

---

### 3.2. **GitHub Flow**

🔹 Fluxo simplificado, ideal para entregas contínuas.

**Processo:**

1. Criar branch a partir da `main`.
2. Implementar e testar a feature.
3. Abrir um **Pull Request (PR)**.
4. Revisão e merge na `main`.
5. Deploy automático.

Ideal para: equipes pequenas, projetos com integração e entrega contínua (CI/CD).

---

### 3.3. **GitLab Flow**

🔹 Combina o Git Flow com práticas de CI/CD modernas.

**Conceito-chave:** Integração entre branches e ambientes (dev, staging, prod).

**Exemplo:**

```
main → produção  
staging → homologação  
dev → desenvolvimento  
```

Ideal para: times DevOps e infraestruturas automatizadas.

---

## 4. Boas Práticas de Versionamento

| Prática                             | Descrição                                              | Exemplo                                                         |
| ----------------------------------- | ------------------------------------------------------ | --------------------------------------------------------------- |
| **Commits semânticos**              | Mensagens claras e padronizadas.                       | `feat(login): adiciona validação JWT`                           |
| **Atomicidade dos commits**         | Cada commit deve representar uma mudança lógica única. | ✅ “Implementa botão de logout”<br>❌ “Várias correções diversas” |
| **Revisão via Pull Request**        | Toda mudança deve ser revisada antes do merge.         | GitHub/GitLab PRs                                               |
| **Tags semânticas (SemVer)**        | `MAJOR.MINOR.PATCH` → `v2.3.1`                         | `v1.0.0`, `v1.1.0`, `v1.1.1`                                    |
| **Proteção de branches principais** | Bloquear commits diretos na `main`.                    | Configuração em GitHub/GitLab                                   |
| **Integração Contínua (CI)**        | Testes automáticos a cada commit.                      | GitHub Actions, Jenkins, GitLab CI                              |

---

## 5. Processos de Versionamento em Times

### **A. Desenvolvimento Colaborativo**

* Cada dev trabalha em uma **branch isolada**.
* Criação de **Pull Requests** para integrar na branch principal.
* Revisões de código garantem **qualidade e segurança**.

### **B. Controle de Releases**

* Utilizar **tags** para marcar versões.
* Automatizar **deploys** a partir de merges ou tags.
* Exemplo:

  * `main` → Produção
  * `staging` → Ambiente de testes
  * `develop` → Desenvolvimento contínuo

### **C. Gestão de Conflitos**

* Usar `git fetch` e `git rebase` quando necessário.
* Evitar commits grandes e pouco descritivos.
* Resolver conflitos antes do merge.

---

## 6. Integração com CI/CD

Versionamento está diretamente ligado a **pipelines automatizados**.
Cada commit ou PR pode acionar uma pipeline para:

1. **Executar testes unitários e integrados**
2. **Analisar qualidade de código** (ex: SonarQube)
3. **Validar segurança** (ex: Dependabot, Snyk)
4. **Gerar build e deploy automatizado**

**Exemplo (GitHub Actions):**

```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Instala dependências
        run: npm install
      - name: Executa testes
        run: npm test
```

---

## 7. Padronização e Convenções

### **A. Padrão de Branches**

```
feature/*      → novas funcionalidades
fix/*          → correções de bugs
chore/*        → tarefas de manutenção
hotfix/*       → correções emergenciais
release/*      → versões estáveis
```

### **B. Padrão de Commits (Conventional Commits)**

```
<tipo>(escopo): descrição breve

Tipos comuns:
feat     → nova funcionalidade
fix      → correção de bug
chore    → manutenção
docs     → documentação
test     → testes
refactor → melhoria interna
```

Exemplo:

```
feat(api): adiciona endpoint para autenticação
fix(ui): corrige erro no botão de login
```

---

## 8. Ferramentas de Apoio

| Categoria               | Ferramenta                         | Função                          |
| ----------------------- | ---------------------------------- | ------------------------------- |
| **Repositório remoto**  | GitHub, GitLab, Bitbucket          | Hospedagem e colaboração        |
| **Controle de versão**  | Git                                | Controle local e remoto         |
| **Qualidade de código** | SonarQube, CodeClimate             | Análise automática              |
| **Automação CI/CD**     | GitHub Actions, GitLab CI, Jenkins | Builds e deploys automatizados  |
| **Segurança**           | Dependabot, Snyk                   | Verificação de vulnerabilidades |

---

## 9. Pra lembrar

Um bom processo de versionamento:

* **Centraliza e organiza o histórico** de mudanças;
* **Facilita o trabalho colaborativo** em equipes grandes ou distribuídas;
* **Previne erros** e facilita **rollbacks**;
* **Integra-se naturalmente a pipelines CI/CD**, garantindo qualidade e estabilidade contínuas.

---

##  Estudo Complementar

1. **Prática:** Criar um repositório no GitHub e aplicar o Git Flow.
2. **Exercício:** Criar commits semânticos e abrir PRs de revisão.
3. **Automação:** Configurar uma pipeline CI simples (ex: GitHub Actions).
4. **Avançado:** Adicionar validação automática de mensagens de commit e lint de código.
