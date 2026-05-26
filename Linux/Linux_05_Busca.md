# 🔎 Linux — Busca e Filtros

Este guia cobre como localizar arquivos, pastas e conteúdo de texto no Linux com eficiência.

---

## 🗂️ Buscando Arquivos com `find`

O `find` é a ferramenta mais poderosa para localizar arquivos no sistema.

### Sintaxe base

```bash
find <onde_buscar> <opções> <critério>
```

---

### Busca por nome

| Comando | Descrição |
| ------- | --------- |
| `find . -name "arquivo.txt"` | Busca pelo nome exato no diretório atual |
| `find / -name "nginx.conf"` | Busca em todo o sistema |
| `find . -name "*.log"` | Busca por extensão |
| `find . -iname "*.TXT"` | Busca sem diferenciar maiúsculas/minúsculas |
| `find . -not -name "*.log"` | Busca arquivos que **não** sejam .log |

```bash
find /etc -name "*.conf"
find ~/documentos -iname "relatorio*"
```

---

### Busca por tipo

| Comando | Descrição |
| ------- | --------- |
| `find . -type f` | Apenas arquivos |
| `find . -type d` | Apenas diretórios |
| `find . -type l` | Apenas links simbólicos |

```bash
find /var -type f -name "*.log"
find ~ -type d -name "backup"
```

---

### Busca por tamanho

| Comando | Descrição |
| ------- | --------- |
| `find . -size +100M` | Arquivos maiores que 100 MB |
| `find . -size -1k` | Arquivos menores que 1 KB |
| `find . -size 50M` | Arquivos com exatamente 50 MB |
| `find . -empty` | Arquivos e pastas vazios |

```bash
find / -size +500M               # arquivos grandes que ocupam espaço
find /tmp -empty                 # arquivos vazios em /tmp
```

---

### Busca por data de modificação

| Comando | Descrição |
| ------- | --------- |
| `find . -mtime -7` | Modificados nos últimos 7 dias |
| `find . -mtime +30` | Modificados há mais de 30 dias |
| `find . -newer arquivo.txt` | Modificados depois de arquivo.txt |
| `find . -mmin -60` | Modificados nos últimos 60 minutos |

```bash
find ~/downloads -mtime +30       # arquivos antigos para limpar
find /var/log -mtime -1           # logs gerados hoje
```

---

### Busca por permissão e dono

| Comando | Descrição |
| ------- | --------- |
| `find . -perm 755` | Arquivos com permissão exata 755 |
| `find . -perm /u+x` | Arquivos executáveis pelo dono |
| `find . -user joao` | Arquivos pertencentes ao usuário "joao" |
| `find . -group dev` | Arquivos pertencentes ao grupo "dev" |

```bash
find /home -user joao -type f
find / -perm /u+x -type f         # todos os executáveis do sistema
```

---

### Executando ações nos resultados

| Comando | Descrição |
| ------- | --------- |
| `find . -name "*.tmp" -delete` | Apaga os arquivos encontrados |
| `find . -name "*.log" -exec ls -lh {} \;` | Executa `ls` em cada resultado |
| `find . -type f -exec chmod 644 {} \;` | Aplica permissão em todos os arquivos |
| `find . -name "*.txt" \| xargs wc -l` | Conta linhas de todos os .txt |

```bash
find /tmp -type f -mtime +7 -delete       # limpa arquivos antigos de /tmp
find . -name "*.sh" -exec chmod +x {} \;  # torna todos os .sh executáveis
```

---

## 📝 Buscando Conteúdo com `grep`

O `grep` busca texto **dentro** de arquivos.

### Sintaxe base

```bash
grep "<padrão>" <arquivo>
```

---

### Opções do grep

| Comando | Descrição |
| ------- | --------- |
| `grep "texto" arquivo` | Busca "texto" no arquivo |
| `grep -i "texto" arquivo` | Sem diferenciar maiúsculas/minúsculas |
| `grep -r "texto" pasta/` | Busca recursiva em uma pasta |
| `grep -n "texto" arquivo` | Exibe o número da linha |
| `grep -c "texto" arquivo` | Conta quantas linhas contêm o texto |
| `grep -l "texto" *.py` | Lista apenas os arquivos que contêm o texto |
| `grep -v "texto" arquivo` | Exibe linhas que **não** contêm o texto |
| `grep -w "palavra" arquivo` | Busca pela palavra exata (não parte dela) |
| `grep -A 3 "texto" arquivo` | Exibe 3 linhas **após** a ocorrência |
| `grep -B 3 "texto" arquivo` | Exibe 3 linhas **antes** da ocorrência |
| `grep -C 3 "texto" arquivo` | Exibe 3 linhas antes e depois |
| `grep -E "padrão" arquivo` | Suporte a expressões regulares estendidas |
| `grep --color "texto" arquivo` | Destaca o texto encontrado em cor |

```bash
grep "erro" /var/log/syslog
grep -in "exception" *.log         # busca sem case, com número de linha
grep -r "def main" ~/projetos/     # busca função em todos os arquivos Python
grep -v "^#" /etc/ssh/sshd_config  # exclui linhas de comentário
grep -E "^[0-9]{3}-" contatos.txt  # expressão regular: linhas com DDD
```

---

### Combinando grep com outros comandos

```bash
ps aux | grep nginx               # filtra processos do nginx
cat /etc/passwd | grep "joao"     # busca usuário no arquivo de senhas
ls -la | grep "^d"                # lista apenas diretórios
history | grep "apt install"      # busca comandos de instalação no histórico
dmesg | grep -i "error"           # busca erros no log do kernel
```

---

## ⚡ Outros Comandos de Busca

### `locate` — Busca rápida por nome (usa banco de dados)

| Comando | Descrição |
| ------- | --------- |
| `locate <nome>` | Busca rápida pelo nome do arquivo |
| `locate -i <nome>` | Sem diferenciar maiúsculas/minúsculas |
| `locate -n 10 <nome>` | Limita a 10 resultados |
| `sudo updatedb` | Atualiza o banco de dados do locate |

```bash
locate nginx.conf
sudo updatedb && locate relatorio.pdf
```

> 💡 `locate` é muito mais rápido que `find`, mas pode estar desatualizado. Instale com `sudo apt install mlocate`.

---

### `which` e `whereis` — Localizar programas

| Comando | Descrição |
| ------- | --------- |
| `which <programa>` | Mostra onde o executável está instalado |
| `whereis <programa>` | Mostra binário, código-fonte e manual |
| `type <comando>` | Diz se é um alias, função ou executável |

```bash
which python3         # /usr/bin/python3
whereis nginx         # nginx: /usr/sbin/nginx /etc/nginx
type ls               # ls is aliased to 'ls --color=auto'
```

---

## ⚠️ Boas Práticas

- Use `find /` com cuidado — buscar no sistema inteiro pode ser lento
- Prefira `locate` para buscas rápidas por nome e `find` quando precisar de filtros avançados
- Teste comandos com `find ... -print` antes de usar `-delete` ou `-exec rm`
- Combine `grep` com `|` (pipe) para filtrar saídas de outros comandos
- Use `grep -r` em vez de abrir cada arquivo manualmente ao debugar código
- A flag `--color` torna o `grep` muito mais fácil de ler — adicione ao `.bashrc`: `alias grep='grep --color=auto'`
