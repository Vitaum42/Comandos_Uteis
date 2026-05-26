# 📦 Linux — Gerenciamento de Pacotes

Este guia cobre como instalar, atualizar, remover e gerenciar programas no Linux.

---

## 🗺️ Gerenciadores de Pacotes por Distribuição

Cada família de distribuição usa um gerenciador de pacotes diferente:

| Distribuição | Gerenciador | Comando base |
| ------------ | ----------- | ------------ |
| Ubuntu, Debian, Mint | **apt** | `sudo apt install` |
| Fedora, RHEL | **dnf** | `sudo dnf install` |
| Arch Linux, Manjaro | **pacman** | `sudo pacman -S` |
| openSUSE | **zypper** | `sudo zypper install` |
| Qualquer distro | **snap** | `sudo snap install` |
| Qualquer distro | **flatpak** | `flatpak install` |

> 💡 Este guia foca no **apt** (Ubuntu/Debian/Mint), o mais comum para iniciantes.

---

## 🔄 Atualização do Sistema

| Comando | Descrição |
| ------- | --------- |
| `sudo apt update` | Atualiza a lista de pacotes disponíveis nos repositórios |
| `sudo apt upgrade` | Instala atualizações disponíveis (pede confirmação) |
| `sudo apt upgrade -y` | Instala atualizações sem pedir confirmação |
| `sudo apt full-upgrade` | Atualiza e resolve dependências mais complexas |
| `sudo apt dist-upgrade` | Similar ao full-upgrade, pode remover pacotes obsoletos |
| `sudo apt update && sudo apt upgrade -y` | Atualiza lista e instala tudo de uma vez |

```bash
sudo apt update
sudo apt upgrade
```

> 💡 Sempre rode `apt update` antes de instalar qualquer coisa — ele atualiza o índice de pacotes.

---

## 📥 Instalando Pacotes

| Comando | Descrição |
| ------- | --------- |
| `sudo apt install <pacote>` | Instala um pacote |
| `sudo apt install <p1> <p2> <p3>` | Instala vários pacotes de uma vez |
| `sudo apt install -y <pacote>` | Instala sem pedir confirmação |
| `sudo apt install --no-install-recommends <p>` | Instala sem pacotes opcionais recomendados |
| `sudo apt reinstall <pacote>` | Reinstala um pacote |
| `sudo dpkg -i <arquivo.deb>` | Instala um pacote `.deb` baixado manualmente |

```bash
sudo apt install git curl wget vim htop -y
sudo dpkg -i google-chrome-stable_amd64.deb
```

---

## 🗑️ Removendo Pacotes

| Comando | Descrição |
| ------- | --------- |
| `sudo apt remove <pacote>` | Remove o pacote (mantém arquivos de configuração) |
| `sudo apt purge <pacote>` | Remove o pacote **e** seus arquivos de configuração |
| `sudo apt autoremove` | Remove dependências que não são mais necessárias |
| `sudo apt autoremove --purge` | Remove dependências órfãs + suas configurações |
| `sudo apt clean` | Limpa o cache de pacotes baixados |
| `sudo apt autoclean` | Remove apenas pacotes desatualizados do cache |

```bash
sudo apt purge vlc
sudo apt autoremove
sudo apt clean
```

---

## 🔍 Buscando e Inspecionando Pacotes

| Comando | Descrição |
| ------- | --------- |
| `apt search <termo>` | Busca pacotes disponíveis |
| `apt show <pacote>` | Exibe detalhes de um pacote |
| `apt list --installed` | Lista todos os pacotes instalados |
| `apt list --upgradable` | Lista pacotes com atualizações disponíveis |
| `dpkg -l` | Lista todos os pacotes instalados (formato completo) |
| `dpkg -l \| grep <termo>` | Filtra por nome |
| `dpkg -L <pacote>` | Lista os arquivos instalados por um pacote |
| `dpkg -S <arquivo>` | Descobre a qual pacote um arquivo pertence |
| `which <programa>` | Mostra onde o programa está instalado |

```bash
apt search python3
apt show nginx
apt list --installed | grep python
dpkg -L vim                          # onde o vim instalou seus arquivos
dpkg -S /usr/bin/git                 # qual pacote instalou o git
```

---

## 📌 Fixando Versões (Hold)

Evita que um pacote seja atualizado automaticamente:

| Comando | Descrição |
| ------- | --------- |
| `sudo apt-mark hold <pacote>` | Congela a versão de um pacote |
| `sudo apt-mark unhold <pacote>` | Descongela o pacote |
| `apt-mark showhold` | Lista todos os pacotes congelados |

```bash
sudo apt-mark hold mysql-server    # evita atualização automática
apt-mark showhold
```

---

## 🧩 Snap — Pacotes Universais

O Snap instala aplicativos em contêineres isolados, funcionando em qualquer distro.

| Comando | Descrição |
| ------- | --------- |
| `sudo snap install <pacote>` | Instala um pacote snap |
| `sudo snap remove <pacote>` | Remove um pacote snap |
| `snap list` | Lista snaps instalados |
| `sudo snap refresh` | Atualiza todos os snaps |
| `snap find <termo>` | Busca pacotes disponíveis |
| `sudo snap install <p> --classic` | Instala com acesso total ao sistema |

```bash
sudo snap install code --classic    # instala o VS Code
sudo snap install discord
snap list
```

---

## 📦 Flatpak — Outra Opção Universal

| Comando | Descrição |
| ------- | --------- |
| `flatpak install <repositorio> <app>` | Instala um app Flatpak |
| `flatpak uninstall <app>` | Remove o app |
| `flatpak list` | Lista apps instalados |
| `flatpak update` | Atualiza todos os apps |
| `flatpak run <app>` | Executa um app Flatpak |

```bash
flatpak install flathub com.spotify.Client
flatpak list
flatpak update
```

> 💡 Instale suporte ao Flatpak com: `sudo apt install flatpak` e adicione o repositório: `flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo`

---

## 📋 Repositórios PPA (Ubuntu)

PPAs são repositórios externos que adicionam programas ou versões mais recentes:

| Comando | Descrição |
| ------- | --------- |
| `sudo add-apt-repository ppa:<usuario/ppa>` | Adiciona um PPA |
| `sudo add-apt-repository --remove ppa:<u/ppa>` | Remove um PPA |
| `cat /etc/apt/sources.list` | Lista repositórios principais |
| `ls /etc/apt/sources.list.d/` | Lista repositórios extras |

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.12
```

> ⚠️ Use PPAs apenas de fontes confiáveis — eles têm acesso total ao seu sistema.

---

## ⚠️ Boas Práticas

- Sempre rode `sudo apt update` antes de instalar qualquer pacote
- Prefira pacotes do repositório oficial antes de PPAs ou .deb externos
- Use `sudo apt purge` em vez de `remove` para eliminar completamente um programa
- Rode `sudo apt autoremove` periodicamente para liberar espaço
- Verifique o pacote com `apt show` antes de instalar para confirmar que é o correto
- Mantenha o sistema atualizado regularmente — especialmente patches de segurança
