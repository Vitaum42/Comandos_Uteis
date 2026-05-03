# 🧰 Git — Comandos por Funcionalidade

Este README organiza os comandos do Git **por funcionalidade**, com descrição clara de cada um.

---

## 📁 Inicialização e Clonagem

| Comando           | Descrição                                    |
| ----------------- | -------------------------------------------- |
| `git init`        | Inicializa um repositório Git na pasta atual |
| `git clone <url>` | Clona um repositório remoto para sua máquina |

---

## 🔍 Inspeção e Status

| Comando             | Descrição                                            |
| ------------------- | ---------------------------------------------------- |
| `git status`        | Mostra arquivos modificados, staged e não rastreados |
| `git log`           | Exibe histórico completo de commits                  |
| `git log --oneline` | Histórico resumido (1 linha por commit)              |
| `git diff`          | Mostra alterações ainda não adicionadas              |
| `git diff --staged` | Mostra alterações já adicionadas ao stage            |

---

## ➕ Adição e Commit

| Comando                     | Descrição                                 |
| --------------------------- | ----------------------------------------- |
| `git add <arquivo>`         | Adiciona um arquivo específico ao stage   |
| `git add .`                 | Adiciona todos os arquivos modificados    |
| `git commit -m "mensagem"`  | Cria um commit com mensagem               |
| `git commit -am "mensagem"` | Adiciona e commita arquivos já rastreados |

---

## 🌿 Branches

| Comando                    | Descrição                              |
| -------------------------- | -------------------------------------- |
| `git branch`               | Lista todas as branches                |
| `git branch <nome>`        | Cria uma nova branch                   |
| `git checkout <branch>`    | Troca para outra branch                |
| `git checkout -b <branch>` | Cria e troca para nova branch          |
| `git switch <branch>`      | Alternativa moderna para trocar branch |
| `git switch -c <branch>`   | Cria e troca (forma moderna)           |
| `git branch -d <branch>`   | Remove uma branch                      |

---

## 🔀 Merge e Rebase

| Comando               | Descrição                                           |
| --------------------- | --------------------------------------------------- |
| `git merge <branch>`  | Mescla uma branch na branch atual                   |
| `git rebase <branch>` | Reorganiza commits em outra base (histórico linear) |

---

## 🌐 Repositório Remoto

| Comando                       | Descrição                                     |
| ----------------------------- | --------------------------------------------- |
| `git remote add origin <url>` | Conecta repositório local a um remoto         |
| `git remote -v`               | Lista repositórios remotos                    |
| `git push`                    | Envia commits para o remoto                   |
| `git push -u origin <branch>` | Define upstream e envia                       |
| `git pull`                    | Atualiza com mudanças remotas (fetch + merge) |
| `git fetch`                   | Baixa mudanças sem aplicar                    |

---

## ⚙️ Configuração

| Comando                                    | Descrição                    |
| ------------------------------------------ | ---------------------------- |
| `git config --global user.name "Seu Nome"` | Define nome global           |
| `git config --global user.email "email"`   | Define email global          |
| `git config --list`                        | Lista todas as configurações |

---

## 🧨 Reset e Reversão

| Comando                      | Descrição                             |
| ---------------------------- | ------------------------------------- |
| `git reset <arquivo>`        | Remove arquivo da staging area        |
| `git reset --soft <commit>`  | Volta commit mantendo alterações      |
| `git reset --mixed <commit>` | Volta commit e limpa stage            |
| `git reset --hard <commit>`  | ⚠️ Remove tudo (alterações + stage)   |
| `git revert <commit>`        | Cria commit que desfaz outro (seguro) |

---

## 🧹 Limpeza

| Comando        | Descrição                           |
| -------------- | ----------------------------------- |
| `git clean -n` | Mostra arquivos que serão removidos |
| `git clean -f` | Remove arquivos não rastreados      |

---

## 🏷️ Tags

| Comando                 | Descrição               |
| ----------------------- | ----------------------- |
| `git tag`               | Lista tags existentes   |
| `git tag <nome>`        | Cria uma nova tag       |
| `git push origin <tag>` | Envia tag para o remoto |

---

## ⚠️ Boas práticas

* Use `git status` frequentemente
* Prefira `git revert` ao invés de `reset --hard` em equipe
* Faça commits pequenos e descritivos
* Trabalhe com branches (`feature/nome`)
* Evite commits diretos na `main`

---
