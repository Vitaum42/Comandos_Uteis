# 📦 Python venv — Comandos por Funcionalidade

Este README organiza os comandos de **ambiente virtual (venv)** de forma clara e padronizada.

---

## 🚀 Criação do Ambiente

| Comando               | Descrição                |
| --------------------- | ------------------------ |
| `python -m venv venv` | Cria um ambiente virtual |

---

## ▶️ Ativação do Ambiente

### 🪟 Windows

| Comando                     | Descrição           |
| --------------------------- | ------------------- |
| `venv\Scripts\activate`     | Ativa no CMD        |
| `venv\Scripts\Activate.ps1` | Ativa no PowerShell |

### 🐧 Linux / 🍎 macOS

| Comando                    | Descrição        |
| -------------------------- | ---------------- |
| `source venv/bin/activate` | Ativa o ambiente |

---

## ⛔ Desativação

| Comando      | Descrição                   |
| ------------ | --------------------------- |
| `deactivate` | Desativa o ambiente virtual |

---

## 🔎 Verificação

| Situação     | Descrição                                    |
| ------------ | -------------------------------------------- |
| `(venv) ...` | Indica que o ambiente está ativo no terminal |

---

## 📦 Gerenciamento de Pacotes

| Comando                | Descrição                               |
| ---------------------- | --------------------------------------- |
| `pip install <pacote>` | Instala um pacote                       |
| `pip list`             | Lista pacotes instalados                |
| `pip freeze`           | Lista pacotes no formato de dependência |

---

## 💾 Dependências

| Comando                           | Descrição                       |
| --------------------------------- | ------------------------------- |
| `pip freeze > requirements.txt`   | Salva dependências              |
| `pip install -r requirements.txt` | Instala dependências do arquivo |

---

## 🔄 Atualização

| Comando                               | Descrição      |
| ------------------------------------- | -------------- |
| `python -m pip install --upgrade pip` | Atualiza o pip |

---

## ❌ Remoção do Ambiente

### 🐧 Linux / 🍎 macOS

| Comando       | Descrição     |
| ------------- | ------------- |
| `rm -rf venv` | Remove a venv |

### 🪟 Windows

| Comando         | Descrição     |
| --------------- | ------------- |
| `rmdir /s venv` | Remove a venv |

---

## 📁 Estrutura Recomendada

```id="estruturavenv"
meu_projeto/
│
├── venv/              # ambiente virtual (não versionar)
├── src/               # código do projeto
│   └── ... 
├── requirements.txt   # dependências
└── README.md          # documentação
```

---

## 🚫 .gitignore

```gitignore id="g1e8nx"
venv/
__pycache__/
*.pyc
.env
```

---

## ⚠️ Boas práticas

* Sempre ativar a venv antes de instalar pacotes
* Não versionar a pasta `venv/`
* Usar `requirements.txt` para padronizar dependências
* Criar uma venv para cada projeto

---
