# ⚛️ Next.js / React — Comandos por Funcionalidade

Este README organiza os conceitos e comandos do **Next.js** de forma clara e padronizada.

---

## 💡 O que é React? O que é Next.js?

**React** é uma biblioteca JavaScript para construir interfaces visuais com componentes reutilizáveis.
**Next.js** é o framework que coloca o React no servidor, adiciona roteamento automático e facilita o deploy.

| Tecnologia | Função principal | Onde roda |
| ---------- | ---------------- | --------- |
| **React** | Constrói os componentes visuais da interface | No browser |
| **Next.js** | Gerencia rotas, servidor, build e deploy do React | No servidor **e** no browser |

> Você não instala React e Next.js separados — ao instalar o Next.js, o React já vem incluso.

---

## 🖥️ Onde Rodar os Comandos

| Terminal | Como abrir |
| -------- | ---------- |
| **VS Code (recomendado)** | Menu superior → `Terminal` → `New Terminal` |
| **CMD** | `Win + R` → digita `cmd` → Enter |
| **Git Bash** | Botão direito na pasta do projeto → `Git Bash Here` |
| **PowerShell** | Botão direito na pasta → `Abrir no Terminal` |

> O terminal do VS Code já abre automaticamente na pasta do projeto — é o mais prático.

---

## ✅ Verificação de Dependências

| Comando | O que verifica | Versão mínima |
| ------- | -------------- | ------------- |
| `node --version` | Node.js instalado | 18.17 ou superior |
| `npm --version` | npm instalado | Vem junto com o Node |
| `npx --version` | npx instalado | Vem junto com o Node |
| `git --version` | Git instalado | Qualquer versão recente |

> Se o Node não estiver instalado: **nodejs.org** → baixar versão **LTS**

---

## 📥 Download e Instalação

| O que instalar | Como instalar | Link |
| -------------- | ------------- | ---- |
| **Node.js** (inclui npm e npx) | Baixar instalador | [nodejs.org](https://nodejs.org) |
| **VS Code** | Baixar instalador | [code.visualstudio.com](https://code.visualstudio.com) |
| **Git** | Baixar instalador | [git-scm.com](https://git-scm.com) |

> Após instalar o Node.js, feche e reabra o terminal para os comandos `node`, `npm` e `npx` serem reconhecidos.

---

## 🚀 Criação do Projeto

| Comando | Descrição |
| ------- | --------- |
| `npx create-next-app@latest <nome>` | Cria um novo projeto Next.js |
| `npx create-next-app@latest .` | Cria o projeto na pasta atual |

### Respostas obrigatórias durante a criação

```
✔ Would you like to use TypeScript?               → Yes
✔ Would you like to use ESLint?                   → Yes
✔ Would you like to use Tailwind CSS?             → Yes
✔ Would you like to use the `src/` directory?     → No
✔ Would you like to use App Router?               → Yes
✔ Would you like to customize the import alias?   → No
```

---

## 📂 Navegação de Pastas no Terminal

| Comando | Descrição |
| ------- | --------- |
| `cd <nome-da-pasta>` | Entra em uma pasta |
| `cd ..` | Volta uma pasta acima |
| `cd C:\Users\Nome\Documents` | Navega para um caminho absoluto |
| `dir` | Lista arquivos da pasta atual (CMD) |
| `ls` | Lista arquivos da pasta atual (Git Bash / PowerShell) |
| `pwd` | Mostra o caminho completo da pasta atual |

---

## ▶️ Execução do Projeto

| Comando | Descrição |
| ------- | --------- |
| `npm run dev` | Inicia o servidor de desenvolvimento em `localhost:3000` |
| `npm run build` | Gera a versão otimizada para produção |
| `npm run start` | Inicia o servidor com a versão de produção (usar após o build) |
| `npm run lint` | Verifica erros de código |
| `Ctrl + C` | Para o servidor em execução |

---

## 📦 Gerenciamento de Pacotes

| Comando | Descrição |
| ------- | --------- |
| `npm install` | Instala todas as dependências do `package.json` |
| `npm install <pacote>` | Instala um pacote no projeto |
| `npm install <p1> <p2> <p3>` | Instala vários pacotes de uma vez |
| `npm install <pacote> --save-dev` | Instala pacote apenas para desenvolvimento |
| `npm uninstall <pacote>` | Remove um pacote do projeto |
| `npm update` | Atualiza todos os pacotes para a versão mais recente permitida |
| `npm list` | Lista os pacotes instalados no projeto |
| `npm list --depth=0` | Lista apenas os pacotes diretos (sem dependências) |
| `npm outdated` | Mostra pacotes com versões mais novas disponíveis |
| `npm cache clean --force` | Limpa o cache do npm (útil em caso de erros) |

> Sempre pare o servidor com `Ctrl + C` antes de instalar novos pacotes.

> Avisos de **"vulnerabilities"** após o `npm install` são normais — podem ser ignorados durante o desenvolvimento.

---

## 🎨 shadcn/ui — Biblioteca de Componentes

| Comando | Descrição |
| ------- | --------- |
| `npx shadcn@latest init` | Inicializa o shadcn/ui no projeto |
| `npx shadcn@latest add <componente>` | Adiciona um componente ao projeto |
| `npx shadcn@latest add --all` | Adiciona todos os componentes disponíveis |

### Respostas durante o `init`

```
✔ Which style would you like to use?              → Default
✔ Which color would you like to use as base?      → Slate
✔ Would you like to use CSS variables for colors? → Yes
```

### Componentes mais utilizados

| Comando | Componente gerado |
| ------- | ----------------- |
| `npx shadcn@latest add button` | Botão estilizado |
| `npx shadcn@latest add card` | Card / painel |
| `npx shadcn@latest add table` | Tabela |
| `npx shadcn@latest add input` | Campo de texto |
| `npx shadcn@latest add label` | Rótulo de formulário |
| `npx shadcn@latest add select` | Lista suspensa |
| `npx shadcn@latest add dialog` | Modal / janela popup |
| `npx shadcn@latest add badge` | Etiqueta colorida |
| `npx shadcn@latest add textarea` | Campo de texto multilinha |
| `npx shadcn@latest add toast` | Notificação temporária |
| `npx shadcn@latest add dropdown-menu` | Menu suspenso |
| `npx shadcn@latest add calendar` | Calendário interativo |

---

## 🗂️ Criação de Arquivos e Pastas

### 🪟 Windows (CMD)

| Comando | Descrição |
| ------- | --------- |
| `mkdir <pasta>` | Cria uma pasta |
| `mkdir pasta1\pasta2` | Cria pastas aninhadas |
| `type nul > <arquivo>` | Cria um arquivo vazio |

### 🐧 Linux / 🍎 macOS / Git Bash

| Comando | Descrição |
| ------- | --------- |
| `mkdir <pasta>` | Cria uma pasta |
| `mkdir -p pasta1/pasta2` | Cria pastas aninhadas |
| `touch <arquivo>` | Cria um arquivo vazio |

---

## 📁 Estrutura de Pastas

```
meu-projeto/
│
├── app/                    ← páginas e rotas (cada subpasta = uma URL)
│   ├── layout.tsx          ← estrutura HTML que envolve todas as páginas
│   ├── page.tsx            ← página da rota "/"
│   ├── globals.css         ← estilos globais
│   │
│   ├── dashboard/
│   │   └── page.tsx        ← rota /dashboard
│   └── login/
│       └── page.tsx        ← rota /login
│
├── components/             ← componentes reutilizáveis entre páginas
│   └── ui/                 ← componentes do shadcn (gerados automaticamente)
│
├── lib/                    ← funções utilitárias e configurações de serviços
│
├── actions/                ← funções que se comunicam com o banco de dados
│
├── public/                 ← arquivos estáticos (imagens, ícones, fontes)
│
├── middleware.ts            ← intercepta requisições antes de chegar nas páginas
├── .env.local               ← variáveis de ambiente (nunca versionar)
├── .gitignore
├── next.config.ts           ← configurações do Next.js
├── tailwind.config.ts       ← configurações do Tailwind CSS
└── package.json             ← dependências do projeto
```

---

## 🗺️ Roteamento Automático

No Next.js não existe configuração manual de rotas.
A URL é definida pela **estrutura de pastas** dentro de `app/`.
Toda pasta que contém um arquivo `page.tsx` vira uma rota acessível no browser.

| Arquivo criado | URL gerada |
| -------------- | ---------- |
| `app/page.tsx` | `localhost:3000/` |
| `app/dashboard/page.tsx` | `localhost:3000/dashboard` |
| `app/login/page.tsx` | `localhost:3000/login` |
| `app/produtos/page.tsx` | `localhost:3000/produtos` |
| `app/produtos/[id]/page.tsx` | `localhost:3000/produtos/123` ← rota dinâmica |

---

## 🧩 Server Components vs Client Components

Todo componente no Next.js é **Server Component por padrão** — roda no servidor, acessa banco diretamente, envia HTML pronto ao browser.

**Client Component** só é necessário quando o componente precisa de interatividade no browser.

| Tipo | Onde roda | Acessa banco? | Tem interação? | Como identificar |
| ---- | --------- | ------------- | -------------- | ---------------- |
| **Server Component** | Servidor | ✅ Sim | ❌ Não | Nenhuma marcação — é o padrão |
| **Client Component** | Browser | ❌ Não | ✅ Sim | `'use client'` no topo do arquivo |

### Server Component (padrão — sem marcação)

```tsx
export default async function DashboardPage() {
  const dados = await buscarDosBanco()

  return (
    <main>
      <h1>Dashboard</h1>
      {dados.map(item => <p key={item.id}>{item.nome}</p>)}
    </main>
  )
}
```

### Client Component (`'use client'` obrigatório)

```tsx
'use client'

import { useState } from 'react'

export default function Formulario() {
  const [valor, setValor] = useState('')

  return <input value={valor} onChange={e => setValor(e.target.value)} />
}
```

> **Regra prática:** comece sempre sem `'use client'`. Adicione só quando o Next.js reclamar no terminal.

---

## 🧠 JSX — Sintaxe dos Componentes

JSX é a sintaxe que mistura HTML com TypeScript dentro dos componentes.
Tudo que está dentro do `return` de um componente é JSX.

| Recurso | Sintaxe JSX | O que faz |
| ------- | ----------- | --------- |
| Variável | `{variavel}` | Exibe o valor de uma variável |
| Condição | `{condicao && <div>...</div>}` | Renderiza só se a condição for verdadeira |
| Ternário | `{condicao ? <A /> : <B />}` | Renderiza A ou B dependendo da condição |
| Lista | `{lista.map(item => <p key={item.id}>{item.nome}</p>)}` | Renderiza um elemento por item |
| Classe CSS | `className="minha-classe"` | Equivalente ao `class` do HTML puro |
| Evento de clique | `onClick={minhaFuncao}` | Chama função ao clicar |
| Evento de input | `onChange={e => setValor(e.target.value)}` | Captura o que o usuário digita |

> Em JSX, `class` vira `className` e `for` vira `htmlFor` — são palavras reservadas do JavaScript.

---

## 🔑 Variáveis de Ambiente

Crie o arquivo `.env.local` na **raiz do projeto** (mesma pasta do `package.json`):

```bash
# .env.local
NEXT_PUBLIC_MINHA_URL=https://exemplo.com
MINHA_CHAVE_SECRETA=valor_secreto
```

| Prefixo | Visível onde | Quando usar |
| ------- | ------------ | ----------- |
| `NEXT_PUBLIC_` | Servidor **e** browser | Chaves que o frontend precisa acessar |
| *(sem prefixo)* | Só no servidor | Senhas e tokens — nunca expostos ao browser |

> O arquivo `.env.local` já vem no `.gitignore` por padrão. Confirme antes de qualquer `git push`.

---

## 📄 Exemplo mínimo de componente

```tsx
// app/page.tsx
export default function HomePage() {
  return (
    <main>
      <h1>Olá, Next.js!</h1>
      <p>Minha primeira página.</p>
    </main>
  )
}
```

> Cada `page.tsx` deve ter obrigatoriamente um `export default` — é o que o Next.js usa para renderizar a página.

---

## 🚫 .gitignore

```gitignore
.env.local
.env
node_modules/
.next/
out/
```

---

## 📁 Estrutura Recomendada

```
meu-projeto/
│
├── app/               ← rotas e páginas
├── components/        ← componentes reutilizáveis
├── lib/               ← utilitários e integrações externas
├── actions/           ← lógica de banco de dados
├── public/            ← arquivos estáticos
├── .env.local         ← variáveis de ambiente (não versionar)
├── .gitignore
└── package.json
```

---

## ⚠️ Boas Práticas

* Usar `'use client'` somente quando necessário — componentes de servidor são mais performáticos
* Nunca versionar o `.env.local` — contém chaves e senhas
* Manter a lógica de banco em `actions/` — não escrever queries direto nas páginas
* Criar uma pasta por responsabilidade dentro de `app/`
* Parar o servidor com `Ctrl + C` antes de instalar pacotes com `npm install`
* Nomear arquivos de componentes em inglês para evitar erros de importação
* Não editar manualmente os arquivos dentro de `components/ui/` — são gerados pelo shadcn
