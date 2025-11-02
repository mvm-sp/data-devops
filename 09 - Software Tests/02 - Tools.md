
# **Principais Ferramentas de Teste de Software**

Organizadas por tipo de teste, com breve descrição, quando usar e exemplos práticos em **JavaScript**, **Python** ou **Gherkin**, conforme o caso.

---

## **Testes Unitários**

**Objetivo:** validar o comportamento de funções ou classes isoladas, garantindo que cada unidade funcione corretamente de forma independente.

---

### **Jest (JavaScript)**

* **Uso:** framework popular para Node.js e React; inclui mocks, assertions e relatórios de cobertura.
* **Quando usar:** sempre que houver funções ou componentes isoláveis.
* **Exemplo:**

```javascript
// math.js
function somar(a, b) { return a + b; }
module.exports = somar;

// math.test.js
const somar = require('./math');
test('deve somar corretamente', () => {
  expect(somar(3, 5)).toBe(8);
});
```

**Execução:** `npx jest`

---

## **Testes de Integração**

**Objetivo:** validar a comunicação entre módulos, APIs, bancos e serviços.

---

### **Supertest + Jest (APIs REST)**

* **Uso:** simula requisições HTTP reais a endpoints.
* **Exemplo:**

```javascript
const request = require('supertest');
const app = require('./app');

test('GET /ping deve retornar ok', async () => {
  const res = await request(app).get('/ping');
  expect(res.status).toBe(200);
});
```

**Execução:** `npx jest`

---

### **Robot Framework (Python)**

* **Uso:** framework genérico baseado em palavras-chave, fácil de ler e estender.
* **Quando usar:** automação de testes funcionais, integrações ou RPA.
* **Exemplo:**

```robot
*** Settings ***
Library           SeleniumLibrary

*** Test Cases ***
Abrir Página Inicial
    Open Browser    https://minhaapp.com    chrome
    Title Should Be    Minha Aplicação
```

**Execução:** `robot testes.robot`

> ✅ Ideal para times multidisciplinares, pois usa sintaxe natural e integra com CI/CD.

---

## **Testes Automatizados de Interface (E2E)**

**Objetivo:** simular a interação do usuário com o sistema — cliques, formulários, navegação, etc.

---

### **Cypress (JavaScript)**

* **Uso:** ferramenta moderna de testes E2E; roda dentro do navegador real.
* **Diferenciais:** fácil debug visual, time travel, integração nativa com CI.
* **Exemplo:**

```javascript
describe('Login', () => {
  it('deve permitir login com credenciais válidas', () => {
    cy.visit('/login');
    cy.get('#usuario').type('admin');
    cy.get('#senha').type('123456');
    cy.get('button[type=submit]').click();
    cy.url().should('include', '/dashboard');
  });
});
```

**Execução:** `npx cypress run` ou `npx cypress open`

---

### **Playwright (JavaScript/TypeScript)**

* **Uso:** testes multiplataforma (Chromium, Firefox, WebKit).
* **Exemplo:**

```javascript
const { test, expect } = require('@playwright/test');
test('verifica login', async ({ page }) => {
  await page.goto('https://minhaapp.com/login');
  await page.fill('#usuario', 'admin');
  await page.fill('#senha', '123456');
  await page.click('button[type=submit]');
  await expect(page).toHaveURL('/dashboard');
});
```

**Execução:** `npx playwright test`

---

### **Cucumber (JavaScript / Gherkin)**

* **Uso:** permite escrever testes no formato **BDD (Behavior Driven Development)**, aproximando times técnicos e de negócio.
* **Quando usar:** requisitos expressos como “cenários” legíveis por humanos.
* **Exemplo (Gherkin + JS):**

 `login.feature`

```gherkin
Funcionalidade: Login no sistema
  Cenário: Login bem-sucedido
    Dado que estou na tela de login
    Quando insiro usuário "admin" e senha "123456"
    Então devo ver a página de dashboard
```

 `login.steps.js`

```javascript
const { Given, When, Then } = require('@cucumber/cucumber');
const { chromium } = require('playwright');

let page;
Given('que estou na tela de login', async () => {
  const browser = await chromium.launch();
  page = await browser.newPage();
  await page.goto('https://minhaapp.com/login');
});
When('insiro usuário {string} e senha {string}', async (u, s) => {
  await page.fill('#usuario', u);
  await page.fill('#senha', s);
  await page.click('button[type=submit]');
});
Then('devo ver a página de dashboard', async () => {
  expect(await page.url()).toContain('/dashboard');
});
```

**Execução:** `npx cucumber-js`

---

## **Testes de Performance**

**Objetivo:** medir desempenho sob carga, latência e estabilidade.

---

### **k6 (JavaScript)**

* **Uso:** scripts JS descrevem cenários com usuários virtuais.
* **Exemplo:**

```javascript
import http from 'k6/http';
export let options = { vus: 50, duration: '30s' };
export default function() {
  http.get('https://api.minhaapp.com');
}
```

**Execução:** `k6 run script.js`

---

### **Artillery (YAML ou JS)**

* **Uso:** simples e ideal para pipelines CI/CD.
* **Exemplo:**

```yaml
config:
  target: "https://api.minhaapp.com"
  phases:
    - duration: 60
      arrivalRate: 10
scenarios:
  - flow:
      - get:
          url: "/usuarios"
```

**Execução:** `npx artillery run perf.yml`

---

## **Testes de Vulnerabilidade (Automatizados)**

**Objetivo:** detectar falhas de segurança conhecidas, versões inseguras e dependências vulneráveis.

---

### **npm audit (JavaScript)**

* **Uso:** escaneia dependências Node.js.
* **Exemplo:**

```bash
npm audit
```

### **Snyk (Multi-linguagem)**

* **Uso:** verifica vulnerabilidades e sugere patches automáticos.
* **Exemplo:**

```bash
snyk test
```

### **OWASP ZAP**

* **Uso:** scanner de segurança web, detecta falhas de injeção, XSS e cabeçalhos inseguros.
* **Exemplo:**

```bash
zap-baseline.py -t https://minhaapp.com -r relatorio.html
```

---

##  **Testes de Penetração (Pentest)**

**Objetivo:** simular ataques reais para avaliar resiliência a invasões e vazamentos.
**Importante:** exigem autorização formal e são conduzidos por especialistas.

---

### **Burp Suite**

* **Uso:** proxy para interceptar e manipular requisições HTTP, detectar falhas e automatizar varreduras.
* **Fluxo:** configurar proxy → capturar tráfego → testar endpoints com Intruder/Repeater.

---

### **Metasploit**

* **Uso:** estrutura de exploração e pós-exploração (testa payloads e vulnerabilidades conhecidas).
* **Exemplo (terminal):**

```text
msfconsole
use exploit/multi/handler
set payload linux/x86/meterpreter/reverse_tcp
set LHOST 10.0.0.5
exploit
```

---

### **Nmap**

* **Uso:** varredura de rede, portas abertas, versões de serviço.
* **Exemplo:**

```bash
nmap -sV -p 1-65535 minhaapp.com
```

---

## **Resumo Consolidado**

| Tipo de Teste   | Ferramentas Principais        | Linguagem / Interface | Uso Principal               |
| --------------- | ----------------------------- | --------------------- | --------------------------- |
| Unitário        | Jest, Mocha                   | JavaScript            | Funções isoladas            |
| Integração      | Supertest, Robot Framework    | JS / Python           | Comunicação entre serviços  |
| E2E / UI        | Cypress, Playwright, Cucumber | JavaScript / Gherkin  | Fluxos completos do usuário |
| Performance     | k6, Artillery                 | JavaScript / YAML     | Carga e latência            |
| Vulnerabilidade | Snyk, npm audit, OWASP ZAP    | CLI / Web             | Falhas conhecidas           |
| Pentest         | Burp Suite, Metasploit, Nmap  | Manual / CLI          | Ataques simulados reais     |

---

## **Boas Práticas Gerais**

* Automatize **unitários, integração e vulnerabilidade** no CI/CD.
* Execute **testes de performance** periodicamente em ambientes de *staging*.
* Conduza **pentests manuais** após grandes atualizações.
* Gere relatórios automáticos de cobertura e vulnerabilidades.
* Use **BDD (Cucumber)** para alinhar times técnicos e de negócio.
* Integre tudo em pipelines (GitHub Actions, Jenkins, GitLab CI).

