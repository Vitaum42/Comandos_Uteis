# 🌐 Flask — Comandos por Funcionalidade

Este README organiza os comandos do **Flask** de forma clara e padronizada.
A **venv é obrigatória**, mas seus comandos estão documentados em outro README.

---

## ⚠️ Sobre a venv

* Criar e ativar uma **venv** antes de usar Flask
* Garante isolamento de dependências
* Consulte o README de venv para os comandos completos

---

## 🚀 Instalação

| Comando             | Descrição                   |
| ------------------- | --------------------------- |
| `pip install flask` | Instala o Flask no ambiente |

---

## 💾 Dependências

| Comando                           | Descrição            |
| --------------------------------- | -------------------- |
| `pip freeze > requirements.txt`   | Salva dependências   |
| `pip install -r requirements.txt` | Instala dependências |

---

## 📄 Arquivo da Aplicação

### 🪟 Windows

| Comando             | Descrição              |
| ------------------- | ---------------------- |
| `type nul > app.py` | Cria arquivo principal |

### 🐧 Linux / 🍎 macOS

| Comando        | Descrição              |
| -------------- | ---------------------- |
| `touch app.py` | Cria arquivo principal |

---

## ▶️ Execução da Aplicação

### Método direto (Python)

| Comando         | Descrição                       |
| --------------- | ------------------------------- |
| `python app.py` | Executa a aplicação diretamente |

---

### Flask CLI (Recomendado)

### 🪟 Windows (CMD)

| Comando                     | Descrição          |
| --------------------------- | ------------------ |
| `set FLASK_APP=app.py`      | Define app         |
| `set FLASK_ENV=development` | Define ambiente    |
| `flask run`                 | Executa o servidor |

### 🪟 Windows (PowerShell)

| Comando                        | Descrição          |
| ------------------------------ | ------------------ |
| `$env:FLASK_APP="app.py"`      | Define app         |
| `$env:FLASK_ENV="development"` | Define ambiente    |
| `flask run`                    | Executa o servidor |

### 🐧 Linux / 🍎 macOS

| Comando                        | Descrição          |
| ------------------------------ | ------------------ |
| `export FLASK_APP=app.py`      | Define app         |
| `export FLASK_ENV=development` | Define ambiente    |
| `flask run`                    | Executa o servidor |

---

## 📄 Exemplo mínimo de `app.py`

```python id="flaskexemplo"
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"

if __name__ == "__main__":
    app.run(debug=True)
```

---

## 📁 Estrutura Recomendada

```id="estruturaflask"
meu_projeto/
│
├── venv/              # ambiente virtual (não versionar)
├── src/               # código do projeto
│   └── app.py
├── requirements.txt   # dependências
└── README.md          # documentação
```

---

## 🚫 .gitignore

```gitignore id="gitignoreflask"
venv/
__pycache__/
*.pyc
.env
```

---

## ⚠️ Boas práticas

* Sempre usar venv
* Não versionar `venv/`
* Usar `requirements.txt`
* Separar código dentro de `src/`
* Usar modo development apenas em ambiente local

---
