
## 5. Métrica 4 – Change Failure Rate (CFR)

### 5.1 Definição

Também chamada “Change Fail Percentage”. Mede a **porcentagem de mudanças (deploys) que causam falha no ambiente de produção**, ou seja, resultam em serviço degradado, incidentes, rollback, hot fix, etc. ([Bookey][1])
Em fórmula simples:



```math

{CFR}={\frac{Número\ de\ deploys\ com\ falha} {correção}}\times{100\%}

```

### 5.2 Por que importa

* Mede a estabilidade/qualidade do processo de entrega: se você entrega rápido mas com muitas falhas, é problemático.
* Ajuda a equilibrar velocidade com confiabilidade — uma parte importante do desempenho de software.
* Alta CFR significa muito retrabalho, altos custos de correção, menor confiança, possivelmente menor moral da equipe.

### 5.3 Como medir

* Definir o que constitui “falha” ou “impacto”: por exemplo, deploy que necessitou de rollback ou hot‐fix ou causou interrupção para o usuário.
* Identificar número de deploys nessa categoria num período.
* Relacionar com o número total de deploys no mesmo período.
* Avaliar a porcentagem.
* Monitorar ao longo do tempo para ver se a taxa está diminuindo ou se há padrões correlacionados com tipos de mudança.

### 5.4 Benchmarks / Categorias

* Equipes de elite: CFR entre **0% a 15%**. ([Santuon][3])
* Equipes alto desempenho: até ~15‑30% (dependendo da indústria). ([Medium][7])
* Equipes de desempenho médio e baixo tendem a ter taxas de 30% ou mais, por vezes acima de 45‑50%. ([Medium][6])

### 5.5 Boas práticas para melhoria

* Induzir mudança menores (lotes menores) → menor risco de falha. ([LinearB][8])
* Automatizar testes, integração, deploy para identificar erros mais cedo (antes de produção).
* Usar feature flags, desativação rápida de funcionalidades, deploy canário para limitar impacto.
* Implantar cultura de “trabalho seguro”: revisões de código, testes automatizados, monitoramento post‑deploy.
* Após falha, realizar análise de causa raiz para evitar reincidência.

### 5.6 Armadilhas / Considerações

* Definição de “falha” precisa estar clara. Se for muito vaga ou muito rígida, métrica perde comparabilidade.
* Focar somente em CFR pode levar a “paralisia” porque a equipe evita deploys para evitar falhas. O foco é equilíbrio: frequência alta + baixo CFR.
* Algumas mudanças são de alto risco inevitável e podem distorcer a métrica se não diferenciar tipo de deploy (por exemplo infra crítica vs bug trivial). Pode fazer sentido segmentar.

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
