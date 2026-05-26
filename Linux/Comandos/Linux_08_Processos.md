# ⚙️ Linux — Processos e Sistema

Este guia cobre como monitorar, controlar e gerenciar processos e recursos do sistema no Linux.

---

## 🔍 Listando Processos

| Comando | Descrição |
| ------- | --------- |
| `ps` | Exibe processos da sessão atual |
| `ps aux` | Lista **todos** os processos do sistema |
| `ps aux --sort=-%cpu` | Ordena por uso de CPU |
| `ps aux --sort=-%mem` | Ordena por uso de memória |
| `ps -ef` | Formato completo com hierarquia |
| `ps -u <usuario>` | Processos de um usuário específico |
| `pgrep <nome>` | Retorna o PID de um processo pelo nome |
| `pidof <programa>` | Retorna o PID de um programa |

```bash
ps aux | grep nginx           # encontra o processo do nginx
ps aux --sort=-%mem | head    # top 10 processos que mais consomem memória
pgrep python3                 # retorna os PIDs do python3
```

**Colunas do `ps aux`:**

| Coluna | Significado |
| ------ | ----------- |
| `USER` | Usuário dono do processo |
| `PID` | ID do processo |
| `%CPU` | Uso de CPU |
| `%MEM` | Uso de memória |
| `VSZ` | Memória virtual (KB) |
| `RSS` | Memória física em uso (KB) |
| `STAT` | Estado do processo |
| `COMMAND` | Comando que iniciou o processo |

---

## 📊 Monitoramento em Tempo Real

### top — Monitor básico

```bash
top
```

| Tecla no top | Ação |
| ------------ | ---- |
| `q` | Sair |
| `k` | Matar um processo (pede o PID) |
| `M` | Ordenar por memória |
| `P` | Ordenar por CPU |
| `1` | Exibir cada CPU individualmente |
| `u` | Filtrar por usuário |
| `h` | Ajuda |

---

### htop — Monitor interativo (recomendado)

```bash
sudo apt install htop
htop
```

| Tecla no htop | Ação |
| ------------- | ---- |
| `F9` | Matar processo selecionado |
| `F6` | Ordenar por coluna |
| `F5` | Exibir em árvore (hierarquia) |
| `F3` | Buscar processo |
| `F2` | Configurações |
| `q` | Sair |

---

## 🔴 Encerrando Processos

| Comando | Descrição |
| ------- | --------- |
| `kill <PID>` | Envia sinal de encerramento ao processo (SIGTERM) |
| `kill -9 <PID>` | Força encerramento imediato (SIGKILL) |
| `kill -15 <PID>` | Encerramento gracioso (padrão) |
| `killall <nome>` | Mata todos os processos com o nome |
| `pkill <nome>` | Mata processos pelo nome (aceita padrão parcial) |
| `pkill -u <usuario>` | Mata todos os processos de um usuário |

```bash
kill 1234
kill -9 5678              # força encerramento
killall firefox
pkill -f "python script"  # mata processo que contém o texto no comando
```

> 💡 Prefira `kill` (SIGTERM) ao invés de `kill -9` — dá chance ao processo de encerrar corretamente.

---

## ⏸️ Processos em Background e Foreground

| Comando | Descrição |
| ------- | --------- |
| `<comando> &` | Executa o comando em background |
| `Ctrl + Z` | Suspende o processo atual |
| `bg` | Retoma o processo suspenso em background |
| `fg` | Traz o processo de background para o foreground |
| `jobs` | Lista processos em background da sessão atual |
| `disown <PID>` | Desassocia processo do terminal (continua após logout) |
| `nohup <comando> &` | Executa e mantém rodando mesmo após fechar o terminal |

```bash
python3 servidor.py &        # roda em background
jobs                         # lista jobs
fg %1                        # traz o job 1 para o foreground
nohup ./deploy.sh &          # roda e ignora o fechamento do terminal
```

---

## 📅 Agendamento de Tarefas

### cron — Tarefas recorrentes

```bash
crontab -e    # editar tarefas do usuário atual
crontab -l    # listar tarefas agendadas
crontab -r    # remover todas as tarefas
```

**Formato do cron:**

```
*  *  *  *  *  comando
│  │  │  │  └─ dia da semana (0=Dom, 6=Sab)
│  │  │  └──── mês (1-12)
│  │  └─────── dia do mês (1-31)
│  └────────── hora (0-23)
└───────────── minuto (0-59)
```

**Exemplos:**

```bash
0 2 * * *    /usr/bin/backup.sh      # todo dia às 02:00
*/15 * * * * /usr/bin/check.sh       # a cada 15 minutos
0 9 * * 1    /usr/bin/relatorio.sh   # toda segunda-feira às 9h
30 8 1 * *   /usr/bin/mensal.sh      # dia 1 de cada mês às 8:30
```

---

## 💾 Uso de Memória e Disco

### Memória RAM

| Comando | Descrição |
| ------- | --------- |
| `free -h` | Exibe uso de RAM e swap em formato legível |
| `free -m` | Exibe em megabytes |
| `vmstat` | Estatísticas de memória virtual e CPU |
| `cat /proc/meminfo` | Informações detalhadas sobre a memória |

```bash
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           15Gi       5,2Gi       3,1Gi       512Mi       7,0Gi       9,5Gi
Swap:         2,0Gi          0B       2,0Gi
```

---

### Disco

| Comando | Descrição |
| ------- | --------- |
| `df -h` | Uso de disco de todas as partições |
| `df -h /home` | Uso de uma partição específica |
| `du -sh <pasta>` | Tamanho total de uma pasta |
| `du -sh * \| sort -h` | Tamanho de cada item, ordenado |
| `lsblk` | Lista discos e partições |
| `fdisk -l` | Detalhes de todos os discos (requer sudo) |
| `ncdu` | Navegador interativo de uso de disco |

```bash
df -h
du -sh ~/Downloads/* | sort -h    # o que mais ocupa espaço em downloads
sudo lsblk
sudo apt install ncdu && ncdu /   # interface visual de uso de disco
```

---

## 🖥️ Informações do Sistema

| Comando | Descrição |
| ------- | --------- |
| `uname -a` | Informações completas do kernel e sistema |
| `uname -r` | Versão do kernel |
| `lsb_release -a` | Versão da distribuição Linux |
| `cat /etc/os-release` | Detalhes da distro |
| `hostname` | Nome do computador |
| `hostname -I` | Endereço IP do computador |
| `uptime` | Tempo ligado e carga do sistema |
| `uptime -p` | Formato mais legível |
| `lscpu` | Informações do processador |
| `lsmem` | Informações da memória RAM |
| `lspci` | Lista dispositivos PCI (placa de vídeo, rede, etc.) |
| `lsusb` | Lista dispositivos USB conectados |
| `dmidecode` | Informações detalhadas do hardware (requer sudo) |

```bash
uname -a
lsb_release -a
lscpu
sudo dmidecode -t memory    # detalhes dos módulos de RAM
```

---

## 📋 Histórico e Logs do Sistema

| Comando | Descrição |
| ------- | --------- |
| `history` | Lista os últimos comandos digitados |
| `history \| grep apt` | Filtra histórico por termo |
| `!<número>` | Repete o comando pelo número do histórico |
| `!!` | Repete o último comando |
| `journalctl` | Logs do sistema (systemd) |
| `journalctl -u <serviço>` | Logs de um serviço específico |
| `journalctl -f` | Acompanha logs em tempo real |
| `journalctl --since "1 hour ago"` | Logs da última hora |
| `dmesg` | Mensagens do kernel |
| `dmesg \| grep -i error` | Filtra erros do kernel |

```bash
history | grep "git commit"
journalctl -u nginx --since today
journalctl -f                      # tail nos logs do sistema
dmesg | grep -i usb                # verificar dispositivo USB
```

---

## ⚠️ Boas Práticas

- Nunca mate processos do sistema com `kill -9` sem entender o que faz
- Use `htop` para ter uma visão completa e interativa dos recursos
- Monitore logs com `journalctl -f` ao instalar ou configurar serviços
- Agende tarefas de manutenção (backup, limpeza) com `cron`
- Verifique o uso de disco periodicamente — um disco cheio pode travar o sistema
- Use `nohup` ou `tmux` para processos longos que não devem ser interrompidos
