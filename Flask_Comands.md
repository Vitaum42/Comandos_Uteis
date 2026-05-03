# 🌐 Flask — Guia de Comandos

Este README contém **apenas os comandos relacionados ao Flask**.
A criação e gerenciamento da **venv** são necessários, mas estão documentados separadamente.

---

## ⚠️ Sobre a venv

Antes de tudo:

* É necessário criar e ativar uma **venv**
* Isso garante isolamento de dependências

> Consulte o README de venv do repositório para os comandos completos.

---

## 🚀 Instalação do Flask

```bash
pip install flask
```

---

## 💾 Salvar dependências (opcional, mas recomendado)

```bash
pip freeze > requirements.txt
```

---

## 📄 Criar arquivo principal

### Windows

```bash
type nul > app.py
```

### Linux / macOS

```bash
touch app.py
```

---

## ▶️ Rodar aplicação

### Método direto (Python)

```bash
python app.py
```

---

## ▶️ Rodar via Flask CLI (recomendado)

### Windows (CMD)

```bash
set FLASK_APP=app.py
set FLASK_ENV=development
flask run
```

### Windows (PowerShell)

```bash
$env:FLASK_APP="app.py"
$env:FLASK_ENV="development"
flask run
```

### Linux / macOS

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```

---

## 📄 Exemplo mínimo de `app.py`

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"

if __name__ == "__main__":
    app.run(debug=True)
```

---

## 📁 Estrutura recomendada

```text
meu_projeto_flask/
│
├── venv/              # ambiente virtual (ver README de venv)
├── app.py             # aplicação principal
├── requirements.txt   # dependências
└── README.md
```

---

## 🚫 .gitignore

```gitignore
venv/
__pycache__/
*.pyc
.env
```
