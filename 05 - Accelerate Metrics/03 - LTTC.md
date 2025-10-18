
## 3. Métrica 2 – Lead Time to Changes (LTTC)

### 3.1 Definição

Também chamada “Lead Time for Changes”. É o tempo que leva desde o momento em que uma mudança de código é **comitada** (ou iniciada) até o momento em que essa mudança está **em produção** ou entregue aos usuários. ([Medium][6])
Em outras descrições pode-se referir ao tempo entre “primeiro commit” até “mudança em produção”. ([Medium][7])

### 3.2 Por que importa

* Essa métrica captura a eficiência de todo o pipeline de entrega (desde desenvolvimento até produção). Quanto menor esse tempo, mais rápido a equipe responde a mudanças, bugs, feedbacks ou oportunidades de negócio.
* Também é indicador de gargalos: se o lead time for alto, talvez exista espera longa para testes, aprovação, integração, deploy, etc.
* Alta performance aqui permite que a empresa tenha vantagem competitiva: entregar antes, iterar mais rápido, ajustar ao mercado.

### 3.3 Como medir

* Definir o ponto inicial (por exemplo, timestamp do commit na branch principal) e o ponto final (por exemplo, timestamp em que a mudança está disponível em produção ou acessível ao cliente).
* Medir para cada mudança ou média de mudanças num período.
* Preferencialmente agrupar por lotes ou tipo de mudança para entender variações (ex: bug fix vs nova funcionalidade).
* Plotar tendência: está descendo ou subindo?

### 3.4 Benchmarks / Categorias

* Equipes de elite: menos de **1 hora** (ou mesmo “praticamente imediato”) para deploy de mudanças. ([Bookey][1])
* Equipes alto desempenho: entre 1 dia e 1 semana. ([Medium][7])
* Equipes desempenho médio: entre 1 semana e 1 mês ou mais. ([Santuon][3])
* Equipes baixo desempenho: 1 mês a 6 meses ou mais. ([Medium][7])

### 3.5 Boas práticas para melhoria

* Reduzir tamanho de mudança (lotes menores) → menos dependências, menos testes demorados. ([LinearB][8])
* Automatizar testes, build, integração, deploy para minimizar atrasos manuais. ([Codurance][4])
* Trabalhar com trunk‑based development (branch curta), evitar longas divergências.
* Eliminar ou reduzir esperas: aprovações manuais, espera por ambiente, bloqueios de deploy.
* Visualizar fluxo de trabalho para identificar gargalos: onde há espera, revisão, teste, integração que demoram?
* Fomentar cultura de entrega contínua: mudanças pequenas, deploys frequentes, feedback rápido.

### 3.6 Armadilhas / Considerações

* Definição de “mudança” pode variar: correção de bug pequeno vs grande feature; variáveis importantes para entender.
* Atenção para não sacrificar qualidade apenas para reduzir lead time. Reduzir lead time com mais falhas não é desejável — por isso precisamos métricas de estabilidade também.
* Métrica média pode esconder caudas longas ou “picos ruins”. É útil ver distribuição, não só média.

---



[1]: https://www.bookey.app/book/accelerate?utm_source=chatgpt.com "Accelerate Chapter Summary | Nicole Forsgren"
[2]: https://waydev.co/accelerate-metrics/?utm_source=chatgpt.com "The \"Accelerate Four\": Metrics to measure DevOps performance"
[3]: https://www.santuon.com/accelerate-the-science-of-lean-software-and-devops-thoughts-and-review/?utm_source=chatgpt.com "Accelerate: The Science of Lean Software and DevOps - Thoughts and Review"
[4]: https://www.codurance.com/publications/2020/03/12/achieving-stability-and-speed-in-software-delivery?utm_source=chatgpt.com "Achieving Stability and Speed in Software Delivery | Codurance"
[5]: https://enji.ai/glossary/accelerate-metrics/?utm_source=chatgpt.com "What Are Accelerate Metrics? | Performance Metrics Glossary"
[6]: https://medium.com/%40muralidharnayakg/dora-metrics-assessing-devops-performance-b07a2411aaaf?utm_source=chatgpt.com "DORA Metrics: Assessing DevOps Performance | by Muralidhar Nayak | Paymatrix | Medium"
[7]: https://medium.com/%40dmyoko/the-four-key-metrics-from-accelerate-a53f75c105b6?utm_source=chatgpt.com "The Four Key Metrics from Accelerate | by Daniel Yokoyama | Medium"
[8]: https://linearb.io/blog/accelerate-metrics?utm_source=chatgpt.com "What Are The Four Accelerate Metrics And Why Do They Matter? | LinearB Blog"
[9]: https://dev.to/jonlauridsen/the-software-delivery-performance-model-dora-metrics-2nf4?utm_source=chatgpt.com "Accelerate's \"Software Delivery Performance\" model & DORA metrics - DEV Community"
[10]: https://en.wikipedia.org/wiki/DevOps_Research_and_Assessment?utm_source=chatgpt.com "DevOps Research and Assessment"
