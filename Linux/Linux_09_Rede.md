# 🌐 Linux — Rede

Este guia cobre os principais comandos para configurar, diagnosticar e usar a rede no Linux.

---

## 📡 Informações de Rede

| Comando | Descrição |
| ------- | --------- |
| `ip a` | Lista interfaces de rede e endereços IP |
| `ip addr show` | Idem, mais detalhado |
| `ip a show eth0` | IP de uma interface específica |
| `hostname -I` | Exibe apenas o IP da máquina |
| `ifconfig` | Exibe config de rede (legado, instale com `net-tools`) |
| `ip link show` | Lista interfaces e seus estados |
| `ip route` | Exibe tabela de rotas |
| `ip route show default` | Exibe o gateway padrão |
| `cat /etc/resolv.conf` | Exibe os servidores DNS configurados |
| `nmcli` | Gerencia conexões via NetworkManager |
| `nmcli device status` | Status das interfaces de rede |

```bash
ip a
ip route show default     # qual é o gateway (roteador)
nmcli device status       # mostra conexões Wi-Fi e cabeadas
```

---

## 🔌 Testando Conectividade

| Comando | Descrição |
| ------- | --------- |
| `ping <host>` | Testa conectividade (Ctrl+C para parar) |
| `ping -c 4 <host>` | Envia exatamente 4 pacotes |
| `ping -i 2 <host>` | Intervalo de 2 segundos entre pacotes |
| `traceroute <host>` | Exibe o caminho até o destino |
| `tracepath <host>` | Alternativa ao traceroute sem sudo |
| `mtr <host>` | Combinação de ping + traceroute em tempo real |
| `nslookup <dominio>` | Resolve nome de domínio para IP |
| `dig <dominio>` | Consulta DNS detalhada |
| `dig +short <dominio>` | Apenas o IP |
| `host <dominio>` | Resolve domínio para IP (simples) |

```bash
ping -c 4 google.com
traceroute google.com
dig google.com
nslookup github.com
mtr google.com             # instale com: sudo apt install mtr
```

---

## 🌍 Download e Requisições HTTP

| Comando | Descrição |
| ------- | --------- |
| `curl <url>` | Faz requisição HTTP e exibe a resposta |
| `curl -o <arquivo> <url>` | Baixa para um arquivo |
| `curl -O <url>` | Baixa com o nome original do arquivo |
| `curl -L <url>` | Segue redirecionamentos |
| `curl -I <url>` | Exibe apenas os headers da resposta |
| `curl -X POST <url>` | Envia requisição POST |
| `curl -d "dados" <url>` | Envia dados no corpo da requisição |
| `curl -H "Header: valor" <url>` | Adiciona header à requisição |
| `curl -u usuario:senha <url>` | Autenticação básica |
| `wget <url>` | Baixa um arquivo |
| `wget -O <nome> <url>` | Baixa com nome personalizado |
| `wget -c <url>` | Retoma download interrompido |
| `wget -r <url>` | Download recursivo de um site |
| `wget -q <url>` | Download silencioso (sem saída) |

```bash
curl https://api.github.com/users/torvalds
curl -O https://example.com/arquivo.zip
wget -c https://ubuntu.com/ubuntu-24.04.iso    # retoma download pausado
curl -X POST -H "Content-Type: application/json" -d '{"nome":"joao"}' https://api.exemplo.com/users
```

---

## 🔐 SSH — Acesso Remoto Seguro

| Comando | Descrição |
| ------- | --------- |
| `ssh <usuario>@<host>` | Conecta ao servidor remoto |
| `ssh -p 2222 <usuario>@<host>` | Conecta em porta personalizada |
| `ssh -i <chave.pem> <usuario>@<host>` | Conecta com chave privada |
| `exit` | Encerra a sessão SSH |
| `ssh-keygen -t ed25519` | Gera par de chaves SSH |
| `ssh-copy-id <usuario>@<host>` | Copia chave pública para o servidor |
| `cat ~/.ssh/id_ed25519.pub` | Exibe a chave pública |

```bash
ssh joao@192.168.1.100
ssh -i ~/.ssh/minha-chave.pem ubuntu@54.123.45.67
ssh-keygen -t ed25519 -C "meu-email@email.com"
ssh-copy-id joao@servidor.com
```

**Arquivo de config SSH** (`~/.ssh/config`):

```
Host meu-servidor
    HostName 192.168.1.100
    User joao
    IdentityFile ~/.ssh/id_ed25519
    Port 22
```

Depois de configurado, basta:

```bash
ssh meu-servidor
```

---

## 📁 Transferência de Arquivos Remota

| Comando | Descrição |
| ------- | --------- |
| `scp <arquivo> <user>@<host>:<destino>` | Copia arquivo para servidor remoto |
| `scp <user>@<host>:<arquivo> <destino>` | Copia arquivo do servidor para local |
| `scp -r <pasta> <user>@<host>:<destino>` | Copia pasta recursivamente |
| `scp -P 2222 <arquivo> <user>@<host>:<dest>` | Usa porta personalizada |
| `rsync -avz <origem> <user>@<host>:<dest>` | Sincroniza com eficiência |
| `rsync -avz --progress <origem> <dest>` | Exibe progresso |
| `rsync --delete <origem> <dest>` | Remove no destino o que não existe na origem |

```bash
scp relatorio.pdf joao@servidor.com:/home/joao/
scp -r projetos/ joao@servidor.com:/var/www/
rsync -avz --progress ~/documentos/ joao@servidor.com:/backup/documentos/
```

---

## 🔍 Portas e Conexões

| Comando | Descrição |
| ------- | --------- |
| `ss -tuln` | Lista portas TCP/UDP em uso |
| `ss -tulnp` | Inclui o processo que usa cada porta |
| `netstat -tuln` | Idem (legado, requer `net-tools`) |
| `lsof -i :<porta>` | Mostra qual processo usa a porta |
| `lsof -i :80` | Mostra o que usa a porta 80 |
| `nmap <host>` | Scan de portas abertas |
| `nmap -p 80,443 <host>` | Escaneia apenas as portas especificadas |
| `nmap -sV <host>` | Detecta serviços e versões |

```bash
ss -tulnp                      # quais portas estão abertas e por quem
sudo lsof -i :3000             # o que está rodando na porta 3000
nmap 192.168.1.100             # portas abertas no servidor
```

---

## 🔥 Firewall com ufw (Ubuntu)

| Comando | Descrição |
| ------- | --------- |
| `sudo ufw status` | Exibe estado e regras do firewall |
| `sudo ufw enable` | Ativa o firewall |
| `sudo ufw disable` | Desativa o firewall |
| `sudo ufw allow 22` | Libera a porta 22 (SSH) |
| `sudo ufw allow 80/tcp` | Libera a porta 80 TCP |
| `sudo ufw deny 3306` | Bloqueia a porta 3306 (MySQL) |
| `sudo ufw allow from 192.168.1.0/24` | Libera uma faixa de IP |
| `sudo ufw delete allow 80` | Remove uma regra |
| `sudo ufw reset` | Reseta todas as regras |

```bash
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw status verbose
```

---

## ⚠️ Boas Práticas

- Sempre use SSH com chave ao invés de senha em servidores
- Mude a porta padrão do SSH (22) para dificultar ataques automatizados
- Ative e configure o `ufw` antes de expor qualquer serviço à internet
- Use `rsync` ao invés de `scp` para transferências grandes — é mais eficiente
- Monitore conexões abertas periodicamente com `ss -tulnp`
- Desative serviços de rede que não estão em uso
- Nunca exponha o banco de dados (3306, 5432) diretamente para a internet
