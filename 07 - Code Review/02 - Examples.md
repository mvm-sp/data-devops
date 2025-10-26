

## Exemplo 1 — Nomeação pouco clara de variáveis

### 🔹 Código original (com inconformidade)

```javascript
function calc(a, b) {
  return a * b / 100;
}
```

### Comentário do revisor

>  *Comentário:*
> O nome da função e dos parâmetros não é muito descritivo. “calc” e “a, b” não deixam claro o que está sendo calculado.
> Sugiro utilizar nomes mais significativos para melhorar a legibilidade e facilitar manutenção futura.

### ✅ Código revisado e aprovado

```javascript
function calculateDiscount(price, discountPercentage) {
  return price * discountPercentage / 100;
}
```

**Lições:**

* Evite nomes genéricos.
* Prefira nomes que expressem **intenção**.

---

## Exemplo 2 — Falta de tratamento de erros

### 🔹 Código original

```javascript
async function fetchUser(id) {
  const response = await fetch(`/api/users/${id}`);
  const data = await response.json();
  return data;
}
```

### Comentário do revisor

>  *Comentário:*
> Esta função não trata possíveis erros na requisição, como falha de rede ou resposta 404.
> Seria importante adicionar tratamento de exceções para evitar falhas silenciosas no sistema.

### ✅ Código revisado

```javascript
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) {
      throw new Error(`Erro na requisição: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error("Erro ao buscar usuário:", error);
    return null;
  }
}
```

**Lições:**

* Sempre trate erros de rede e exceções em funções assíncronas.
* Um bom *review* valoriza **resiliência e robustez**.

---

## Exemplo 3 — Problema de segurança: injeção de HTML

### 🔹 Código original

```javascript
function renderMessage(message) {
  document.getElementById("output").innerHTML = `<p>${message}</p>`;
}
```

### Comentário do revisor

> *Comentário:*
> Inserir conteúdo direto em `innerHTML` pode gerar vulnerabilidade XSS se `message` vier de entrada do usuário.
> Recomendo usar `textContent` ou sanitizar o valor antes de renderizar.

### ✅ Código revisado

```javascript
function renderMessage(message) {
  const output = document.getElementById("output");
  const paragraph = document.createElement("p");
  paragraph.textContent = message;
  output.appendChild(paragraph);
}
```

**Lições:**

* Revisões devem incluir **checagens de segurança**.
* Evitar manipulação direta de HTML com dados externos.

---

## Exemplo 4 — Duplicação de código

### 🔹 Código original

```javascript
function getUserName(user) {
  if (user && user.name) {
    return user.name;
  } else {
    return "Anônimo";
  }
}

function getUserEmail(user) {
  if (user && user.email) {
    return user.email;
  } else {
    return "Não informado";
  }
}
```

### Comentário do revisor

> *Comentário:*
> Há duplicação de lógica nas duas funções (`if (user && user.prop)`).
> Talvez seja interessante criar uma função auxiliar genérica para reaproveitar o código.

### ✅ Código revisado

```javascript
function getUserProperty(user, prop, defaultValue) {
  return user && user[prop] ? user[prop] : defaultValue;
}

function getUserName(user) {
  return getUserProperty(user, "name", "Anônimo");
}

function getUserEmail(user) {
  return getUserProperty(user, "email", "Não informado");
}
```

**Lições:**

* Revisores atentos buscam **simplificação e reutilização**.
* Um *review* de qualidade identifica padrões repetitivos.

---

## Exemplo 5 — Falta de testes e cobertura

### 🔹 Código original

```javascript
function sum(a, b) {
  return a + b;
}
```

### Comentário do revisor

> *Comentário:*
> A função é simples, mas seria bom incluir um teste unitário básico.
> Mesmo funções pequenas devem ser cobertas para manter consistência da suíte de testes.

### ✅ Código revisado com teste

```javascript
// Código-fonte
function sum(a, b) {
  return a + b;
}

// Teste (usando Jest)
test("soma dois números corretamente", () => {
  expect(sum(2, 3)).toBe(5);
});
```

**Lições:**

* Revisões podem (e devem) exigir **testes unitários**.
* Garantem qualidade contínua e confiança em futuras alterações.

---

## Boas práticas de comunicação no *Code Review*

| Tipo de comentário     | Exemplo de má prática | Exemplo de boa prática                                                                                |
| ---------------------- | --------------------- | ----------------------------------------------------------------------------------------------------- |
| **Técnico**            | “Isso está errado.”   | “Acho que essa lógica pode falhar em casos nulos. Que tal usar `??` para tratar valores indefinidos?” |
| **Estilo**             | “Use nomes melhores.” | “O nome ‘data’ é genérico; talvez ‘userData’ descreva melhor o conteúdo.”                             |
| **Sugerindo melhoria** | “Mude isso.”          | “Poderíamos usar `Array.map()` aqui — reduz a complexidade e melhora legibilidade.”                   |

---

## ✅ Conclusão

Um *Code Review* eficaz:

* **não busca culpados**, busca **melhoria contínua**;
* **valoriza clareza, segurança e manutenção**;
* **gera aprendizado mútuo e cultura de qualidade**.

