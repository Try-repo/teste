# 🚀 Teste Técnico - Fullstack

## 📌 Objetivo
Criar uma **API REST** para gerenciar pedidos de um **sistema simples de marketplace**, processá-los via mensageria (**RabbitMQ**) e implementar **cache com Redis** para otimizar requisições.

---

## 📂 Estrutura do Projeto

### 📌 O que já está pronto?
✅ **Dockerfile e Docker Compose** (Você pode modificar se necessário).  
✅ **Estrutura base da API (`backend/`)** (Com `package.json`, `tsconfig.json` e diretórios, você pode modificar se necessário).  
✅ **Configuração de banco de dados, Redis e RabbitMQ no Docker**.  
✅ **Diretório `src/` já criado, mas os arquivos principais estão vazios para você implementar**.  

### 📌 O que você precisa fazer?
🔹 **Criar os endpoints na API (`POST /pedidos`, `GET /pedidos/:id`, `GET /pedidos`)**.  
🔹 **Implementar autenticação JWT**.  
🔹 **Configurar a comunicação com RabbitMQ para processar pedidos**.  
🔹 **Adicionar cache no Redis e invalidá-lo quando necessário**.  

### 📌 Estrutura inicial do projeto:
```
fullstack-test/
│── backend/            # API em Node.js (NestJS)
│   │── src/
│   │   │── modules/
│   │   │   ├── pedidos/         # (Você deve criar esse módulo)
│   │   │   ├── auth/            # (Você deve criar esse módulo)
│   │   │── main.ts              # (Arquivo inicial vazio - você deve implementá-lo)
│   │   │── app.module.ts        # (Você deve criar esse módulo principal)
│   │── test/                    # Testes unitários (Opcional)
│   │── Dockerfile               # Dockerfile para API (Pronto, mas você pode modificar)
│   │── package.json             # Dependências do projeto (Pronto , você pode modificar se necessário)
│   │── README.md                # Documentação do backend
│
│── frontend/           # Aplicação Vue.js para consumir a API (Opcional)
│   │── src/
│   │   │── components/
│   │   │── views/
│   │   │── main.js
│   │── public/
│   │── package.json
│   │── README.md
│
│── docker-compose.yml  # Orquestração dos containers (API, PostgreSQL, Redis, RabbitMQ)
│── README.md           # Documentação principal do projeto
```

---

## 📌 Tecnologias Utilizadas
O projeto já possui a base para rodar **NestJS com TypeScript** e depende das seguintes tecnologias:

### **Backend**
- **Node.js (NestJS)** → Framework para API RESTful.
- **TypeScript** → Melhor organização e segurança no código.
- **PostgreSQL** → Banco de dados relacional.
- **Redis** → Para cache de pedidos.
- **RabbitMQ** → Para mensageria e processamento de pedidos.
- **JWT** → Para autenticação segura.
- **Docker & Docker Compose** → Para facilitar o setup local.

### **Frontend (Opcional, mas recomendado)**
- **Vue.js/Nuxt.js** → Interface para listar pedidos e criar novos.
- **Axios** → Consumo da API.
- **Vuetify/Tailwind** → Estilização.

---

## 🚀 O que você precisa implementar?

### 📌 **1️⃣ Backend (API RESTful)**
- Criar **3 endpoints principais**:
  - `POST /pedidos` → Criar um pedido (**autenticado via JWT**).
  - `GET /pedidos/:id` → Buscar detalhes de um pedido (**com cache Redis**).
  - `GET /pedidos` → Listar todos os pedidos.
- Criar **autenticação JWT** para login e acesso aos endpoints.
- O sistema deve persistir os pedidos no **banco de dados (PostgreSQL, já configurado no Docker)**.

### 📌 **2️⃣ Mensageria (RabbitMQ)**
- Quando um pedido for criado (`POST /pedidos`), enviar uma **mensagem para uma fila do RabbitMQ**.
- Criar um **worker** que processa pedidos da fila e atualiza seu status.
- O worker deve **simular o envio de um e-mail ou notificação**.

### 📌 **3️⃣ Cache (Redis)**
- Implementar **cache Redis** para reduzir acessos ao banco no endpoint `GET /pedidos/:id`.
- Quando um pedido for atualizado, **invalidar o cache automaticamente**.

### 📌 **4️⃣ Frontend (Diferencial, mas não obrigatório)**
- Criar um **frontend Vue.js simples** que consome a API:
  - Exibir lista de pedidos.
  - Permitir criar novos pedidos.

---

## 📌 Como enviar sua entrega?
### **1️⃣ Criar uma branch com seu nome**
```sh
git checkout -b nome-sobrenome
```
> **Exemplo:**
> Se o nome do candidato for **João Silva**, ele deve rodar:
> ```sh
> git checkout -b joao-silva
> ```

### **2️⃣ Fazer os commits normalmente**
```sh
git add .
git commit -m "Entrega do teste técnico - Nome Sobrenome"
```

### **3️⃣ Enviar a branch para o repositório**
```sh
git push origin nome-sobrenome
```

### **4️⃣ Criar um Pull Request (PR)**
- Acessar o repositório no GitHub.
- Abrir um **Pull Request (PR)** da sua branch para `main` ou `master`.

---

## 📌 Setup e Rodando o Projeto

### **1️⃣ Clonar o repositório**
```sh
git clone https://github.com/Try-repo/teste.git
cd teste
```

### **2️⃣ Rodar com Docker**
```sh
docker-compose up --build
```
Isso sobe os serviços:
- **Backend (NestJS/Express)** → Porta `3000`
- **Banco de Dados (PostgreSQL)** → Porta `5432`
- **Mensageria (RabbitMQ)** → Porta `5672`
- **Cache (Redis)** → Porta `6379`

### **3️⃣ Testar Endpoints (Exemplo com cURL)**
```sh
# Criar um novo pedido
curl -X POST http://localhost:3000/pedidos -H "Authorization: Bearer <token>" -d '{"produto": "Camiseta", "preco": 100.00}'

# Buscar um pedido específico
curl -X GET http://localhost:3000/pedidos/1 -H "Authorization: Bearer <token>"
```

### **4️⃣ Login (Autenticação JWT)**
```sh
curl -X POST http://localhost:3000/auth/login -d '{"email": "admin@test.com", "password": "123456"}'
```
Isso retorna um **token JWT**, que deve ser usado nas próximas requisições.

---

## ❓ Dúvidas
Caso tenha dúvidas sobre o teste, entre em contato com o recrutador responsável.  
Boa sorte! 🚀
