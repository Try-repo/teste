### Estrutura do Projeto Fullstack (Teste Técnico)

#### 📌 **Objetivo**
Criar uma API REST para gerenciar pedidos de um sistema simples de marketplace, processar os pedidos via mensageria (**RabbitMQ**) e implementar cache para otimizar requisições.

---

## 📂 **Estrutura do Projeto**
```
fullstack-test/
│── backend/            # API em Node.js (NestJS)
│   │── src/
│   │   │── modules/
│   │   │   ├── pedidos/         # Módulo de pedidos
│   │   │   ├── auth/            # Módulo de autenticação
│   │   │── main.ts              # Arquivo principal da API
│   │   │── app.module.ts        # Módulo principal
│   │── test/                    # Testes unitários
│   │── Dockerfile               # Dockerfile para API
│   │── package.json             # Dependências do projeto
│   │── README.md                # Documentação do backend
│
│── frontend/           # Aplicação Vue.js para consumir a API
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

## 📌 **Tecnologias Utilizadas**

### Backend
- **Node.js (NestJS ou Express)** → Framework para API
- **TypeScript** → Melhor organização e segurança no código
- **PostgreSQL** → Banco de dados relacional
- **Redis** → Cache de pedidos para otimizar performance
- **RabbitMQ** → Mensageria para processar pedidos em background
- **JWT** → Autenticação segura
- **Docker & Docker Compose** → Para facilitar setup local

### Frontend (Opcional, mas recomendado)
- **Vue.js/Nuxt.js** → Interface simples para listar pedidos
- **Axios** → Consumo de API
- **Vuetify/Tailwind** → Estilização

---

## 🚀 **Requisitos do Teste**

### 📌 **1️⃣ Backend (API RESTful)**
- Criar **3 endpoints principais**:
  - `POST /pedidos` → Criar um pedido (autenticado via JWT)
  - `GET /pedidos/:id` → Buscar detalhes de um pedido (com cache Redis)
  - `GET /pedidos` → Listar todos os pedidos
- Criar **autenticação JWT** (usuário pode logar e acessar pedidos)
- O sistema deve persistir os pedidos no **banco de dados relacional (MySQL ou PostgreSQL)**

### 📌 **2️⃣ Mensageria (RabbitMQ)**
- Quando um pedido for criado (`POST /pedidos`), enviar uma **mensagem para uma fila no RabbitMQ**
- Criar um **worker** que processa pedidos da fila e atualiza seu status
- O worker deve **simular o envio de um e-mail ou notificação**

### 📌 **3️⃣ Cache (Redis)**
- Implementar **cache Redis** para reduzir acessos ao banco de dados no endpoint `GET /pedidos/:id`
- Quando um pedido for atualizado, **invalidar o cache** automaticamente

### 📌 **4️⃣ Frontend (Diferencial, mas não obrigatório)**
- Criar um **frontend Vue.js simples** que consome a API:
  - Exibir lista de pedidos
  - Permitir criar novos pedidos

---

## 🔧 **Setup e Rodando o Projeto**
### **1️⃣ Clonar o repositório**
```sh
git clone https://github.com/Try-repo/teste.git
cd teste
```

### **2️⃣ Rodar com Docker**
```sh
docker-compose up --build
```
Isso sobe os containers:
- **Backend (NestJS/Express)** → Porta `3000`
- **Banco de Dados (MySQL/PostgreSQL)** → Porta `3306`
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
Isso retorna um **token JWT** que pode ser usado nas próximas requisições.

---

## **📈 Pontuação para Avaliação**
| Critério | Pontos |
|-----------------------------|--------|
| API funcional com JWT e CRUD de pedidos | 30 |
| Banco de dados bem estruturado | 15 |
| Uso correto do RabbitMQ (Mensageria) | 20 |
| Cache Redis funcionando corretamente | 10 |
| Docker funcionando com Docker Compose | 10 |
| Frontend Vue.js consumindo API (Opcional) | +10 |

---

