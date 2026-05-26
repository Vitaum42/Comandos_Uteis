# 🔤 Linux — Atalhos e Produtividade no Terminal

Este guia cobre atalhos de teclado, personalização e ferramentas que aumentam sua eficiência no terminal.

---

## ⌨️ Atalhos Essenciais do Terminal

### Controle de execução

| Atalho | Ação |
| ------ | ---- |
| `Ctrl + C` | Cancela/mata o processo em execução |
| `Ctrl + Z` | Suspende o processo (coloca em background) |
| `Ctrl + D` | Encerra a sessão atual do terminal (EOF) |
| `Ctrl + \` | Envia sinal SIGQUIT (saída com core dump) |

---

### Navegação na linha de comando

| Atalho | Ação |
| ------ | ---- |
| `Ctrl + A` | Move o cursor para o **início** da linha |
| `Ctrl + E` | Move o cursor para o **fim** da linha |
| `Ctrl + ←` | Move uma palavra para a esquerda |
| `Ctrl + →` | Move uma palavra para a direita |
| `Alt + B` | Volta uma palavra |
| `Alt + F` | Avança uma palavra |

---

### Edição na linha de comando

| Atalho | Ação |
| ------ | ---- |
| `Ctrl + U` | Apaga do cursor até o **início** da linha |
| `Ctrl + K` | Apaga do cursor até o **fim** da linha |
| `Ctrl + W` | Apaga a palavra à esquerda do cursor |
| `Alt + D` | Apaga a palavra à direita do cursor |
| `Ctrl + Y` | Cola o que foi apagado com `Ctrl+U/K/W` |
| `Ctrl + H` | Apaga o caractere à esquerda (Backspace) |
| `Ctrl + T` | Troca os dois últimos caracteres |
| `Alt + U` | Converte a palavra para MAIÚSCULAS |
| `Alt + L` | Converte a palavra para minúsculas |

---

### Histórico de comandos

| Atalho / Comando | Ação |
| ---------------- | ---- |
| `↑` / `↓` | Navega pelo histórico de comandos |
| `Ctrl + R` | Busca interativa no histórico (digite para filtrar) |
| `Ctrl + G` | Cancela a busca no histórico |
| `!!` | Repete o último comando |
| `!<número>` | Repete o comando pelo número no histórico |
| `!<texto>` | Repete o último comando que começa com esse texto |
| `!$` | Usa o último argumento do comando anterior |
| `!*` | Usa todos os argumentos do comando anterior |
| `history` | Lista o histórico |
| `history N` | Lista os últimos N comandos |
| `history -c` | Limpa o histórico da sessão |

```bash
Ctrl + R  →  (reverse-search): apt
# encontra o último comando que contém "apt"

!!                   # repete o último comando
sudo !!              # repete o último com sudo
cd !$                # usa o último argumento do comando anterior
history 20           # últimos 20 comandos
```

---

### Controle do terminal

| Atalho | Ação |
| ------ | ---- |
| `Ctrl + L` | Limpa a tela (equivale ao `clear`) |
| `Ctrl + S` | Pausa a saída do terminal |
| `Ctrl + Q` | Retoma a saída do terminal |
| `Tab` | Autocompletar comando ou caminho |
| `Tab Tab` | Lista todas as opções disponíveis |

---

## 🚀 Produtividade com Aliases

Aliases são atalhos para comandos longos. Defina no `~/.bashrc` ou `~/.zshrc`:

```bash
# Atalhos de navegação
alias ..='cd ..'
alias ...='cd ../..'
alias ~='cd ~'

# Listagem
alias ll='ls -lah'
alias la='ls -A'
alias l='ls -CF'

# Segurança
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Atualização
alias update='sudo apt update && sudo apt upgrade -y'
alias install='sudo apt install'

# Git
alias gs='git status'
alias ga='git add .'
alias gc='git commit -m'
alias gp='git push'

# Rede
alias myip='hostname -I | awk "{print \$1}"'
alias ports='ss -tulnp'

# Utilitários
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias cls='clear'
```

Após editar, aplique com:

```bash
source ~/.bashrc
```

---

## 🧮 Variáveis de Ambiente

| Comando | Descrição |
| ------- | --------- |
| `echo $VARIAVEL` | Exibe o valor de uma variável |
| `export NOME=valor` | Define uma variável de ambiente |
| `env` | Lista todas as variáveis de ambiente |
| `printenv <VAR>` | Exibe uma variável específica |
| `unset <VAR>` | Remove uma variável |

```bash
echo $HOME           # /home/joao
echo $PATH           # caminhos de busca de executáveis
echo $USER           # usuário atual
export EDITOR=vim    # define o editor padrão
```

**Variáveis importantes:**

| Variável | O que contém |
| -------- | ------------ |
| `$HOME` | Diretório home do usuário |
| `$USER` | Nome do usuário atual |
| `$PATH` | Caminhos onde o sistema busca executáveis |
| `$SHELL` | Shell em uso (`/bin/bash`, `/bin/zsh`) |
| `$PWD` | Diretório atual |
| `$OLDPWD` | Diretório anterior |
| `$EDITOR` | Editor de texto padrão |

---

## 📟 Multiplexador de Terminal — tmux

O `tmux` permite dividir o terminal e manter sessões ativas mesmo após desconexão.

```bash
sudo apt install tmux
tmux                  # inicia uma sessão
```

**Atalhos do tmux** (prefixo padrão: `Ctrl + B`):

| Atalho | Ação |
| ------ | ---- |
| `Ctrl+B c` | Cria uma nova janela |
| `Ctrl+B n` | Próxima janela |
| `Ctrl+B p` | Janela anterior |
| `Ctrl+B "` | Divide o painel horizontalmente |
| `Ctrl+B %` | Divide o painel verticalmente |
| `Ctrl+B ↑↓←→` | Navega entre painéis |
| `Ctrl+B d` | Desacopla da sessão (ela continua rodando) |
| `Ctrl+B x` | Fecha o painel atual |
| `tmux attach` | Reconecta à sessão existente |
| `tmux ls` | Lista sessões ativas |
| `tmux new -s nome` | Cria sessão com nome |
| `tmux attach -t nome` | Reconecta a sessão pelo nome |

---

## 🐚 Pipes e Redirecionamento

| Operador | Descrição |
| -------- | --------- |
| `\|` | Redireciona a saída de um comando para outro |
| `>` | Redireciona saída para arquivo (sobrescreve) |
| `>>` | Redireciona saída para arquivo (acrescenta) |
| `<` | Usa arquivo como entrada |
| `2>` | Redireciona erros para arquivo |
| `2>&1` | Redireciona erros para o mesmo lugar que a saída |
| `&>` | Redireciona saída e erros juntos |
| `tee` | Exibe no terminal e salva em arquivo ao mesmo tempo |

```bash
ls -la | grep ".sh"                    # filtra resultados
cat /etc/passwd | cut -d: -f1 | sort   # lista usuários ordenados
comando 2>/dev/null                    # descarta erros
comando | tee saida.txt                # exibe e salva ao mesmo tempo
```

---

## 🔧 Personalização do Shell

### Mudando o prompt (PS1)

Adicione ao `~/.bashrc`:

```bash
# Prompt com usuário, host e diretório coloridos
PS1='\[\e[32m\]\u@\h\[\e[0m\]:\[\e[34m\]\w\[\e[0m\]\$ '
```

### Instalando o Zsh + Oh My Zsh (popular)

```bash
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

O Oh My Zsh traz autocompletar avançado, temas e plugins que tornam o terminal muito mais agradável.

---

## ⚠️ Boas Práticas

- Use `Ctrl + R` para buscar comandos antigos em vez de digitar tudo novamente
- Configure seus aliases no `.bashrc` logo de início — economiza muito tempo
- Use `tmux` ao trabalhar em servidores remotos para não perder progresso
- Evite aliases que sobrescrevem comandos nativos sem a flag de segurança (ex: `alias rm='rm -i'`)
- Teste comandos novos em uma pasta temporária antes de aplicar em produção
- Use `Tab` sempre — reduz erros de digitação e é mais rápido
