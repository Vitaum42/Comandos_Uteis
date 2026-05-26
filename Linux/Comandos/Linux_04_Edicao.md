# 📄 Linux — Leitura e Edição de Arquivos

Este guia cobre como visualizar, criar e editar arquivos diretamente no terminal do Linux.

---

## 👁️ Visualizando Conteúdo de Arquivos

### Exibir o arquivo inteiro

| Comando | Descrição |
| ------- | --------- |
| `cat <arquivo>` | Exibe o conteúdo completo |
| `cat -n <arquivo>` | Exibe com número de linhas |
| `cat -A <arquivo>` | Exibe caracteres especiais (tabs, fim de linha) |
| `cat arq1 arq2` | Concatena e exibe dois arquivos |
| `cat arq1 arq2 > arq3` | Une dois arquivos em um terceiro |

```bash
cat /etc/hosts
cat -n script.py
cat cabecalho.txt corpo.txt > completo.txt
```

---

### Exibir com paginação

| Comando | Descrição |
| ------- | --------- |
| `less <arquivo>` | Exibe com paginação interativa (recomendado) |
| `more <arquivo>` | Paginação simples (só avança) |

**Controles do `less`:**

| Tecla | Ação |
| ----- | ---- |
| `Space` / `PgDn` | Avança uma página |
| `b` / `PgUp` | Volta uma página |
| `↑` / `↓` | Avança/volta uma linha |
| `/texto` | Busca "texto" no arquivo |
| `n` | Próxima ocorrência da busca |
| `N` | Ocorrência anterior |
| `g` | Vai para o início |
| `G` | Vai para o final |
| `q` | Sai do `less` |

```bash
less /var/log/syslog
```

---

### Exibir início e fim do arquivo

| Comando | Descrição |
| ------- | --------- |
| `head <arquivo>` | Exibe as primeiras 10 linhas |
| `head -n 20 <arquivo>` | Exibe as primeiras N linhas |
| `tail <arquivo>` | Exibe as últimas 10 linhas |
| `tail -n 30 <arquivo>` | Exibe as últimas N linhas |
| `tail -f <arquivo>` | Monitora o arquivo em tempo real (logs) |
| `tail -f -n 50 <arq>` | Últimas 50 linhas + monitoramento |

```bash
head -n 5 /etc/passwd
tail -f /var/log/syslog       # monitorar log ao vivo (Ctrl+C para sair)
```

---

## ✍️ Escrevendo em Arquivos pelo Terminal

### Redirecionamento de saída

| Comando | Descrição |
| ------- | --------- |
| `echo "texto" > arquivo` | Escreve (sobrescreve o conteúdo existente) |
| `echo "texto" >> arquivo` | Acrescenta ao final do arquivo |
| `comando > arquivo` | Redireciona saída de um comando para arquivo |
| `comando >> arquivo` | Acrescenta saída de um comando ao arquivo |
| `comando 2> erros.txt` | Redireciona apenas erros para um arquivo |
| `comando > saida.txt 2>&1` | Redireciona saída e erros para o mesmo arquivo |

```bash
echo "Olá, mundo!" > saudacao.txt
echo "Segunda linha" >> saudacao.txt
ls -la > listagem.txt
python3 script.py > saida.txt 2>&1
```

---

## ✏️ Editores de Texto no Terminal

### nano — Simples e ideal para iniciantes

```bash
nano <arquivo>
```

**Atalhos do nano:**

| Atalho | Ação |
| ------ | ---- |
| `Ctrl + O` | Salvar o arquivo |
| `Ctrl + X` | Sair (pergunta se quer salvar) |
| `Ctrl + K` | Recortar linha |
| `Ctrl + U` | Colar linha |
| `Ctrl + W` | Buscar texto |
| `Ctrl + \` | Buscar e substituir |
| `Ctrl + G` | Exibir ajuda |
| `Alt + U` | Desfazer |
| `Ctrl + C` | Exibir linha/coluna atual |

---

### vim — Poderoso e presente em todo servidor Linux

```bash
vim <arquivo>
```

O Vim possui **modos** de operação:

| Modo | Como entrar | O que faz |
| ---- | ----------- | --------- |
| **Normal** | `Esc` | Navegação e comandos (modo padrão) |
| **Inserção** | `i`, `a`, `o` | Digitar e editar texto |
| **Visual** | `v` | Selecionar texto |
| **Comando** | `:` | Executar comandos (salvar, sair, etc.) |

**Comandos essenciais do Vim:**

| Comando | Ação |
| ------- | ---- |
| `i` | Entra no modo inserção antes do cursor |
| `a` | Entra no modo inserção após o cursor |
| `o` | Insere nova linha abaixo e entra em inserção |
| `Esc` | Volta ao modo normal |
| `:w` | Salva o arquivo |
| `:q` | Sai do Vim |
| `:wq` | Salva e sai |
| `:q!` | Sai sem salvar (força) |
| `dd` | Apaga a linha atual |
| `yy` | Copia a linha atual |
| `p` | Cola após o cursor |
| `u` | Desfaz última ação |
| `Ctrl + r` | Refaz ação desfeita |
| `/texto` | Busca "texto" no arquivo |
| `n` | Próxima ocorrência |
| `:%s/old/new/g` | Substitui "old" por "new" em todo arquivo |
| `gg` | Vai para o início do arquivo |
| `G` | Vai para o final do arquivo |
| `:set number` | Exibe número de linhas |

> 💡 **Dica de sobrevivência no Vim:** Se estiver preso, pressione `Esc` várias vezes e depois `:q!` para sair sem salvar.

---

### gedit / kate / mousepad — Editores com interface gráfica

```bash
gedit <arquivo>       # GNOME
kate <arquivo>        # KDE
mousepad <arquivo>    # XFCE
```

> 💡 Úteis para editar arquivos de configuração com conforto visual.

---

## 🔄 Comparando Arquivos

| Comando | Descrição |
| ------- | --------- |
| `diff <arq1> <arq2>` | Mostra diferenças entre dois arquivos |
| `diff -u <arq1> <arq2>` | Formato unificado (mais legível) |
| `diff -y <arq1> <arq2>` | Exibe lado a lado |
| `cmp <arq1> <arq2>` | Compara byte a byte |

```bash
diff config_antiga.txt config_nova.txt
diff -u v1.py v2.py
```

---

## 🛠️ Manipulação Avançada de Texto

| Comando | Descrição |
| ------- | --------- |
| `sort <arquivo>` | Ordena linhas alfabeticamente |
| `sort -r <arquivo>` | Ordena em ordem inversa |
| `sort -n <arquivo>` | Ordena numericamente |
| `uniq <arquivo>` | Remove linhas duplicadas consecutivas |
| `sort arq \| uniq` | Remove todas as duplicatas |
| `cut -d: -f1 <arq>` | Extrai a 1ª coluna usando `:` como separador |
| `cut -c1-10 <arq>` | Extrai os primeiros 10 caracteres de cada linha |
| `tr 'a-z' 'A-Z'` | Converte minúsculas em maiúsculas |
| `sed 's/old/new/g' arq` | Substitui texto sem editar o arquivo |
| `sed -i 's/old/new/g' arq` | Substitui e salva no próprio arquivo |
| `awk '{print $1}' arq` | Exibe a primeira coluna de cada linha |

```bash
sort nomes.txt
sort -n numeros.txt | uniq
cut -d: -f1 /etc/passwd           # lista todos os usuários do sistema
sed 's/erro/ERRO/g' log.txt       # substitui "erro" por "ERRO"
awk '{print $1, $3}' dados.txt    # exibe 1ª e 3ª colunas
```

---

## ⚠️ Boas Práticas

- Prefira `less` ao invés de `cat` para arquivos grandes
- Use `nano` para edições rápidas e `vim` para edições avançadas no servidor
- Faça backup antes de editar arquivos de configuração do sistema
- Ao usar `sed -i`, teste primeiro sem o `-i` para ver o resultado antes de salvar
- Use `tail -f` para monitorar logs de aplicações em tempo real
- Evite `>` quando quiser apenas acrescentar — use `>>` para não perder dados existentes
