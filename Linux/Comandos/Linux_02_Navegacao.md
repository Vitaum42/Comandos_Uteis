# 🔍 Linux — Navegação no Sistema de Arquivos

Este guia cobre os principais comandos para navegar e entender a estrutura de diretórios do Linux.

---

## 🗂️ Estrutura de Diretórios do Linux

Diferente do Windows (que usa `C:\`, `D:\`), o Linux possui uma estrutura única em árvore partindo da raiz `/`:

| Diretório | O que contém |
| --------- | ------------ |
| `/` | Raiz do sistema — tudo parte daqui |
| `/home` | Pastas pessoais dos usuários (`/home/seu_usuario`) |
| `/root` | Pasta do superusuário (root) |
| `/bin` | Comandos essenciais do sistema (`ls`, `cp`, `mv`...) |
| `/sbin` | Comandos administrativos do sistema |
| `/etc` | Arquivos de configuração do sistema |
| `/var` | Dados variáveis: logs, cache, filas de impressão |
| `/tmp` | Arquivos temporários (apagados ao reiniciar) |
| `/usr` | Programas e bibliotecas instalados pelo usuário |
| `/opt` | Softwares de terceiros instalados manualmente |
| `/dev` | Dispositivos de hardware (HD, USB, etc.) |
| `/proc` | Informações de processos e do kernel em tempo real |
| `/mnt` e `/media` | Pontos de montagem (HDs externos, pendrives) |
| `/boot` | Arquivos de inicialização do sistema e kernel |

---

## 📌 Caminhos: Absoluto vs Relativo

| Tipo | Exemplo | Descrição |
| ---- | ------- | --------- |
| **Absoluto** | `/home/joao/documentos` | Caminho completo a partir da raiz `/` |
| **Relativo** | `documentos/projetos` | Caminho a partir do diretório atual |
| **Home** | `~/documentos` | `~` é um atalho para `/home/seu_usuario` |

---

## 🧭 Comandos de Navegação

### Saber onde você está

| Comando | Descrição |
| ------- | --------- |
| `pwd` | Exibe o caminho completo do diretório atual |

```bash
$ pwd
/home/joao/documentos
```

---

### Listar arquivos e pastas

| Comando | Descrição |
| ------- | --------- |
| `ls` | Lista arquivos e pastas do diretório atual |
| `ls <caminho>` | Lista arquivos de um diretório específico |
| `ls -l` | Lista com detalhes (permissões, tamanho, data) |
| `ls -a` | Mostra arquivos ocultos (começam com `.`) |
| `ls -la` | Detalhes + arquivos ocultos |
| `ls -lh` | Tamanhos em formato legível (KB, MB, GB) |
| `ls -lt` | Ordenado por data de modificação |
| `ls -R` | Lista recursivamente subpastas |

```bash
$ ls -lh
drwxr-xr-x 2 joao joao 4,0K mai 20 10:30 documentos
-rw-r--r-- 1 joao joao  12K mai 19 09:15 relatorio.pdf
```

> 💡 A primeira coluna indica o tipo: `d` = pasta, `-` = arquivo, `l` = link simbólico.

---

### Entrar e sair de pastas

| Comando | Descrição |
| ------- | --------- |
| `cd <pasta>` | Entra em uma pasta |
| `cd ..` | Volta uma pasta (nível acima) |
| `cd ../..` | Volta dois níveis acima |
| `cd ~` | Vai direto para o home do usuário |
| `cd /` | Vai para a raiz do sistema |
| `cd -` | Volta para o último diretório visitado |
| `cd` | Sem argumento: vai para o home |

```bash
cd /var/log       # vai para /var/log
cd ..             # volta para /var
cd ~/documentos   # vai para /home/usuario/documentos
cd -              # volta para o diretório anterior
```

---

## 🌳 Visualizar Estrutura em Árvore

| Comando | Descrição |
| ------- | --------- |
| `tree` | Exibe estrutura em árvore do diretório atual |
| `tree <caminho>` | Estrutura de um diretório específico |
| `tree -L 2` | Limita a profundidade a 2 níveis |
| `tree -a` | Inclui arquivos ocultos |
| `tree -d` | Mostra apenas diretórios |

```bash
$ tree -L 2
.
├── documentos
│   ├── relatorio.pdf
│   └── projetos
├── downloads
└── imagens
```

> 💡 Instale com `sudo apt install tree` caso não esteja disponível.

---

## 📊 Informações sobre Disco e Espaço

| Comando | Descrição |
| ------- | --------- |
| `df -h` | Exibe uso de disco de todas as partições |
| `df -h /home` | Exibe uso de disco de uma partição específica |
| `du -sh <pasta>` | Tamanho total de uma pasta |
| `du -sh *` | Tamanho de cada item no diretório atual |
| `du -ah <pasta>` | Tamanho de cada arquivo/pasta recursivamente |
| `du -sh * \| sort -h` | Ordena pastas por tamanho |

```bash
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   18G   30G  38% /
/dev/sda2       200G   80G  110G  42% /home
```

---

## 🔗 Links Simbólicos (Atalhos)

| Comando | Descrição |
| ------- | --------- |
| `ln -s <origem> <destino>` | Cria um link simbólico (atalho) |
| `ls -l` | Mostra para onde o link aponta |
| `readlink <link>` | Exibe o destino real do link |
| `unlink <link>` | Remove o link simbólico |

```bash
ln -s /var/log/syslog ~/meu-log   # cria atalho para o log do sistema
ls -l ~/meu-log                   # meu-log -> /var/log/syslog
```

---

## ⚠️ Boas Práticas de Navegação

- Use `Tab` para autocompletar caminhos e evitar erros de digitação
- Prefira caminhos absolutos em scripts para evitar ambiguidade
- Evite criar arquivos com espaços no nome; prefira `_` ou `-`
- Arquivos começando com `.` são ocultos — use `ls -a` para vê-los
- Não mexa em `/etc`, `/boot` ou `/sys` sem saber exatamente o que está fazendo
- Use `cd -` para alternar rapidamente entre dois diretórios
