

#  I. PADRÕES DE CÓDIGO

---

## 1. Definição e Objetivo

### 1.1 O que são Padrões de Código

“Padrões de código” (ou *coding standards*) são **regras e diretrizes formais** que especificam **como o código deve ser escrito, estruturado e organizado** em um projeto ou linguagem.

Eles tratam de aspectos técnicos como:

* Estrutura de funções, classes e módulos.
* Organização de arquivos e pacotes.
* Convenções de nomenclatura e tipos.
* Práticas de tratamento de erros e exceções.
* Testabilidade e modularidade.

> **Referência:** GeeksforGeeks – *Coding Standards and Guidelines*
> ([geeksforgeeks.org/coding-standards-and-guidelines](https://www.geeksforgeeks.org/coding-standards-and-guidelines))

---

## 2. Motivação

1. **Manutenibilidade:** Código consistente facilita a leitura e manutenção por toda a equipe.
2. **Confiabilidade:** Reduz erros e comportamentos inesperados.
3. **Escalabilidade:** Permite crescimento ordenado do código e integração entre módulos.
4. **Integração Contínua:** Linters e testes automáticos dependem de padronização.
5. **Treinamento:** Novos desenvolvedores aprendem o estilo da base mais rapidamente.

---

## 3. Elementos de um Padrão de Código

| Categoria               | Descrição                                                                       |
| ----------------------- | ------------------------------------------------------------------------------- |
| **Nomenclatura**        | Regras para variáveis, funções, classes e constantes.                           |
| **Estrutura**           | Tamanho máximo de funções, organização em módulos, dependências.                |
| **Tratamento de Erros** | Convenções para exceções, retornos e logs.                                      |
| **Documentação**        | Comentários, docstrings e metadados do código.                                  |
| **Controle de Versão**  | Política de commits e mensagens padrão.                                         |
| **Boas Práticas**       | Evitar duplicação, manter SRP (*Single Responsibility Principle*), modularizar. |

---

## 4. Padrões de Projeto (Design Patterns)

### 4.1 Definição

Os *Design Patterns* são **soluções recorrentes** para problemas comuns de design de software. São descritos formalmente, nomeados e categorizados (criacionais, estruturais e comportamentais).

### 4.2 Tipos Clássicos (GoF)

| Tipo                | Exemplos                    | Propósito                                     |
| ------------------- | --------------------------- | --------------------------------------------- |
| **Criacionais**     | Singleton, Factory, Builder | Controle de criação de objetos                |
| **Estruturais**     | Adapter, Decorator, Proxy   | Organização e composição de classes/objetos   |
| **Comportamentais** | Observer, Strategy, Command | Comunicação entre objetos e controle de fluxo |

> **Referência:** Gamma, Helm, Johnson, Vlissides – *Design Patterns: Elements of Reusable Object-Oriented Software* (1994)

---

## 5. Princípios Fundamentais (SOLID)

| Princípio                     | Descrição                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------- |
| **S** – Single Responsibility | Uma classe deve ter uma única responsabilidade.                                 |
| **O** – Open/Closed           | Aberta para extensão, fechada para modificação.                                 |
| **L** – Liskov Substitution   | Subtipos devem poder substituir seus tipos-base.                                |
| **I** – Interface Segregation | Interfaces específicas e pequenas são preferíveis.                              |
| **D** – Dependency Inversion  | Módulos de alto nível não devem depender de módulos de baixo nível diretamente. |

---

## 6. Governança e Implementação

* Criar um documento de *Coding Standards* central (ex: `CODING_GUIDELINES.md`).
* Aplicar revisões de código com checklist de conformidade.
* Automatizar verificações com ferramentas (linters, testes estáticos).
* Atualizar o padrão conforme novas práticas e linguagens evoluem.

---

# 📚 III. BIBLIOGRAFIA BÁSICA E COMPLEMENTAR

### **Livros Fundamentais**

1. **Steve McConnell – *Code Complete* (2ª ed., 2004)**
   Referência clássica sobre boas práticas de desenvolvimento e legibilidade.
2. **Robert C. Martin – *Clean Code* (2008)**
   Guia sobre clareza, simplicidade e ética de código limpo.
3. **Erich Gamma et al. – *Design Patterns* (1994)**
   Obra fundacional dos padrões de projeto orientados a objeto.
4. **Martin Fowler – *Refactoring: Improving the Design of Existing Code* (2ª ed., 2018)**
   Sobre como aplicar padrões e melhorar código legado sem alterar comportamento.

---

### **Guias e Documentos de Estilo**

* **PEP 8 – Python Enhancement Proposal 8:** [https://peps.python.org/pep-0008/](https://peps.python.org/pep-0008/)
* **Google Style Guides:** [https://google.github.io/styleguide/](https://google.github.io/styleguide/)
* **Airbnb JavaScript Style Guide:** [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)
* **Oracle Java Code Conventions:** [https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html](https://www.oracle.com/java/technologies/javase/codeconventions-introduction.html)

---

### **Artigos e Estudos Acadêmicos**

* Allamanis, M. et al. (2014). *Learning Natural Coding Conventions.* Proceedings of FSE 2014.
* Johnson, R. (1992). *Documenting Frameworks Using Patterns.*
* GeeksforGeeks. *Coding Standards and Guidelines.*
* Aper­tis Project. *Coding Conventions and Policies.*

---

## 🧭 Conclusão

| Tema                  | Foco Principal                                           | Benefício                                       |
| --------------------- | -------------------------------------------------------- | ----------------------------------------------- |
| **Padrões de Código** | Estrutura, modularização, boas práticas, design patterns | Confiabilidade, manutenção e arquitetura sólida |
| **Style Guides**      | Aparência, formatação e legibilidade visual              | Consistência, colaboração e clareza             |

Um projeto maduro **integra ambos**:

> O padrão de código garante *como o sistema é construído*;
> O style guide garante *como o código é lido e entendido*.
