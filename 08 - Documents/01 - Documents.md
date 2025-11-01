

# Processos de Documentação

A documentação é um pilar essencial para a governança técnica e a continuidade de projetos de software. Ela conecta o planejamento estratégico, o desenvolvimento e a operação, fornecendo uma base de conhecimento que garante previsibilidade, rastreabilidade e qualidade.

Os principais tipos de documentação encontrados em ambientes corporativos e técnicos são: **documentação de projeto**, **documentação de código** e **documentação de configuração de esteiras de automação**. Cada uma possui objetivos e formatos próprios, e seu bom uso é um indicador de maturidade organizacional.

---

## 1. Documentação de Projeto

A documentação de projeto segue modelos consolidados pela engenharia de gestão, como os propostos no **PMBOK (Project Management Body of Knowledge)**, que organiza o ciclo de vida de um projeto em grupos de processos (iniciação, planejamento, execução, monitoramento e encerramento).

Entre os principais artefatos estão o **Termo de Abertura do Projeto**, o **Plano de Gerenciamento**, o **Registro de Riscos** e o **Cronograma**. O cronograma é especialmente relevante por representar o tempo de execução e a relação de dependência entre as atividades.

### Exemplo textual de cronograma

```
Cronograma do Projeto: Sistema de Pagamentos Online
Versão: 2.1 | Data: 25/10/2025

Fase 1 – Levantamento de Requisitos
  Início: 01/11/2025 | Fim: 10/11/2025 | Responsável: Ana Souza

Fase 2 – Desenvolvimento Backend
  Início: 11/11/2025 | Fim: 05/12/2025 | Responsável: Equipe Engenharia

Fase 3 – Testes Integrados
  Início: 06/12/2025 | Fim: 15/12/2025 | Responsável: João Ferreira

Fase 4 – Implantação e Treinamento
  Início: 16/12/2025 | Fim: 20/12/2025 | Responsável: Equipe DevOps
```

### Representação visual de cronograma (modelo Gantt)

O mesmo conteúdo, quando representado graficamente em uma ferramenta como o **Microsoft Project** ou **Primavera P6**, ficaria assim:

```
| Data →         01/11     10/11     20/11     01/12     10/12     20/12
----------------------------------------------------------------------------
Levantamento de Requisitos [##########]
Desenvolvimento Backend                [######################]
Testes Integrados                                            [########]
Implantação e Treinamento                                              [###]
```

Esse diagrama de Gantt é uma forma de documentação visual utilizada pelo PMBOK para apoiar a comunicação entre partes interessadas. Ele deixa claro o encadeamento das fases e permite identificar gargalos e atrasos de forma imediata.
O artefato costuma ser acompanhado de versões controladas, indicando revisões e ajustes realizados ao longo da execução do projeto.

---

## 2. Documentação de Código

A documentação de código é o registro técnico do funcionamento interno do sistema. Seu objetivo é explicar **como o software executa suas funções** e **como suas partes se relacionam**, facilitando a manutenção, a colaboração e a auditoria de qualidade.

No ecossistema Java, a ferramenta **Javadoc** é o principal recurso para geração automatizada de documentação. A partir de comentários padronizados dentro do código-fonte, o Javadoc gera automaticamente páginas HTML navegáveis que descrevem classes, métodos, parâmetros e exceções.

### Exemplo de código documentado

```java
/**
 * Classe responsável por operações de cálculo de desconto em vendas.
 */
public class CalculadoraDeVendas {

    /**
     * Calcula o valor total de uma venda aplicando um desconto percentual.
     *
     * @param valorBase valor inicial da venda
     * @param percentualDesconto percentual de desconto aplicado
     * @return valor final da venda após desconto
     */
    public double calcularVenda(double valorBase, double percentualDesconto) {
        return valorBase - (valorBase * percentualDesconto / 100);
    }
}
```

### Simulação da página HTML gerada pelo Javadoc

Após rodar o comando:

```bash
javadoc -d ./docs -sourcepath ./src com.exemplo.vendas
```

O Javadoc gera uma estrutura como a seguinte:

```
docs/
 ├── index.html
 ├── allclasses-index.html
 └── com/
     └── exemplo/
         └── vendas/
             ├── CalculadoraDeVendas.html
             └── package-summary.html
```

O arquivo `CalculadoraDeVendas.html` conterá uma página semelhante a esta:

---

**Javadoc Output – CalculadoraDeVendas**

> **Package:** com.exemplo.vendas
> **Class:** CalculadoraDeVendas
> **Descrição:** Classe responsável por operações de cálculo de desconto em vendas.

| Método                                                       | Descrição                                          | Retorno  |
| ------------------------------------------------------------ | -------------------------------------------------- | -------- |
| `calcularVenda(double valorBase, double percentualDesconto)` | Calcula o valor total da venda aplicando desconto. | `double` |

---

Essa documentação é navegável por meio de links entre classes, permitindo que o desenvolvedor explore a estrutura completa do projeto de forma interativa.
Além disso, por ser gerada automaticamente a partir do código, ela reduz a defasagem entre o comportamento real do sistema e o material técnico disponível.

### JUnit como documentação executável

Os testes unitários também funcionam como documentação viva do comportamento do código.
Um exemplo em **JUnit 5**:

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

/**
 * Testes para a classe CalculadoraDeVendas.
 */
public class CalculadoraDeVendasTest {

    @Test
    public void deveCalcularVendaComDescontoCorretamente() {
        CalculadoraDeVendas calc = new CalculadoraDeVendas();
        double resultado = calc.calcularVenda(100.0, 10.0);
        assertEquals(90.0, resultado, 0.01);
    }
}
```

Ao executar os testes com `mvn test` ou `gradle test`, é possível gerar relatórios HTML de cobertura (com ferramentas como JaCoCo), que documentam **quais partes do código foram testadas** e **com que frequência**. Essa combinação de Javadoc e testes transforma o código em um sistema autodescritivo e verificável.

---

## 3. Documentação de Configuração de Esteiras de Automação

A terceira dimensão da documentação técnica trata da **automação de processos de entrega e infraestrutura**, um campo consolidado pelo movimento DevOps.
Ferramentas como **Terraform**, **GitHub Actions**, **Jenkins** e **GitLab CI** tornaram-se parte do ciclo de documentação operacional, pois os próprios arquivos de automação são lidos como artefatos de configuração.

### Exemplo de documentação com Terraform

```hcl
# Cria uma instância EC2 para o ambiente de staging
# AMI e tipo de instância definidos por variáveis externas
resource "aws_instance" "staging_server" {
  ami           = var.ami_id
  instance_type = var.instance_type
  tags = {
    Name        = "staging-app"
    Environment = "staging"
  }
}
```

### Exemplo de documentação de pipeline CI/CD (arquivo PIPELINE.md)

```
Pipeline CI/CD – Aplicação API Pagamentos

1. build: compila o código Java e executa testes JUnit
2. test: executa testes integrados com banco MySQL em container
3. deploy-staging: cria infraestrutura via Terraform e publica build
4. deploy-prod: implanta versão aprovada no ambiente de produção

Variáveis obrigatórias:
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- DATABASE_URL
```

Essa documentação garante a rastreabilidade do fluxo de entrega, permitindo que qualquer integrante da equipe saiba como o código é compilado, testado e implantado. Além disso, reduz a dependência de conhecimento tácito, um dos principais riscos operacionais em times de software.

---

## Conclusão

A documentação é um processo transversal que conecta o planejamento, o desenvolvimento e a operação.

* O **PMBOK** orienta a documentação de projeto, com ênfase em cronogramas, planos e relatórios.
* O **Javadoc** e o **JUnit** representam a documentação de código, descrevendo o comportamento técnico e validando seu funcionamento.
* O **Terraform** e os **pipelines de automação** constituem a documentação operacional, garantindo previsibilidade e auditabilidade das entregas.

Quando essas três dimensões se integram, a organização atinge um estado de maturidade documental que favorece a colaboração, a escalabilidade e a governança técnica.
Em um cenário de engenharia moderna, a documentação não é apenas registro, mas uma extensão viva do próprio sistema.

---

**Referências**

* PMI. *A Guide to the Project Management Body of Knowledge (PMBOK® Guide)* – 7ª Edição. Project Management Institute, 2021.
* Oracle. *Javadoc Tool Documentation*. Disponível em: [https://docs.oracle.com/javase/](https://docs.oracle.com/javase/).
* JUnit 5 User Guide. *Testing Framework for Java*. Disponível em: [https://junit.org/junit5/](https://junit.org/junit5/).
* HashiCorp. *Terraform Documentation*. Disponível em: [https://developer.hashicorp.com/terraform/docs](https://developer.hashicorp.com/terraform/docs).

