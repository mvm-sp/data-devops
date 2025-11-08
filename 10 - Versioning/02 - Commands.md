
# Comandos Git Mais Utilizados — Guia Prático e Explicado

O **Git** é o coração do versionamento moderno.
Dominar seus comandos principais é essencial para trabalhar com **colaboração, CI/CD e controle de releases**.

---

## Inicialização e Configuração do Repositório

| Comando           | Função                                   | Exemplo                                                                                           | Explicação                                                               |
| ----------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| `git init`        | Inicializa um repositório Git local      | `git init`                                                                                        | Cria a pasta `.git` e começa o controle de versão no diretório atual.    |
| `git clone <url>` | Clona um repositório remoto              | `git clone https://github.com/usuario/repositorio.git`                                            | Copia o repositório remoto para a máquina local.                         |
| `git config`      | Define configurações de usuário e editor | `git config --global user.name "Marcelo"`<br>`git config --global user.email "marcelo@email.com"` | As configurações `--global` valem para todos os repositórios do sistema. |

---

## Gerenciamento de Arquivos e Commits

| Comando                     | Função                                | Exemplo                                                 | Explicação                                         |
| --------------------------- | ------------------------------------- | ------------------------------------------------------- | -------------------------------------------------- |
| `git status`                | Mostra o status atual do repositório  | `git status`                                            | Indica arquivos modificados, novos e rastreados.   |
| `git add <arquivo>`         | Adiciona arquivos à área de stage     | `git add index.html`                                    | Move o arquivo para o “pré-commit”.                |
| `git add .`                 | Adiciona todas as alterações          | `git add .`                                             | Útil para adicionar múltiplos arquivos de uma vez. |
| `git commit -m "mensagem"`  | Cria um commit com mensagem           | `git commit -m "feat(api): adiciona endpoint de login"` | Registra oficialmente as alterações.               |
| `git commit -am "mensagem"` | Adiciona e comita arquivos rastreados | `git commit -am "fix(css): corrige alinhamento"`        | Evita precisar rodar `git add` antes.              |
| `git log`                   | Exibe histórico de commits            | `git log --oneline --graph --decorate`                  | Mostra histórico de forma resumida e visual.       |

---

## Branches e Fluxo de Trabalho

| Comando                    | Função                                | Exemplo                            | Explicação                                 |
| -------------------------- | ------------------------------------- | ---------------------------------- | ------------------------------------------ |
| `git branch`               | Lista as branches locais              | `git branch`                       | Mostra em qual branch você está.           |
| `git branch <nome>`        | Cria uma nova branch                  | `git branch feature/login`         | Cria a branch, mas não muda para ela.      |
| `git checkout <branch>`    | Troca para outra branch               | `git checkout feature/login`       | Move o HEAD para a branch especificada.    |
| `git checkout -b <branch>` | Cria e troca de branch ao mesmo tempo | `git checkout -b feature/cadastro` | Muito usado no início de novas tarefas.    |
| `git merge <branch>`       | Junta outra branch à atual            | `git merge feature/login`          | Integra alterações e pode gerar conflitos. |
| `git branch -d <branch>`   | Exclui uma branch local               | `git branch -d feature/antiga`     | Use `-D` para forçar a exclusão.           |

---

## Atualização e Sincronização com Repositórios Remotos

| Comando                       | Função                                   | Exemplo                         | Explicação                                                 |
| ----------------------------- | ---------------------------------------- | ------------------------------- | ---------------------------------------------------------- |
| `git remote -v`               | Mostra repositórios remotos configurados | `git remote -v`                 | Exibe URLs associadas ao repositório local.                |
| `git fetch`                   | Baixa atualizações do remoto sem aplicar | `git fetch origin`              | Atualiza as referências locais, mas não altera seu código. |
| `git pull`                    | Baixa e integra atualizações             | `git pull origin main`          | Equivale a `fetch + merge`.                                |
| `git push`                    | Envia commits locais para o remoto       | `git push origin feature/login` | Sobe suas alterações para o servidor.                      |
| `git push -u origin <branch>` | Define branch remota padrão              | `git push -u origin develop`    | Após isso, pode usar apenas `git push`.                    |

---

## Controle de Histórico e Reversão

| Comando                     | Função                                      | Exemplo                    | Explicação                                       |
| --------------------------- | ------------------------------------------- | -------------------------- | ------------------------------------------------ |
| `git diff`                  | Mostra diferenças entre commits/arquivos    | `git diff`                 | Exibe mudanças não comitadas.                    |
| `git diff --staged`         | Mostra diferenças no stage                  | `git diff --staged`        | Exibe o que será incluído no próximo commit.     |
| `git reset <arquivo>`       | Remove arquivo do stage                     | `git reset index.html`     | Tira o arquivo da área de commit sem apagar.     |
| `git restore <arquivo>`     | Restaura arquivo modificado                 | `git restore app.js`       | Desfaz alterações locais não comitadas.          |
| `git revert <commit>`       | Cria um novo commit que desfaz o anterior   | `git revert 7a2f5d3`       | Ideal para reverter sem alterar histórico.       |
| `git reset --hard <commit>` | Volta o repositório para um commit anterior | `git reset --hard 1d2a3f4` | ⚠️ Cuidado: descarta mudanças irreversivelmente. |

---

## 6. Comparação e Inspeção

| Comando                | Função                                    | Exemplo               | Explicação                               |
| ---------------------- | ----------------------------------------- | --------------------- | ---------------------------------------- |
| `git show <commit>`    | Mostra detalhes de um commit              | `git show 7a2f5d3`    | Inclui autor, data e diffs.              |
| `git blame <arquivo>`  | Mostra autor de cada linha                | `git blame main.py`   | Útil para identificar quem alterou algo. |
| `git log -p <arquivo>` | Exibe histórico de mudanças de um arquivo | `git log -p index.js` | Mostra commits e diffs daquele arquivo.  |

---

## Tags e Releases

| Comando                                  | Função                        | Exemplo                                   | Explicação                                   |
| ---------------------------------------- | ----------------------------- | ----------------------------------------- | -------------------------------------------- |
| `git tag`                                | Lista tags existentes         | `git tag`                                 | Mostra as versões marcadas.                  |
| `git tag v1.0.0`                         | Cria uma tag simples          | `git tag v1.2.0`                          | Marca o commit atual como uma versão.        |
| `git push origin v1.0.0`                 | Envia uma tag para o remoto   | `git push origin v2.0.0`                  | Publica a tag no repositório remoto.         |
| `git tag -a v1.0.0 -m "Release estável"` | Cria tag anotada com mensagem | `git tag -a v1.0.0 -m "Primeira release"` | Usada em pipelines de release automatizadas. |

---

## Rebase e Otimização do Histórico

| Comando                    | Função                                      | Exemplo                   | Explicação                                      |
| -------------------------- | ------------------------------------------- | ------------------------- | ----------------------------------------------- |
| `git rebase <branch>`      | Reorganiza commits sobre outra branch       | `git rebase main`         | Mantém histórico linear (sem merges visuais).   |
| `git rebase -i HEAD~3`     | Rebase interativo (editar histórico)        | `git rebase -i HEAD~3`    | Permite editar, juntar ou remover commits.      |
| `git cherry-pick <commit>` | Aplica um commit específico em outra branch | `git cherry-pick 9d4f0a1` | Traz apenas aquela mudança, sem merge completo. |

---

## Limpeza e Manutenção

| Comando         | Função                            | Exemplo         | Explicação                                      |
| --------------- | --------------------------------- | --------------- | ----------------------------------------------- |
| `git clean -f`  | Remove arquivos não rastreados    | `git clean -f`  | Limpa arquivos fora do controle do Git.         |
| `git gc`        | Faz limpeza e compressão de dados | `git gc`        | “Garbage collection” — otimiza o repositório.   |
| `git stash`     | Guarda alterações temporariamente | `git stash`     | Salva alterações sem commit para voltar depois. |
| `git stash pop` | Recupera alterações guardadas     | `git stash pop` | Restaura o último `stash` salvo.                |

---

## Fluxo Prático de Trabalho (Exemplo Real)

Um exemplo prático de ciclo de desenvolvimento moderno usando Git:

```bash
# 1. Clonar repositório
git clone https://github.com/empresa/api.git
cd api

# 2. Criar nova branch para a feature
git checkout -b feature/autenticacao

# 3. Adicionar e comitar alterações
git add .
git commit -m "feat(auth): adiciona validação JWT"

# 4. Atualizar branch principal e integrar
git fetch origin
git rebase origin/main

# 5. Subir branch e abrir Pull Request
git push -u origin feature/autenticacao
```

---

## Dicas Extras e Boas Práticas

✅ Use **commits pequenos e descritivos**
✅ Atualize a branch antes de fazer o `merge` (`git pull --rebase`)
✅ **Nunca** force push (`git push -f`) em branches compartilhadas
✅ Automatize checagens com pipelines (lint, testes, builds)
✅ Utilize **tags e releases** para marcar versões de produção

