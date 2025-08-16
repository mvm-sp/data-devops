### O que é o CALMS?

**CALMS** é um acrônimo que representa cinco pilares fundamentais que sustentam a adoção bem-sucedida de práticas **DevOps** em uma organização:

* **C**ultura (Culture)
* **A**utomação (Automation)
* **L**ean
* **M**edição (Measurement)
* **S**haring (Compartilhamento)

O CALMS não é um processo, metodologia ou ferramenta, mas sim um **modelo mental ou estrutura de avaliação** (framework) que ajuda empresas a diagnosticar, guiar e implementar a **transformação DevOps**. Ele fornece uma forma de **avaliar maturidade organizacional** e alinhar práticas técnicas com valores culturais e operacionais.

---

##  Origem do CALMS

###  Quando surgiu?

O conceito **CALMS** foi introduzido por **John Willis** e **Damon Edwards**([ITrevolution][12]) por volta de **2010**, durante os primeiros anos do movimento DevOps. Mais tarde, foi popularizado e sistematizado por **Jez Humble** ([Atlassian][11]) (coautor do livro *"The DevOps Handbook"* e *"Continuous Delivery"*).

Eles perceberam que o sucesso de DevOps não se baseava apenas na automação (como muitos acreditavam na época), mas sim em uma combinação de elementos **culturais, organizacionais e técnicos**. O CALMS surgiu como resposta a essa necessidade de enxergar o DevOps de forma holística.

---

## Por que foi necessário criar o CALMS?

Antes do DevOps, as áreas de desenvolvimento (Dev) e operações (Ops) trabalhavam **em silos**, o que frequentemente resultava em:

* Lançamentos demorados e inseguros.
* Conflitos entre entregar rápido (Dev) e manter estável (Ops).
* Falta de visibilidade, colaboração e feedback.

O **CALMS** surgiu como **modelo de maturidade** e **ponto de partida para adoção DevOps**, ajudando organizações a responder perguntas como:

* “Nossa cultura permite falhas e aprendizado?”
* “Estamos medindo os indicadores certos?”
* “Estamos automatizando processos chave?”
* “Compartilhamos conhecimento entre áreas?”

---

## Quando passou a ser adotado amplamente?

A adoção do CALMS começou a crescer a partir de **2014**, quando DevOps ganhou maior relevância com o lançamento de obras como:

* *The Phoenix Project* (2013)
* *The DevOps Handbook* (2016)
* A consolidação dos conceitos nos eventos **DevOpsDays** e na prática de **Continuous Delivery** em grandes empresas (Netflix, Amazon, Google).

Hoje, o CALMS é amplamente usado por:

* Consultorias e times de transformação digital.
* Plataformas como **Atlassian**, **Microsoft Azure DevOps**, **AWS** e **Google Cloud** para orientar clientes.
* Equipes que desejam mensurar sua **maturidade DevOps** antes de iniciar mudanças profundas.

---

## O que torna o CALMS relevante até hoje?

1. **É atemporal** – ainda que ferramentas mudem, os pilares do CALMS continuam válidos.
2. **É prático e flexível** – aplicável tanto a engenharia de software quanto engenharia de dados.
3. **Ajuda a evitar armadilhas** – como investir em ferramentas de automação sem resolver problemas culturais ou de colaboração.
4. **Facilita diagnósticos e benchmarking** – pode ser usado como base para entrevistas, workshops ou planos de melhoria contínua.

---


## 1. Cultura (Culture / Collaboration)

**Definição:** Construir uma cultura de colaboração, responsabilidade compartilhada, confiança e aprendizado contínuo. É o alicerce do DevOps.([Dev Community Hub][1], [TechTarget][2])

**Exemplo na Engenharia de Software:**

* Times multifuncionais (devs, QA, operações) trabalham juntos desde o planejamento até a produção.
* Post‑mortems sem culpa ("blameless") após incidentes, focando aprendizado em vez de culpabilizar.([Atlassian][3], [Medium][4])

**Exemplo na Engenharia de Dados:**

* Data engineers, analistas de dados e devs colaboram desde o design do pipeline até a entrega dos dados.
* Integração de dados como parte do ciclo contínuo, com respeito mútuo pelos desafios de cada especialidade.
* Estruturas organizacionais como “plataforma de dados” servindo várias equipes, aliviando carga cognitiva, promovendo propriedade e colaboração.([ManageEngine][5])

---

## 2. Automação (Automation)

**Definição:** Automação de tarefas repetitivas no desenvolvimento, implantação, infraestrutura e testes para tornar os processos confiáveis e ágeis.([Atlassian][3], [Graph AI][6])

**Exemplo na Engenharia de Software:**

* Implementação de pipelines CI/CD (com Jenkins, GitLab CI, CircleCI, etc.).
* Usar IaC (Terraform, Ansible) para provisionar infraestrutura identicamente em diferentes ambientes.([Techopedia][7])
* Estratégias de deploy como **Blue/Green** e **Canary**: deploy controlado em ambientes paralelos ou segmentos de usuários, reduzindo riscos.([Tech Futurist][8])

**Exemplo na Engenharia de Dados:**

* Deploy de pipelines de dados (ETL/ELT) automatizado com testes: validação de dados, qualidade, regressão.
* Automação de provisionamento de clusters (Spark, Airflow, banco de dados) via IaC + integração contínua.
* Testes automatizados nos pipelines de dados (dados sintéticos, integridade, esquemas).

---

## 3. Lean

**Definição:** Eliminar desperdícios, focar no que realmente agrega valor, iterar rapidamente e aprender com falhas.([Atlassian][3], [Dev Community Hub][1])

**Exemplo na Engenharia de Software:**

* Entregas frequentes em pequenos lotes. Uso de Kanban e limites de WIP para melhorar fluxo e detectar gargalos.([Techopedia][7], [TechTarget][2])
* Melhorias contínuas com retrospectivas regulares, cultura de antifragilidade — falhar rápido, aprender sempre.([Atlassian][3], [Dev Community Hub][1])

**Exemplo na Engenharia de Dados:**

* Desenvolvimento incremental de pipelines: primeiro validação simples dos dados, depois enriquecimento, monitoramento evolutivo.
* Ajuste de ETL baseado em feedback real (por exemplo, performance ou falhas no processamento).
* Mapear o fluxo de dados, eliminar etapas manuais ou redundantes (e.g., transformações repetidas, handoffs).

---

## 4. Medição (Measurement)

**Definição:** Coletar métricas e dados para avaliar desempenho, tomar decisões e impulsionar melhorias.([ManageEngine][5], [Dev Community Hub][1], [TechTarget][2])

**Exemplo na Engenharia de Software:**

* Uso dos *DORA metrics*: frequência de deployment, lead time, taxa de falha de mudança, tempo de recuperação MTTR.([ManageEngine][5], [Wikipedia][9])
* Dashboards com Prometheus + Grafana para monitoramento e KPIs contínuos, como cobertura de testes, qualidade de código.([Techopedia][7])

**Exemplo na Engenharia de Dados:**

* Métricas específicas de dados: volume processado por hora, latência de ingestão, erros por pipeline, qualidade dos dados (exatidão, completude).
* Monitoramento contínuo de SLA de pipelines, taxas de falhas e tempo de recuperação em caso de interrupções.

---

## 5. Compartilhamento (Sharing)

**Definição:** Facilitar a troca de conhecimento, transparência, documentação, feedback e aprendizado coletivo.([ManageEngine][5], [Dev Community Hub][1])

**Exemplo na Engenharia de Software:**

* Wikis, tech talks internos, repositórios compartilhados e comunidades de prática para disseminar boas práticas.
* Revisões de código e post‑mortems compartilhados entre devs e ops.([Techopedia][7], [Medium][4])

**Exemplo na Engenharia de Dados:**

* Documentação de pipelines, definições de esquemas, contratos de dados acessível a todos.
* Workshops regulares, apresentações internas sobre novas abordagens, dados como produto — promovendo alinhamento entre stakeholders (analistas, usuários finais).
* Feedback loops entre produtores de dados e consumidores (por exemplo, cientistas de dados identificando melhorias nos pipelines).

---

## Resumo

| Pilar            | Engenharia de Software                             | Engenharia de Dados                                                   |
| ---------------- | -------------------------------------------------- | --------------------------------------------------------------------- |
| Cultura          | Times multifuncionais, post‑mortems sem culpa      | Plataformas de dados compartilhadas, colaboração ativa entre times    |
| Automação        | Pipelines CI/CD, IaC, Blue/Green, Canary           | Deploy e monitoramento automáticos de pipelines de dados              |
| Lean             | Entregas em pequenos lotes, Kanban, retrospectivas | Desenvolvimento incremental de pipelines, eliminação de gargalos      |
| Medição          | Métricas DORA, dashboards de performance           | Monitoramento de SLAs, qualidade e performance das pipelines de dados |
| Compartilhamento | Docs, tech talks, revisões de código, post‑mortems | Documentação de dados e pipelines, workshops, alinhamento entre áreas |

---

### O que devemos lembrar?

* O **CALMS** deve ser aplicado de forma integrada — um pilar reforça o outro.([Medium][4], [Dev Community Hub][1])
* Embora o foco inicial tenha sido DevOps em engenharia de software, os mesmos princípios se estendem muito bem à engenharia de dados, com adaptações às necessidades de qualidade, consistência e colaboração no tratamento dos dados.
* Uma abordagem híbrida que combine DevOps com práticas emergentes como MLOps é uma evolução natural, onde pipelines de dados, modelos de ML e aplicações de software compartilham os mesmos princípios de automação, cultura e governança.([TechRadar][10])


[1]: https://devcommunityhub.com/approaches/devops/the-calms-framework-your-essential-compass-for-navigating-devops-culture/?utm_source=chatgpt.com "The CALMS Framework: Your Essential Compass for Navigating DevOps Culture - Dev community hub"
[2]: https://www.techtarget.com/whatis/definition/CALMS?utm_source=chatgpt.com "What is CALMS for DevOps? | Definition from TechTarget"
[3]: https://www.atlassian.com/br/devops/frameworks/calms-framework?utm_source=chatgpt.com "Framework CALMS | Atlassian"
[4]: https://hanancs.medium.com/the-calms-framework-8b8fec4fdd46?utm_source=chatgpt.com "The CALMS Framework. A DevOps Concept | by Ben Subendran | Medium"
[5]: https://www.manageengine.com/br/service-desk/itsm/devops-calms-framework.html?utm_source=chatgpt.com "Estrutura CALMS em DevOps [As três mananeiras e 5 pilares]"
[6]: https://www.graphapp.ai/engineering-glossary/devops/calms-model?utm_source=chatgpt.com "CALMS Model: Definition, Examples, and Applications | Graph AI"
[7]: https://www.techopedia.com/definition/calms?utm_source=chatgpt.com "What is CALMS? Definition, Pillars, and How It Works"
[8]: https://techfuturist.tech/devops-calms-framework-and-ci-cd-pipelines/?utm_source=chatgpt.com "DevOps CALMS Framework and CI/CD Pipelines - Tech Futurist"
[9]: https://en.wikipedia.org/wiki/DevOps_Research_and_Assessment?utm_source=chatgpt.com "DevOps Research and Assessment"
[10]: https://www.techradar.com/pro/breaking-silos-unifying-devops-and-mlops-into-a-unified-software-supply-chain?utm_source=chatgpt.com "Breaking silos: unifying DevOps and MLOps into a unified software supply chain"
[11]: https://www.atlassian.com/devops/frameworks/calms-framework "The acronym was coined by Jez Humble, co-author of “The DevOps Handbook,” and stands for Culture, Automation, Lean, Measurement, and Sharing."
[12]: https://itrevolution.com/articles/devops-culture-part-1/ "After the first US based Devopsdays in Mountainview 2010 Damon Edwards and I coined the acronym CAMS"