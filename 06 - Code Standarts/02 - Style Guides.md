
#  II. STYLE GUIDES DE PROGRAMAÇÃO

---

## 1. Definição e Propósito

Um **Style Guide** (Guia de Estilo) define **a aparência, formatação e legibilidade do código**.
Enquanto o *coding standard* dita **como o código funciona**, o *style guide* dita **como ele é escrito visualmente**.

Foco principal:

* **Consistência visual e semântica.**
* **Clareza para o leitor.**
* **Facilidade de manutenção.**

> **Exemplo:** PEP 8 (Python), Google Style Guides (para várias linguagens).

---

## 2. Estrutura de um Style Guide

| Categoria                   | Exemplos de Regras                                                        |
| --------------------------- | ------------------------------------------------------------------------- |
| **Indentação**              | 4 espaços por nível; nunca misturar tabs e espaços.                       |
| **Quebras de Linha**        | Máximo de 79–100 caracteres por linha.                                    |
| **Espaçamento**             | Espaço após vírgulas, mas não antes de parênteses.                        |
| **Nomenclatura Estética**   | `camelCase` (variáveis), `PascalCase` (classes), `ALL_CAPS` (constantes). |
| **Comentário e Docstrings** | Padrão uniforme para documentação.                                        |
| **Importações**             | Ordem: bibliotecas padrão → terceiros → internas.                         |
| **Estilo de Chaves**        | Posição (mesma linha ou nova linha) padronizada.                          |

> **Referência:** Python PEP 8, Java Code Conventions, Google JavaScript Style Guide.

---

## 3. Ferramentas de Apoio

| Linguagem                 | Ferramentas                                           |
| ------------------------- | ----------------------------------------------------- |
| **Python**                | `flake8`, `black`, `pylint`                           |
| **JavaScript/TypeScript** | `eslint`, `prettier`, `standardjs`                    |
| **Java**                  | `checkstyle`, `spotbugs`                              |
| **C/C++**                 | `clang-format`, `cppcheck`                            |
| **Multi-linguagem**       | `.editorconfig` (padroniza formatação entre editores) |

Essas ferramentas automatizam a conformidade e evitam debates subjetivos sobre estilo.

---

## 4. Criação de um Style Guide Interno

1. **Escolher base existente:** adaptar PEP 8, Google Style, Airbnb Style Guide etc.
2. **Definir escopo:** formatação, nomenclatura, documentação, estrutura de arquivos.
3. **Registrar no repositório:** arquivo `STYLE_GUIDE.md` visível e acessível.
4. **Automatizar:** configurar linters e formatadores automáticos no CI/CD.
5. **Educar:** incluir o guia no onboarding e nas revisões de código.

---

## 5. Revisão e Evolução

* Atualizar periodicamente conforme novas versões da linguagem surgem.
* Coletar feedback da equipe (evitar guias rígidos demais).
* Manter exemplos de “bom” e “mau” código.
* Registrar exceções e justificativas.

---

## 6. Cultura e Liderança

Um style guide eficaz depende de **cultura**:

* Encarar o estilo como ferramenta de comunicação, não de imposição.
* Líderes técnicos devem aplicar e seguir as regras.
* Valorização da legibilidade sobre preferências pessoais.
* Incentivo à refatoração e clareza contínua.

---



### **Guias e Documentos de Estilo**

* **PEP 8 – Python Enhancement Proposal 8:** [https://peps.python.org/pep-0008/](https://peps.python.org/pep-0008/)
* **Google Style Guides:** [https://google.github.io/styleguide/](https://google.github.io/styleguide/)
* **Airbnb JavaScript Style Guide:** [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)
* **Oracle Java Code Conventions:** [https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html](https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html)

---
