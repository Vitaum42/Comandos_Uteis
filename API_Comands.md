# 🚀 FastAPI — Guia Completo (Comandos + Estrutura Profissional)

Este README reúne:

* ✅ **Comandos essenciais para rodar FastAPI**
* ✅ **Estrutura profissional de projeto (separação de responsabilidades)**

---

## ⚠️ Sobre a venv

* Crie e ative uma **venv** antes de começar
* Evita conflito de bibliotecas entre projetos
* Consulte o README de venv para os comandos completos

---

# 💻 Comandos por Funcionalidade

## 🚀 Instalação

| Comando                       | Descrição                                                           |
| ----------------------------- | ------------------------------------------------------------------- |
| `pip install fastapi uvicorn` | Instala o FastAPI (API) e o Uvicorn (servidor que roda a aplicação) |

---

## 💾 Dependências

| Comando                           | Descrição                    |
| --------------------------------- | ---------------------------- |
| `pip freeze > requirements.txt`   | Salva tudo que você instalou |
| `pip install -r requirements.txt` | Instala tudo automaticamente |

---

## 📄 Criar arquivo principal

### 🪟 Windows

| Comando              | Descrição                      |
| -------------------- | ------------------------------ |
| `type nul > main.py` | Cria o arquivo principal vazio |

### 🐧 Linux / 🍎 macOS

| Comando         | Descrição                      |
| --------------- | ------------------------------ |
| `touch main.py` | Cria o arquivo principal vazio |

---

## ▶️ Rodar a aplicação

| Comando                     | Descrição                                                  |
| --------------------------- | ---------------------------------------------------------- |
| `uvicorn main:app --reload` | Liga a API e reinicia automaticamente ao salvar alterações |

---

## 🌐 Acessos no navegador

| URL                         | Descrição                |
| --------------------------- | ------------------------ |
| http://127.0.0.1:8000       | API rodando              |
| http://127.0.0.1:8000/docs  | Interface para testar    |
| http://127.0.0.1:8000/redoc | Documentação alternativa |

---

## 🔄 Métodos HTTP

| Método | Descrição              |
| ------ | ---------------------- |
| GET    | Buscar dados           |
| POST   | Criar dados            |
| PUT    | Atualizar tudo         |
| PATCH  | Atualizar parcialmente |
| DELETE | Remover dados          |

---

# 🧱 Estrutura de Projeto (Profissional)

## 📁 Estrutura Recomendada

```bash id="estrutura-completa"
meu_projeto/
│
├── venv/                  # ambiente virtual (não versionar)
│
├── src/                   # código principal
│   │
│   ├── main.py            # ponto de entrada da API
│   │
│   ├── routes/            # rotas (endpoints)
│   │   ├── user_routes.py
│   │   └── product_routes.py
│   │
│   ├── services/          # lógica da aplicação
│   │   ├── user_service.py
│   │   └── product_service.py
│   │
│   ├── models/            # modelos de dados
│   │   ├── user_model.py
│   │   └── product_model.py
│   │
│   ├── schemas/           # entrada/saída (opcional)
│   │   └── user_schema.py
│   │
│   ├── database/          # conexão com banco
│   │   ├── connection.py
│   │   └── base.py
│   │
│   ├── config/            # configurações
│   │   └── settings.py
│   │
│   └── utils/             # funções auxiliares
│       └── helpers.py
│
├── tests/                 # testes
│   └── test_users.py
│
├── .env                   # variáveis de ambiente
├── .gitignore
├── requirements.txt
└── README.md
```

---

# 🧠 Explicação das Pastas

## ▶️ `main.py`

* Onde a API começa
* Junta todas as rotas

---

## 🌐 `routes/`

* Recebe as requisições (GET, POST, etc)
* Só direciona (não faz lógica pesada)

---

## ⚙️ `services/`

* Onde fica a lógica de verdade
* Regras do sistema

---

## 📦 `models/`

* Define como os dados são estruturados
* Validação automática

---

## 📄 `schemas/`

* Define entrada e saída da API
* Ajuda a organizar melhor projetos maiores

---

## 🗄️ `database/`

* Conexão com banco de dados
* Configuração do ORM

---

## ⚙️ `config/`

* Configurações gerais
* Variáveis do sistema

---

## 🧰 `utils/`

* Funções reutilizáveis
* Código auxiliar

---

## 🧪 `tests/`

* Testes da aplicação
* Garante que tudo funciona

---

# 🔄 Fluxo da Aplicação

```text id="fluxo-api"
Cliente → Rota → Service → Banco → Service → Rota → Cliente
```

---

# ⚠️ Boas práticas

* Não colocar lógica dentro das rotas
* Sempre separar responsabilidades
* Usar `.env` para dados sensíveis
* Nomear arquivos de forma clara
* Manter padrão desde o início

---

Esse modelo já segue um padrão usado em projetos profissionais.
