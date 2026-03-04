# 💳 Sistema de Solicitações de Crédito

**README — Guia de Instalação e Uso**  
`Node.js` · `React` · `MariaDB` · `Git` · `AWS Ready`

---

## 1. Descrição do Projeto

Este projeto implementa um sistema de cadastro, listagem, atualização e remoção (CRUD) de solicitações de crédito. O objetivo é praticar conceitos fundamentais de desenvolvimento Full Stack:

- Construção de uma API REST com Node.js e Express
- Arquitetura em camadas: Routes → Controllers → Services → Models
- Integração com banco de dados relacional MariaDB
- Interface web em React com estado imutável
- Validação de dados no front-end e no back-end
- Versionamento e publicação do código no GitHub

---

## 2. Tecnologias Utilizadas

| Tecnologia | Função | Por que usar? |
|---|---|---|
| **Node.js** | Servidor JavaScript | Executa JS fora do navegador, alta performance para APIs |
| **Express** | Framework REST | Simplifica roteamento e tratamento de requisições HTTP |
| **MariaDB** | Banco relacional | Armazenamento estruturado com SQL padrão e constraints |
| **mysql2** | Driver Node ↔ DB | Biblioteca oficial para queries SQL via Node.js |
| **dotenv** | Variáveis de ambiente | Isola credenciais sensíveis fora do código-fonte |
| **React** | Interface web | Componentização e gerenciamento de estado reativo |
| **Axios** | Cliente HTTP | Simplifica chamadas à API REST no front-end |
| **Git** | Controle de versão | Rastreia alterações, trabalho em equipe, GitHub |

---

## 3. Pré-requisitos

- Git (versão 2.x ou superior)
- Node.js 18 LTS ou superior (inclui npm)
- MariaDB 10.2 ou superior
- VS Code (editor recomendado)

---

## 4. Preparação do Ambiente (Windows)

### 4.1 Instalar o Git

Acesse https://git-scm.com/download/win e baixe o instalador. Mantenha todas as opções padrão.

```bash
git --version    # Resultado esperado: git version 2.x.x
```

> **Por que Git?** Registra o histórico de alterações, permite trabalho em equipe e publica o código no GitHub.

---

### 4.2 Instalar o Node.js

Acesse https://nodejs.org e baixe a versão **LTS**. Durante a instalação, marque a opção **"Add to PATH"**. Feche e reabra o terminal após instalar.

```bash
node --version   # Resultado esperado: v18.x.x ou superior
npm --version    # Resultado esperado: 9.x.x ou superior
```

> **Por que Node.js?** Permite executar JavaScript no servidor. Base para rodar o Express e gerenciar pacotes via npm.

---

### 4.3 Instalar o MariaDB

Acesse https://mariadb.org/download/. Selecione Windows e baixe o instalador MSI. Durante a instalação, defina e **anote a senha do usuário root** — será usada no arquivo `.env`.

```bash
mysql --version  # Resultado esperado: mysql Ver 15.1 ...
```

---

### 4.4 Instalar o VS Code

Acesse https://code.visualstudio.com/. Extensões recomendadas: **ESLint**, **Prettier**, **GitLens**.

---

## 5. Instalação do Projeto

### 5.1 Clonar o Repositório

```bash
cd C:\Users\SEU_USUARIO\Documents
git clone https://github.com/seu-usuario/projeto-credito.git
cd projeto-credito
```

### 5.2 Instalar Dependências do Back-end

O comando `npm install` lê o `package.json` e baixa todos os pacotes para a pasta `node_modules`.

```bash
cd backend
npm install
```

### 5.3 Instalar Dependências do Front-end

```bash
cd ..\frontend
npm install
```

---

## 6. Configuração de Variáveis de Ambiente

Variáveis de ambiente armazenam dados sensíveis fora do código-fonte. O arquivo `.env` nunca deve ser enviado ao GitHub — ele já está listado no `.gitignore`.

```bash
cd backend
copy .env.example .env
```

Abra o arquivo `.env` no VS Code e preencha com suas credenciais:

```env
PORT=3001
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=SUA_SENHA_DO_MARIADB
DB_NAME=credito_db
NODE_ENV=development
```

> ⚠️ **O arquivo `.env` NUNCA deve ser enviado ao GitHub. Ele já está no `.gitignore`.**

---

## 7. Configuração do Banco de Dados

Execute o script SQL para criar o banco, a tabela e os dados de exemplo:

```bash
mysql -u root -p < backend\database.sql
```

Ou dentro do cliente MySQL:

```sql
source C:/caminho/para/projeto-credito/backend/database.sql
```

Isso irá criar o banco `credito_db`, a tabela `solicitacoes` com constraints e inserir 3 registros de exemplo.

---

## 8. Como Rodar o Projeto

### 8.1 Iniciar o Back-end

```bash
cd backend
npm run dev
```

✅ Saída esperada: `Servidor rodando na porta 3001` | Acesse: http://localhost:3001/health

### 8.2 Iniciar o Front-end

Abra um **novo terminal** (sem fechar o do back-end):

```bash
cd frontend
npm start
```

✅ O navegador abrirá automaticamente em: http://localhost:3000

---

## 9. Estrutura de Pastas

| Arquivo | Responsabilidade |
|---|---|
| `backend/src/config/database.js` | Pool de conexões com MariaDB |
| `backend/src/routes/` | Mapeamento dos endpoints REST |
| `backend/src/controllers/` | Recebe req/res HTTP, chama service |
| `backend/src/services/` | Regras de negócio e validações |
| `backend/src/models/` | Único ponto de acesso ao banco |
| `backend/src/app.js` | Configuração do Express e middlewares |
| `backend/src/server.js` | Ponto de entrada da aplicação |
| `backend/database.sql` | Script de criação do banco |
| `frontend/src/App.js` | Estado global e handlers React |
| `frontend/src/services/api.js` | Chamadas Axios à API |
| `frontend/src/components/FormSolicitacao.js` | Formulário com validação local |
| `frontend/src/components/ListaSolicitacoes.js` | Lista com badges e ações |

---

## 10. Endpoints da API REST

| Método | Rota | Descrição | Status |
|---|---|---|---|
| `POST` | `/solicitacoes` | Criar solicitação | 201 Created |
| `GET` | `/solicitacoes` | Listar todas | 200 OK |
| `GET` | `/solicitacoes/:id` | Buscar por ID | 200 OK |
| `PUT` | `/solicitacoes/:id` | Atualizar status | 200 OK |
| `DELETE` | `/solicitacoes/:id` | Remover | 200 OK |
| `GET` | `/health` | Health check | 200 OK |

---

## 11. Versionamento com Git e GitHub

### Configuração inicial (apenas uma vez)

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

### Inicializar e subir o repositório

```bash
git init
git add .
git commit -m "feat: estrutura inicial do projeto CRUD"
git remote add origin https://github.com/seu-usuario/projeto-credito.git
git branch -M main
git push -u origin main
```

### Fluxo de trabalho diário

```bash
git status                                     # Verifica o que foi alterado
git add .                                      # Prepara arquivos para commit
git commit -m "feat: nova funcionalidade"      # Registra o snapshot
git push                                       # Envia para o GitHub
```

### Convenção de mensagens de commit

- `feat:` — nova funcionalidade
- `fix:` — correção de bug
- `docs:` — atualização de documentação
- `refactor:` — melhoria sem mudança de comportamento