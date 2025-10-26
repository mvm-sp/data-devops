Este é um **estudo prático em JavaScript** mostrando comparações **na sequência** entre:

* **Código “ruim”** (sem Padrões de Código e sem Style Guide);
* **Código “bom”** (com aplicação correta de **Padrões de Código** *e* **Style Guide**).

Cada exemplo traz explicações do que está errado e como foi corrigido.

---

#  EXEMPLO 1 — Estrutura e Nomeação de Funções

### ❌ Sem padrões de código nem style guide

```javascript
function calc(a,b,c){
if(a=="sum"){return b+c}else if(a=="sub"){return b-c}else if(a=="mul"){return b*c}else if(a=="div"){return b/c}
}
```

### Problemas

* Nenhuma indentação → difícil de ler.
* Nomes vagos: `calc`, `a`, `b`, `c`.
* Uso incorreto de igualdade (`==` em vez de `===`).
* Falta de tratamento de erros (divisão por zero).
* Falta de consistência visual (quebra de linha, espaços, ponto e vírgula).

---

### ✅ Com Padrões de Código e Style Guide

```javascript
/**
 * Performs a basic arithmetic operation between two numbers.
 * @param {string} operation - One of: "add", "subtract", "multiply", "divide".
 * @param {number} x - First operand.
 * @param {number} y - Second operand.
 * @returns {number} Result of the operation.
 */
function calculate(operation, x, y) {
  if (typeof x !== 'number' || typeof y !== 'number') {
    throw new Error('Operands must be numbers.');
  }

  switch (operation) {
    case 'add':
      return x + y;
    case 'subtract':
      return x - y;
    case 'multiply':
      return x * y;
    case 'divide':
      if (y === 0) throw new Error('Cannot divide by zero.');
      return x / y;
    default:
      throw new Error(`Unknown operation: ${operation}`);
  }
}
```

### Correções aplicadas

* **Padrões de Código:**

  * Nomes claros e descritivos (`calculate`, `operation`, `x`, `y`).
  * Validação de entrada.
  * Uso de `switch` para clareza.
  * Tratamento de exceções.

* **Style Guide:**

  * Indentação de 2 espaços.
  * Espaços ao redor de operadores.
  * Comentário JSDoc padronizado.
  * Quebras de linha consistentes.
  * Uso de `===` e boas práticas semicolons automáticos.

---

#  EXEMPLO 2 — Estrutura de Classe e Organização de Código

### ❌ Código sem padrão nem estilo

```javascript
class user{
constructor(n,a){
this.n=n
this.a=a}
sayhi(){
console.log("hi "+this.n+" your age is "+this.a)
}}
u=new user("ana",22)
u.sayhi()
```

### Problemas

* Nomes de classe e variáveis em minúsculas.
* Ausência de espaços e quebras de linha.
* Atributos sem significado (`n`, `a`).
* Código não modular (instância global).
* Saída concatenada sem interpolação.

---

### ✅ Código com Padrões de Código + Style Guide

```javascript
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHi() {
    console.log(`Hi ${this.name}, you are ${this.age} years old.`);
  }
}

// Instantiation
const user = new User('Ana', 22);
user.sayHi();
```

### Correções aplicadas

* **Padrões de Código:**

  * Classe nomeada com `PascalCase` (`User`).
  * Variáveis com `camelCase` (`user`, `name`, `age`).
  * Código encapsulado e coeso (SRP).

* **Style Guide:**

  * Indentação padronizada.
  * Espaços ao redor de operadores e chaves.
  * Template literals para legibilidade.
  * Comentário simples de contexto.

---

# EXEMPLO 3 — Modularização e Organização de Arquivos

### ❌ Sem padrões

```javascript
// file1.js
function d(a,b){return a*b}

// file2.js
import * as f from './file1.js'
console.log(f.d(3,4))
```

### Problemas

* Função nomeada sem propósito (`d`).
* Módulo com nome genérico (`f`).
* Falta de documentação.
* Estrutura de pastas e import confusos.

---

### ✅ Com Padrões e Style Guide

```javascript
// utils/mathOperations.js
/**
 * Multiplies two numbers.
 * @param {number} x 
 * @param {number} y 
 * @returns {number}
 */
export function multiply(x, y) {
  return x * y;
}

// app.js
import { multiply } from './utils/mathOperations.js';

console.log(multiply(3, 4));
```

### Correções aplicadas

* **Padrões de Código:**

  * Nomeação semântica (`multiply`).
  * Módulos organizados por responsabilidade (`utils/`).
  * Export/import explícitos.

* **Style Guide:**

  * Documentação JSDoc.
  * Linhas curtas, espaçamento consistente.
  * Nomes de arquivos em `camelCase` e minúsculo.

---

# EXEMPLO 4 — Tratamento de Erros e Controle de Fluxo

### ❌ Sem padrões

```javascript
function getUser(id){
return fetch("https://api.exemplo.com/users/"+id).then(r=>r.json()).then(d=>console.log(d)).catch(e=>console.log("err"))
}
```

### Problemas

* Fluxo difícil de ler (encadeamento longo).
* Falta de nomes significativos.
* Mensagens genéricas de erro.
* Concatenação de strings.
* Falta de `await` e tratamento adequado.

---

### ✅ Com Padrões e Style Guide

```javascript
/**
 * Fetches a user by ID from the API.
 * @param {number} userId
 * @returns {Promise<Object>}
 */
async function getUser(userId) {
  try {
    const response = await fetch(`https://api.exemplo.com/users/${userId}`);
    if (!response.ok) throw new Error(`Request failed: ${response.status}`);
    
    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error(`Error fetching user ${userId}:`, error.message);
    throw error;
  }
}
```

### Correções aplicadas

* **Padrões de Código:**

  * Uso de `async/await` para clareza.
  * Validação e tratamento estruturado de erros.
  * Nomeação expressiva (`userId`, `data`, `response`).

* **Style Guide:**

  * Interpolação em template literals.
  * Indentação e espaçamento consistentes.
  * Log e mensagens descritivas.

---

# CONCLUSÃO COMPARATIVA

| Critério              | Sem Padrões / Estilo               | Com Padrões e Style Guide       |
| --------------------- | ---------------------------------- | ------------------------------- |
| **Legibilidade**      | Caótica, difícil de entender       | Clareza e consistência          |
| **Manutenção**        | Propensa a erros e retrabalho      | Fácil de manter e revisar       |
| **Erros e Exceções**  | Sem tratamento                     | Tratamento robusto e previsível |
| **Nomes e Estrutura** | Ambíguos e curtos                  | Significativos e coesos         |
| **Automação**         | Sem suporte a linters/formatadores | Compatível com ESLint/Prettier  |
| **Colaboração**       | Código inconsistente entre autores | Equipe com estilo unificado     |

---

