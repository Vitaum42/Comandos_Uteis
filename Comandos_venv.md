# 📦 Python venv — Guia Completo

Este guia reúne **todos os comandos em sequência**, sem separações, para uso direto no dia a dia com ambientes virtuais (`venv`).

```bash
# Criar ambiente virtual
python -m venv venv

# Ativar (Windows CMD)
venv\Scripts\activate

# Ativar (Windows PowerShell)
venv\Scripts\Activate.ps1

# Ativar (Linux/macOS)
source venv/bin/activate

# Verificar se está ativo (apenas visual)
(venv) caminho/do/projeto>

# Instalar pacote
pip install nome_do_pacote

# Listar pacotes
pip list

# Salvar dependências
pip freeze > requirements.txt

# Instalar dependências
pip install -r requirements.txt

# Atualizar pip
python -m pip install --upgrade pip

# Desativar ambiente
deactivate

# Remover ambiente (Linux/macOS)
rm -rf venv

# Remover ambiente (Windows)
rmdir /s venv
```

## 📁 Estrutura recomendada

```
meu_projeto/
│
├── venv/              # ambiente virtual (não versionar)
├── src/               # código do projeto
│   └── ... 
├── requirements.txt   # dependências
└── README.md          # documentação
```

## 🚫 .gitignore

```
venv/
__pycache__/
*.pyc
.env
```
