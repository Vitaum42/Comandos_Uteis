# 👤 Linux — Usuários e Permissões

Este guia cobre o sistema de usuários, grupos e permissões de arquivos no Linux.

---

## 👥 Entendendo Usuários no Linux

O Linux é um sistema multiusuário. Existem três tipos de usuários:

| Tipo | Descrição |
| ---- | --------- |
| **root** | Superusuário com acesso total ao sistema |
| **usuário comum** | Usuário padrão com acesso limitado |
| **usuário de serviço** | Criado automaticamente por programas (nginx, postgres, etc.) |

---

## 🔍 Informações sobre Usuários

| Comando | Descrição |
| ------- | --------- |
| `whoami` | Exibe o nome do usuário atual |
| `id` | UID, GID e grupos do usuário atual |
| `id <usuario>` | UID, GID e grupos de outro usuário |
| `who` | Lista usuários logados no sistema |
| `w` | Lista usuários logados com detalhes de atividade |
| `last` | Histórico de logins |
| `finger <usuario>` | Informações detalhadas do usuário |
| `cat /etc/passwd` | Lista todos os usuários do sistema |
| `getent passwd` | Idem, com suporte a usuários de rede |

```bash
$ id
uid=1000(joao) gid=1000(joao) grupos=1000(joao),27(sudo),4(adm)

$ cat /etc/passwd | cut -d: -f1   # lista apenas os nomes de usuário
```

---

## ➕ Criando e Gerenciando Usuários

| Comando | Descrição |
| ------- | --------- |
| `sudo adduser <nome>` | Cria usuário interativamente (recomendado) |
| `sudo useradd <nome>` | Cria usuário sem configurações extras |
| `sudo useradd -m -s /bin/bash <nome>` | Cria com home e shell definidos |
| `sudo userdel <nome>` | Remove o usuário |
| `sudo userdel -r <nome>` | Remove o usuário e sua pasta home |
| `sudo usermod -aG <grupo> <usuario>` | Adiciona usuário a um grupo |
| `sudo usermod -l <novo> <antigo>` | Renomeia o usuário |
| `passwd` | Altera a senha do usuário atual |
| `sudo passwd <usuario>` | Altera a senha de outro usuário |
| `sudo passwd -l <usuario>` | Bloqueia (desativa) um usuário |
| `sudo passwd -u <usuario>` | Desbloqueia um usuário |

```bash
sudo adduser maria
sudo usermod -aG sudo maria        # dá privilégios de sudo para "maria"
sudo userdel -r maria              # remove usuário e pasta home
```

---

## 👥 Grupos

| Comando | Descrição |
| ------- | --------- |
| `groups` | Lista grupos do usuário atual |
| `groups <usuario>` | Lista grupos de um usuário |
| `cat /etc/group` | Lista todos os grupos do sistema |
| `sudo groupadd <grupo>` | Cria um novo grupo |
| `sudo groupdel <grupo>` | Remove um grupo |
| `sudo gpasswd -a <usuario> <grupo>` | Adiciona usuário ao grupo |
| `sudo gpasswd -d <usuario> <grupo>` | Remove usuário do grupo |
| `newgrp <grupo>` | Muda o grupo ativo da sessão atual |

```bash
sudo groupadd desenvolvedores
sudo gpasswd -a joao desenvolvedores
groups joao
```

---

## 🔐 sudo — Executando como Superusuário

| Comando | Descrição |
| ------- | --------- |
| `sudo <comando>` | Executa como root (pede senha do usuário atual) |
| `sudo -i` | Abre shell interativo como root |
| `sudo -u <usuario> <comando>` | Executa como outro usuário |
| `sudo !!` | Repete o último comando com sudo |
| `su <usuario>` | Troca para outro usuário (pede a senha dele) |
| `su -` | Entra como root com ambiente completo |
| `sudo visudo` | Edita o arquivo de permissões do sudo com segurança |

```bash
sudo apt install nginx
sudo -i                  # vira root (cuidado!)
sudo !!                  # refaz o último comando com sudo
```

---

## 🔒 Permissões de Arquivos

### Entendendo as permissões

Ao rodar `ls -l`, você vê algo como:

```
-rwxr-xr-- 1 joao dev 4096 mai 20 10:30 script.sh
```

| Campo | Significado |
| ----- | ----------- |
| `-` | Tipo: `-` arquivo, `d` diretório, `l` link |
| `rwx` | Permissões do **dono** (r=leitura, w=escrita, x=execução) |
| `r-x` | Permissões do **grupo** |
| `r--` | Permissões dos **outros** |
| `joao` | Dono do arquivo |
| `dev` | Grupo do arquivo |

---

### Valores numéricos (octal)

| Número | Permissão | Significado |
| ------ | --------- | ----------- |
| `7` | `rwx` | Leitura + Escrita + Execução |
| `6` | `rw-` | Leitura + Escrita |
| `5` | `r-x` | Leitura + Execução |
| `4` | `r--` | Somente Leitura |
| `0` | `---` | Nenhuma permissão |

---

### Alterando permissões com `chmod`

| Comando | Descrição |
| ------- | --------- |
| `chmod 755 <arquivo>` | Dono: rwx / Grupo e Outros: r-x |
| `chmod 644 <arquivo>` | Dono: rw- / Grupo e Outros: r-- |
| `chmod 600 <arquivo>` | Dono: rw- / Grupo e Outros: nada |
| `chmod +x <arquivo>` | Adiciona permissão de execução para todos |
| `chmod -x <arquivo>` | Remove permissão de execução |
| `chmod u+w <arquivo>` | Adiciona escrita para o dono (u=user) |
| `chmod g-w <arquivo>` | Remove escrita do grupo (g=group) |
| `chmod o-r <arquivo>` | Remove leitura dos outros (o=others) |
| `chmod -R 755 <pasta>` | Aplica recursivamente em toda a pasta |

```bash
chmod 755 deploy.sh           # torna o script executável
chmod 600 ~/.ssh/id_rsa       # protege chave SSH
chmod -R 644 ~/documentos/    # somente leitura para todos os arquivos
chmod +x *.sh                 # torna todos os .sh executáveis
```

**Permissões mais comuns:**

| Código | Uso típico |
| ------ | ---------- |
| `755` | Scripts e executáveis |
| `644` | Arquivos de configuração e documentos |
| `600` | Chaves privadas e arquivos sensíveis |
| `777` | ⚠️ Todos podem fazer tudo (evite!) |
| `700` | Só o dono acessa (pasta pessoal) |

---

### Alterando dono e grupo com `chown` e `chgrp`

| Comando | Descrição |
| ------- | --------- |
| `sudo chown <usuario> <arquivo>` | Muda o dono |
| `sudo chown <usuario>:<grupo> <arq>` | Muda dono e grupo |
| `sudo chown -R <usuario>:<grupo> <pasta>` | Muda recursivamente |
| `sudo chgrp <grupo> <arquivo>` | Muda apenas o grupo |

```bash
sudo chown joao arquivo.txt
sudo chown joao:dev projeto/
sudo chown -R www-data:www-data /var/www/html/
```

---

## 🔑 Permissões Especiais

| Permissão | Valor | Descrição |
| --------- | ----- | --------- |
| **SUID** | `4755` | Executa com permissões do **dono**, não do executante |
| **SGID** | `2755` | Executa com permissões do **grupo** |
| **Sticky bit** | `1777` | Só o dono pode deletar arquivos (usado em `/tmp`) |

```bash
chmod 4755 programa         # seta SUID
chmod 1777 /pasta/publica   # seta sticky bit
ls -l /tmp                  # drwxrwxrwt (o 't' indica sticky bit)
```

---

## ⚠️ Boas Práticas

- Nunca use `chmod 777` em produção — dá acesso total a qualquer usuário
- Use `sudo` ao invés de logar como root diretamente
- Arquivos de configuração sensíveis devem ter permissão `600` ou `640`
- Adicione usuários a grupos específicos em vez de dar sudo para tudo
- Revise permissões periodicamente com `find / -perm 777 -type f`
- Proteja chaves SSH com `chmod 600 ~/.ssh/id_rsa`
