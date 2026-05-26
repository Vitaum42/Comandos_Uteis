# 🗜️ Linux — Compactação e Arquivamento

Este guia cobre como compactar, descompactar e gerenciar arquivos comprimidos no Linux.

---

## 📦 tar — O Formato Mais Comum no Linux

O `tar` empacota arquivos (e opcionalmente comprime). É o formato padrão no Linux.

### Compactando com tar

| Comando | Descrição |
| ------- | --------- |
| `tar -czf <saida.tar.gz> <pasta>` | Compacta com gzip (mais comum) |
| `tar -cjf <saida.tar.bz2> <pasta>` | Compacta com bzip2 (menor, mais lento) |
| `tar -cJf <saida.tar.xz> <pasta>` | Compacta com xz (menor ainda) |
| `tar -cf <saida.tar> <pasta>` | Apenas empacota, sem compressão |
| `tar -czf <saida.tar.gz> arq1 arq2` | Compacta múltiplos arquivos |
| `tar -czf <saida.tar.gz> -C <pasta> .` | Compacta sem incluir o caminho completo |
| `tar -czf <saida.tar.gz> --exclude="*.log" <pasta>` | Exclui arquivos .log |

```bash
tar -czf backup.tar.gz ~/documentos/
tar -czf projeto.tar.gz src/ tests/ README.md
tar -czf logs.tar.gz --exclude="*.tmp" /var/log/
```

---

### Listando conteúdo sem descompactar

| Comando | Descrição |
| ------- | --------- |
| `tar -tzf <arquivo.tar.gz>` | Lista conteúdo de um .tar.gz |
| `tar -tjf <arquivo.tar.bz2>` | Lista conteúdo de um .tar.bz2 |
| `tar -tf <arquivo.tar>` | Lista conteúdo de um .tar |

```bash
tar -tzf backup.tar.gz | head -20    # lista os primeiros 20 arquivos
```

---

### Descompactando tar

| Comando | Descrição |
| ------- | --------- |
| `tar -xzf <arquivo.tar.gz>` | Descompacta .tar.gz no diretório atual |
| `tar -xjf <arquivo.tar.bz2>` | Descompacta .tar.bz2 |
| `tar -xJf <arquivo.tar.xz>` | Descompacta .tar.xz |
| `tar -xf <arquivo.tar>` | Desempacota .tar |
| `tar -xzf <arquivo.tar.gz> -C <pasta>` | Descompacta em pasta específica |
| `tar -xzf <arquivo.tar.gz> <arquivo>` | Extrai apenas um arquivo específico |

```bash
tar -xzf backup.tar.gz
tar -xzf backup.tar.gz -C /tmp/restauracao/
tar -xzf projeto.tar.gz src/config.json    # extrai só um arquivo
```

---

### Memorize as flags do tar

| Flag | Significado |
| ---- | ----------- |
| `-c` | **C**ria um arquivo |
| `-x` | E**x**trai |
| `-t` | Lis**t**a o conteúdo |
| `-f` | Especifica o nome do **f**icheiro |
| `-z` | Usa compressão g**z**ip |
| `-j` | Usa compressão b**j**ip2 |
| `-J` | Usa compressão x**z** |
| `-v` | Modo **v**erboso (mostra arquivos) |
| `-C` | Define o diretório de destino |

---

## 📁 zip e unzip

Formato popular e compatível com Windows.

| Comando | Descrição |
| ------- | --------- |
| `zip <saida.zip> <arquivo>` | Compacta um arquivo |
| `zip -r <saida.zip> <pasta>` | Compacta uma pasta recursivamente |
| `zip -r <saida.zip> <pasta> -x "*.log"` | Exclui arquivos .log |
| `zip -9 <saida.zip> <pasta>` | Máxima compressão |
| `zip -e <saida.zip> <pasta>` | Compacta com senha |
| `unzip <arquivo.zip>` | Descompacta no diretório atual |
| `unzip <arquivo.zip> -d <pasta>` | Descompacta em pasta específica |
| `unzip -l <arquivo.zip>` | Lista conteúdo sem descompactar |
| `unzip -o <arquivo.zip>` | Sobrescreve sem perguntar |

```bash
zip -r backup.zip ~/documentos/
zip -r9 projeto.zip src/ tests/ -x "*.pyc"
unzip backup.zip -d ~/restauracao/
unzip -l pacote.zip            # só ver o conteúdo
```

> 💡 Instale com: `sudo apt install zip unzip`

---

## 🗃️ gzip, bzip2, xz — Compressão Simples

Esses compressores atuam em um **único arquivo** (não em pastas):

| Comando | Descrição |
| ------- | --------- |
| `gzip <arquivo>` | Comprime e substitui pelo .gz |
| `gzip -k <arquivo>` | Comprime mantendo o original |
| `gzip -d <arquivo.gz>` | Descomprime |
| `gunzip <arquivo.gz>` | Alias para descomprimir |
| `bzip2 <arquivo>` | Comprime com bzip2 |
| `bzip2 -d <arquivo.bz2>` | Descomprime bzip2 |
| `xz <arquivo>` | Comprime com xz (maior compressão) |
| `xz -d <arquivo.xz>` | Descomprime xz |

```bash
gzip -k banco_de_dados.sql          # gera banco_de_dados.sql.gz
gunzip banco_de_dados.sql.gz
xz -k arquivo_grande.log            # compressão máxima
```

---

## 📊 Comparando Formatos de Compressão

| Formato | Extensão | Velocidade | Compressão | Compatibilidade |
| ------- | -------- | ---------- | ---------- | --------------- |
| gzip | `.tar.gz` | ⚡⚡⚡ Rápido | ⭐⭐ Boa | ✅ Universal |
| bzip2 | `.tar.bz2` | ⚡⚡ Médio | ⭐⭐⭐ Ótima | ✅ Universal |
| xz | `.tar.xz` | ⚡ Lento | ⭐⭐⭐⭐ Excelente | ✅ Boa |
| zip | `.zip` | ⚡⚡⚡ Rápido | ⭐⭐ Boa | ✅ Windows/Linux/Mac |
| 7z | `.7z` | ⚡ Variável | ⭐⭐⭐⭐ Excelente | ⚠️ Requer p7zip |

> 💡 **Para uso geral:** `.tar.gz` — rápido e amplamente suportado.
> **Para máxima compressão:** `.tar.xz`.
> **Para compatibilidade com Windows:** `.zip`.

---

## 📦 7-Zip no Linux

| Comando | Descrição |
| ------- | --------- |
| `7z a <saida.7z> <pasta>` | Compacta em 7z |
| `7z e <arquivo.7z>` | Extrai no diretório atual |
| `7z x <arquivo.7z>` | Extrai preservando a estrutura de pastas |
| `7z x <arquivo.7z> -o<pasta>` | Extrai em pasta específica |
| `7z l <arquivo.7z>` | Lista o conteúdo |

```bash
sudo apt install p7zip-full
7z a backup.7z ~/documentos/
7z x backup.7z -o/tmp/restauracao
```

---

## ⚠️ Boas Práticas

- Use `tar -tzf` para conferir o conteúdo antes de descompactar
- Prefira `.tar.gz` para backups — boa compressão e alta compatibilidade
- Use `.zip` quando precisar compartilhar com usuários Windows
- Sempre especifique `-C <pasta>` ao descompactar para não bagunçar o diretório atual
- Para arquivos muito grandes, considere `.tar.xz` — a compressão extra compensa no armazenamento
- Ao fazer backup de bancos de dados, comprima o dump: `pg_dump banco | gzip > banco.sql.gz`
