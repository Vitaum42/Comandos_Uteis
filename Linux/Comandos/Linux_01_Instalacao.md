# 📦 Linux — Instalação

Este guia cobre todo o processo de instalação do Linux, desde a escolha da distribuição até a configuração inicial do sistema.

---

## 🗺️ Escolhendo a Distribuição

A "distribuição" (distro) é a versão do Linux que você vai instalar. Existem dezenas, mas para iniciantes as mais recomendadas são:

| Distribuição | Baseada em | Indicada para | Link |
| ------------ | ---------- | ------------- | ---- |
| **Ubuntu** | Debian | Iniciantes em geral | [ubuntu.com](https://ubuntu.com/download) |
| **Linux Mint** | Ubuntu | Quem vem do Windows | [linuxmint.com](https://linuxmint.com/download.php) |
| **Pop!_OS** | Ubuntu | Desenvolvedores e gamers | [pop.system76.com](https://pop.system76.com) |
| **Zorin OS** | Ubuntu | Transição do Windows/Mac | [zorin.com](https://zorin.com/os/download/) |
| **Fedora** | — | Usuários intermediários | [fedoraproject.org](https://fedoraproject.org) |
| **Debian** | — | Estabilidade máxima | [debian.org](https://www.debian.org/distrib/) |
| **Arch Linux** | — | Usuários avançados | [archlinux.org](https://archlinux.org) |

> 💡 **Recomendação para iniciantes:** Ubuntu LTS ou Linux Mint Cinnamon.

---

## 💾 Requisitos Mínimos de Hardware

| Componente | Mínimo | Recomendado |
| ---------- | ------ | ----------- |
| Processador | 2 GHz dual-core | 4 GHz quad-core |
| RAM | 2 GB | 4 GB ou mais |
| Armazenamento | 25 GB | 50 GB ou mais |
| Pendrive | 4 GB | 8 GB ou mais |

---

## 🛠️ Criando o Pendrive Bootável

### Ferramentas recomendadas

| Ferramenta | Sistema | Link |
| ---------- | ------- | ---- |
| **Rufus** | Windows | [rufus.ie](https://rufus.ie/) |
| **balenaEtcher** | Windows / Mac / Linux | [etcher.balena.io](https://etcher.balena.io/) |
| **Ventoy** | Windows / Linux | [ventoy.net](https://www.ventoy.net/) |

### Passo a passo com Rufus (Windows)

1. Baixe a ISO da distribuição escolhida
2. Abra o Rufus com o pendrive conectado
3. Selecione o pendrive em **Dispositivo**
4. Clique em **Selecionar** e escolha a ISO baixada
5. Mantenha as configurações padrão e clique em **Iniciar**
6. Aguarde a conclusão (5–10 min)

---

## 🔧 Acessando o Boot pelo Pendrive

Ao reiniciar o computador, pressione a tecla de boot antes do Windows carregar:

| Fabricante | Tecla comum |
| ---------- | ----------- |
| ASUS | F2 ou Del |
| Dell | F12 |
| HP | F9 ou F10 |
| Lenovo | F1 ou F12 |
| Acer | F2 ou Del |
| Samsung | F2 |

> 💡 Se não souber a tecla, procure por `"boot menu [modelo do seu notebook]"`.

---

## 🖥️ Instalação do Ubuntu (Passo a Passo)

1. **Selecione o idioma** — Escolha Português (Brasil)
2. **Tipo de instalação** — Escolha "Instalação normal"
3. **Atualizações** — Marque "Baixar atualizações durante a instalação"
4. **Particionamento:**
   - **Dual boot com Windows:** Selecione "Instalar Ubuntu ao lado do Windows"
   - **Somente Linux:** Selecione "Apagar disco e instalar Ubuntu" ⚠️
5. **Fuso horário** — Selecione "São Paulo" ou a sua cidade
6. **Crie seu usuário** — Defina nome, nome do computador, usuário e senha
7. **Aguarde** — A instalação leva de 10 a 30 minutos
8. **Reinicie** e remova o pendrive quando solicitado

---

## 🚀 Primeiros Comandos Após a Instalação

Abra o terminal (`Ctrl + Alt + T`) e execute:

### Atualizar o sistema

```bash
sudo apt update && sudo apt upgrade -y
```

### Instalar pacotes essenciais

```bash
sudo apt install curl wget git vim htop build-essential -y
```

### Instalar suporte a codecs de mídia

```bash
sudo apt install ubuntu-restricted-extras -y
```

### Verificar se o sistema está atualizado

```bash
sudo apt list --upgradable
```

### Reiniciar após as atualizações

```bash
sudo reboot
```

---

## 🔄 Dual Boot — Linux + Windows

> Permite usar os dois sistemas no mesmo computador.

### Antes de instalar:
- **Faça backup** dos seus dados do Windows
- **Desative o Secure Boot** na BIOS (em alguns casos)
- **Desative o Fast Startup** no Windows:
  - Painel de Controle → Opções de Energia → Escolher a função dos botões → desmarcar "Inicialização Rápida"
- **Libere espaço** em disco pelo Windows (mínimo 30 GB livres)

### Durante a instalação:
- Selecione **"Instalar ao lado do Windows"** — o instalador cuidará do particionamento
- Ao reiniciar, o **GRUB** (menu de boot) aparecerá para escolher o sistema

---

## 🧹 Desinstalando o Linux (Dual Boot)

Caso queira remover o Linux e volcar apenas ao Windows:

1. Boot no Windows
2. Abra o **Gerenciamento de Disco**
3. Delete as partições do Linux (ext4, swap)
4. Expanda a partição do Windows no espaço liberado
5. Repare o bootloader com o comando no Prompt (como administrador):

```cmd
bootrec /fixmbr
bootrec /fixboot
bootrec /rebuildbcd
```

---

## ⚠️ Boas Práticas na Instalação

- Sempre faça backup antes de instalar ou reparticionar
- Prefira versões LTS (Long Term Support) — mais estáveis e suportadas por mais tempo
- Nunca force o desligamento durante a instalação
- Teste a distro no modo "Experimentar" antes de instalar definitivamente
- Mantenha pelo menos 10% do disco livre para o sistema funcionar bem
