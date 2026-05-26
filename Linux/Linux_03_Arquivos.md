# 📁 Linux — Arquivos e Pastas

Este guia cobre a criação, cópia, movimentação, renomeação e remoção de arquivos e diretórios no Linux.

---

## 📄 Criando Arquivos

| Comando | Descrição |
| ------- | --------- |
| `touch <arquivo>` | Cria um arquivo vazio |
| `touch arq1 arq2 arq3` | Cria vários arquivos de uma vez |
| `touch -t 202501011200 <arq>` | Cria com data/hora específica |
| `> <arquivo>` | Cria arquivo vazio ou limpa o conteúdo de um existente |
| `echo "texto" > <arquivo>` | Cria arquivo com conteúdo |
| `cat > <arquivo>` | Cria arquivo e digita conteúdo (Ctrl+D para salvar) |

```bash
touch notas.txt
touch arquivo1.txt arquivo2.txt arquivo3.txt
echo "Olá, Linux!" > saudacao.txt
```

---

## 📂 Criando Pastas (Diretórios)

| Comando | Descrição |
| ------- | --------- |
| `mkdir <pasta>` | Cria uma pasta |
| `mkdir pasta1 pasta2 pasta3` | Cria várias pastas de uma vez |
| `mkdir -p <a/b/c>` | Cria pastas aninhadas (inclusive as intermediárias) |
| `mkdir -v <pasta>` | Exibe o que foi criado |

```bash
mkdir projetos
mkdir -p projetos/web/frontend   # cria toda a hierarquia
mkdir src tests docs              # três pastas de uma vez
```

---

## 📋 Copiando Arquivos e Pastas

| Comando | Descrição |
| ------- | --------- |
| `cp <origem> <destino>` | Copia um arquivo |
| `cp arq1 arq2 <pasta>` | Copia múltiplos arquivos para uma pasta |
| `cp -r <pasta> <destino>` | Copia uma pasta recursivamente |
| `cp -i <origem> <destino>` | Pede confirmação antes de sobrescrever |
| `cp -u <origem> <destino>` | Copia apenas se a origem for mais nova |
| `cp -v <origem> <destino>` | Exibe o que está sendo copiado |
| `cp -p <origem> <destino>` | Preserva permissões, dono e data |
| `cp -a <pasta> <destino>` | Cópia completa preservando tudo (equivale a `-rp`) |

```bash
cp relatorio.pdf backup/
cp -r projetos/ /mnt/backup/projetos/
cp -iv notas.txt notas_backup.txt     # interativo + verboso
```

---

## 🚚 Movendo e Renomeando

> `mv` serve tanto para **mover** quanto para **renomear** — no Linux são a mesma operação.

| Comando | Descrição |
| ------- | --------- |
| `mv <origem> <destino>` | Move ou renomeia arquivo/pasta |
| `mv arq1 arq2 <pasta>` | Move múltiplos arquivos para uma pasta |
| `mv -i <origem> <destino>` | Pede confirmação antes de sobrescrever |
| `mv -u <origem> <destino>` | Move apenas se a origem for mais nova |
| `mv -v <origem> <destino>` | Exibe o que está sendo movido |

```bash
mv notas.txt anotacoes.txt          # renomear
mv anotacoes.txt ~/documentos/      # mover
mv -i *.txt documentos/             # mover todos os .txt com confirmação
```

---

## 🗑️ Removendo Arquivos e Pastas

> ⚠️ **Cuidado:** No Linux não existe "lixeira" no terminal. O que for removido com `rm` **não pode ser recuperado facilmente**.

| Comando | Descrição |
| ------- | --------- |
| `rm <arquivo>` | Remove um arquivo |
| `rm arq1 arq2` | Remove múltiplos arquivos |
| `rm *.log` | Remove todos os arquivos .log |
| `rm -i <arquivo>` | Pede confirmação antes de remover |
| `rm -r <pasta>` | Remove pasta e todo seu conteúdo |
| `rm -rf <pasta>` | ⚠️ Remove forçadamente sem confirmação |
| `rmdir <pasta>` | Remove pasta **vazia** |

```bash
rm temporario.txt
rm -i importante.txt          # pergunta antes de deletar
rm -r projeto_antigo/
rmdir pasta_vazia/
```

> 🚨 **NUNCA execute** `rm -rf /` ou `rm -rf /*` — isso apaga todo o sistema operacional!

---

## 🔍 Visualizando Informações de Arquivos

| Comando | Descrição |
| ------- | --------- |
| `file <arquivo>` | Identifica o tipo real do arquivo |
| `stat <arquivo>` | Exibe metadados completos (tamanho, datas, permissões) |
| `ls -lh <arquivo>` | Tamanho e detalhes do arquivo |
| `wc <arquivo>` | Conta linhas, palavras e bytes |
| `wc -l <arquivo>` | Conta apenas linhas |
| `wc -w <arquivo>` | Conta apenas palavras |

```bash
$ file imagem.png
imagem.png: PNG image data, 1920 x 1080

$ stat relatorio.pdf
  Arquivo: relatorio.pdf
  Tamanho: 245760    Blocos: 480    Bloco de E/S: 4096  arquivo comum
  Modificado: 2025-05-10 14:32:00.000000000

$ wc -l codigo.py
142 codigo.py
```

---

## 🔗 Links Simbólicos e Hard Links

| Comando | Descrição |
| ------- | --------- |
| `ln -s <origem> <link>` | Cria um link simbólico (atalho, como no Windows) |
| `ln <origem> <link>` | Cria um hard link (referência direta ao mesmo arquivo) |
| `ls -l` | Mostra `->` indicando links simbólicos |
| `readlink <link>` | Mostra o destino do link |
| `unlink <link>` | Remove o link sem apagar o arquivo original |

```bash
ln -s /etc/nginx/nginx.conf ~/nginx.conf   # atalho para o arquivo de config
ls -l ~/nginx.conf
# nginx.conf -> /etc/nginx/nginx.conf
```

---

## 🎯 Curingas (Wildcards)

Curingas permitem selecionar múltiplos arquivos de uma vez:

| Curinga | Significado | Exemplo |
| ------- | ----------- | ------- |
| `*` | Qualquer sequência de caracteres | `*.txt` → todos os .txt |
| `?` | Um único caractere qualquer | `arq?.txt` → arq1.txt, arqA.txt |
| `[abc]` | Um dos caracteres listados | `[abc]*.sh` → arquivos que começam com a, b ou c |
| `[0-9]` | Qualquer dígito | `log[0-9].txt` → log1.txt, log2.txt... |
| `{a,b}` | Alternativas exatas | `{jpg,png}` → jpg ou png |

```bash
rm *.tmp                  # apaga todos os .tmp
cp foto?.jpg backup/      # copia foto1.jpg, foto2.jpg, etc
ls [A-Z]*.md              # lista .md que começam com letra maiúscula
mkdir {jan,fev,mar}       # cria pastas jan, fev e mar
```

---

## ⚠️ Boas Práticas

- Sempre use `-i` ao remover arquivos importantes para confirmar antes de deletar
- Prefira `cp` antes de `mv` quando não tiver certeza do resultado
- Evite espaços em nomes de arquivos; use `_` ou `-` no lugar
- Faça backup de arquivos importantes antes de mover ou editar
- Teste curingas com `ls` antes de usar com `rm` para ver o que será afetado
- Use `trash-cli` (`sudo apt install trash-cli`) para ter uma "lixeira" no terminal: `trash <arquivo>`
