
## 4. Métrica 3 – Mean Time to Recovery (MTTR)

### 4.1 Definição

Às vezes chamado “Time to Restore Service” ou “Time to Recover” — mede o tempo médio que a equipe leva para **recuperar** de uma falha em produção, ou seja, desde que um incidente se inicia até que o serviço esteja restaurado ao estado normal ou entregue novamente aos usuários. ([EngMgmtPlatform][5])
É uma métrica de **resiliência** e confiabilidade operacional.

### 4.2 Por que importa

* Em ambientes de software vivo, falhas ocorrem — a métrica não mede se você falha, mas **quanto tempo você leva para se recuperar**. Equipes que se recuperam rapidamente limitam o impacto para o cliente/negócio. ([Bookey][1])
* Uma boa MTTR é indicativo de monitoramento, resposta a incidentes, automação de recuperação, visibilidade operacional, cultura de aprendizagem pós‑morte.
* Baixo MTTR ajuda a manter confiança do usuário, reduzir custo de downtime, minimizar impacto comercial.

### 4.3 Como medir

* Definir claramente “falha” ou “incidente” (por exemplo, degradação de serviço, interrupção que impacta usuário).
* Para cada incidente: registrar o momento de início (por exemplo, alerta ou notificação de falha) e o momento de restauração (quando o serviço voltou a funcionar ou dados liberados novamente).
* Calcular tempo médio de recuperação: (somatório de todos os tempos de recuperação) / (número de incidentes).
* Monitorar tendências e também considerar “tempo até detecção” + “tempo até correção” se possível.
* Verificar quais incidentes foram causados por deploys ou mudanças — há interligação com CFR.

### 4.4 Benchmarks / Categorias

* Equipes de elite: menos de **1 hora** para recuperação. ([Santuon][3])
* Equipes alto desempenho: menos de 1 dia. ([Medium][7])
* Equipes desempenho médio: de 1 dia a 1 semana. ([DEV Community][9])
* Equipes baixo desempenho: uma semana ou mais, possivelmente meses. ([Medium][6])

### 4.5 Boas práticas para melhoria

* Ter monitoramento e alertas eficazes: detectar falhas o mais cedo possível. ([Codurance][4])
* Automatizar procedimentos de rollback ou mitigação (feature flags, canary deploys, circuit breakers).
* Ter equipes cross‑functional que saibam lidar com incidentes de produção e não dependam de longos processos de escalonamento.
* Depois de incidente: fazer análise de causa raiz (post‑mortem) e implementar melhorias para evitar repetição.
* Simular falhas (chaos engineering) ou usar drills de incidentes para treinar a equipe e reduzir tempo real de resposta.

### 4.6 Armadilhas / Considerações

* Definição de “restaurado” pode variar — é preciso acordar “serviço normal” ou “mínimo aceitável”.
* Focar apenas em média pode mascarar incidentes graves raros. Ver variação e máximos também importante.
* Melhorar MTTR não significa que falhas não ocorrem — sim que impacto é contido rapidamente. A métrica de CFR complementa para medir falhas em primeiro lugar.

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
