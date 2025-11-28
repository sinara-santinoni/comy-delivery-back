# 🍕 Comy Delivery - Backend

<div align="center">

![Java](https://img.shields.io/badge/Java-21-orange?style=for-the-badge&logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.7-brightgreen?style=for-the-badge&logo=spring)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14+-blue?style=for-the-badge&logo=postgresql)
![Maven](https://img.shields.io/badge/Maven-3.9+-red?style=for-the-badge&logo=apache-maven)

Sistema de delivery de comida desenvolvido com Spring Boot, oferecendo APIs REST completas para gerenciamento de restaurantes, pedidos, entregas e clientes.

[Sobre](#-sobre-o-projeto) • [Tecnologias](#-tecnologias-utilizadas) • [Instalação](#️-instalação-e-configuração) • [Como Rodar](#️-como-rodar-o-projeto) • [API](#-documentação-da-api) • [Equipe](#-equipe-de-desenvolvimento)

</div>

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Configuração](#️-instalação-e-configuração)
- [Como Rodar o Projeto](#️-como-rodar-o-projeto)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Funcionalidades Principais](#-funcionalidades-principais)
- [Documentação da API](#-documentação-da-api)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)
- [Banco de Dados](#️-banco-de-dados)
- [Testando a API](#-testando-a-api)
- [Troubleshooting](#-troubleshooting)
- [Scripts Úteis](#-scripts-úteis)
- [Equipe de Desenvolvimento](#-equipe-de-desenvolvimento)

---

## 🎯 Sobre o Projeto

O **Comy Delivery** é uma plataforma completa de delivery que conecta restaurantes, clientes e entregadores. O sistema oferece funcionalidades robustas como:

- 🔄 Gestão de pedidos em tempo real
- 📍 Cálculo automático de frete baseado em distância
- 🎟️ Sistema de cupons de desconto
- ⭐ Avaliações de restaurantes e entregadores
- 📧 Recuperação de senha por e-mail
- 🕐 Controle automático de abertura/fechamento de restaurantes

---

## 🚀 Tecnologias Utilizadas

| Tecnologia | Versão | Descrição |
|------------|--------|-----------|
| **Java** | 21 | Linguagem principal |
| **Spring Boot** | 3.5.7 | Framework backend |
| **Spring Data JPA** | - | Persistência de dados |
| **Spring Validation** | - | Validação de dados |
| **Spring Cloud OpenFeign** | - | Cliente HTTP declarativo |
| **PostgreSQL** | 14+ | Banco de dados relacional |
| **Lombok** | - | Redução de boilerplate |
| **BCrypt** | - | Criptografia de senhas |
| **JavaMailSender** | - | Envio de e-mails |
| **Springdoc OpenAPI** | - | Documentação Swagger |
| **Maven** | 3.9+ | Gerenciamento de dependências |

---

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- ☕ **Java 21** ou superior → [Download](https://www.oracle.com/java/technologies/downloads/#java21)
- 📦 **Maven 3.9+** (ou use o Maven Wrapper incluído)
- 🐘 **PostgreSQL 14+** → [Download](https://www.postgresql.org/download/)
- 🔧 **Git** → [Download](https://git-scm.com/)
- 💻 **IDE** de sua preferência (IntelliJ IDEA, Eclipse, VS Code)

---

## ⚙️ Instalação e Configuração

### 1️⃣ Clone o Repositório

```bash
git clone https://github.com/seu-usuario/comy-delivery-back.git
cd comy-delivery-back
```

### 2️⃣ Configure o Banco de Dados

Crie um banco de dados PostgreSQL:

```sql
CREATE DATABASE comy_delivery;
```

### 3️⃣ Configure as Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```properties
# Banco de Dados
DATABASE_URL=jdbc:postgresql://localhost:5432/comy_delivery
DATABASE_USERNAME=seu_usuario
DATABASE_PASSWORD=sua_senha

# E-mail (Gmail)
EMAIL_SENDER=seu_email@gmail.com
SENHA_EMAIL_SENDER=sua_senha_app

# API Externa (AwesomeAPI - CEP)
AWESOMEAPI_KEY=sua_chave_api

# URLs (Opcional - valores padrão)
FRONTEND_URL=http://localhost:4200
BACKEND_URL=http://localhost:8084
PASSWORD_RECOVERY_URL=http://localhost:4200/reset-password?
```

### 📧 Configuração do Gmail

Para usar o envio de e-mails via Gmail:

1. Acesse sua [Conta Google](https://myaccount.google.com/)
2. Vá em **Segurança** → **Verificação em duas etapas** (ative se necessário)
3. Em **Senhas de app**, gere uma nova senha
4. Use essa senha na variável `SENHA_EMAIL_SENDER`

### 4️⃣ Instale as Dependências

```bash
# Linux/Mac
./mvnw clean install

# Windows
mvnw.cmd clean install
```

---

## ▶️ Como Rodar o Projeto

### Opção 1: Maven Wrapper (Recomendado)

```bash
# Linux/Mac
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

### Opção 2: Maven Instalado

```bash
mvn spring-boot:run
```

### Opção 3: Rodando o JAR

```bash
# Gerar o JAR
./mvnw clean package

# Executar
java -jar target/comy-delivery-back-0.0.1-SNAPSHOT.jar
```

### Opção 4: Pela IDE

1. Abra o projeto na sua IDE
2. Localize `ComyDeliveryBackApplication.java`
3. Clique com o botão direito → **Run**

---

## 🌐 Acessando a Aplicação

Após iniciar o servidor:

| Recurso | URL |
|---------|-----|
| **API Base** | `http://localhost:8084` |
| **Swagger UI** | `http://localhost:8084/swagger-ui.html` |
| **Health Check** | `http://localhost:8084/api/health` |

---

## 📁 Estrutura do Projeto

```
src/main/java/com/comy_delivery_back/
├── client/              # Clientes Feign (APIs externas)
├── configuration/       # Configurações (CORS, Async, Swagger)
├── controller/          # Controllers REST
├── dto/                 # DTOs (Request/Response)
│   ├── request/
│   └── response/
├── enums/               # Enumerações (Status, Tipos, Categorias)
├── exception/           # Exceções customizadas
├── model/               # Entidades JPA
├── repository/          # Repositórios Spring Data
├── scheduler/           # Tarefas agendadas
├── security/            # Configurações de segurança
├── service/             # Lógica de negócio
└── utils/               # Classes utilitárias
```

---

## 🎯 Funcionalidades Principais

### 👥 Gestão de Usuários
- ✅ Cadastro e autenticação (Clientes, Restaurantes, Entregadores, Admins)
- ✅ Recuperação de senha por e-mail
- ✅ Soft delete (desativação de contas)

### 🍕 Restaurantes
- ✅ Cadastro com imagens (logo e banner)
- ✅ Gestão de horários de funcionamento
- ✅ Sistema de abertura/fechamento automático
- ✅ Catálogo de produtos com categorias
- ✅ Sistema de promoções

### 🛍️ Pedidos
- ✅ Criação com múltiplos itens e adicionais
- ✅ Aplicação de cupons de desconto
- ✅ Cálculo automático de frete por distância
- ✅ Fluxo completo: Pendente → Confirmado → Em Preparo → Pronto → Saiu para Entrega → Entregue
- ✅ Sistema de aceitação/recusa

### 🚚 Entregas
- ✅ Atribuição automática de entregadores
- ✅ Rastreamento em tempo real
- ✅ Cálculo de tempo estimado
- ✅ Dashboard de performance

### 🎟️ Cupons
- ✅ Cupons de valor fixo e percentual
- ✅ Validação automática de validade e limite de uso
- ✅ Requisito de valor mínimo

### ⭐ Avaliações
- ✅ Sistema de avaliação de restaurantes e entregadores
- ✅ Cálculo automático de média

### 📍 Endereços
- ✅ Integração com API de CEP (AwesomeAPI)
- ✅ Busca automática de coordenadas
- ✅ Cálculo de distância (Fórmula de Haversine)
- ✅ Gestão de múltiplos endereços por usuário

---

## 📖 Documentação da API

A documentação completa está disponível via **Swagger UI**: `http://localhost:8084/swagger-ui.html`

### 🔑 Principais Endpoints

#### Restaurantes
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/api/restaurante` | Cadastrar restaurante |
| `GET` | `/api/restaurante/{id}` | Buscar por ID |
| `GET` | `/api/restaurante/abertos` | Listar abertos |
| `PUT` | `/api/restaurante/{id}` | Atualizar dados |

#### Clientes
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/api/cliente` | Cadastrar cliente |
| `GET` | `/api/cliente/{id}` | Buscar por ID |
| `POST` | `/api/cliente/recuperar-senha` | Recuperar senha |
| `GET` | `/api/cliente/{id}/restaurantes-distancia` | Listar por distância |

#### Pedidos
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/api/pedido` | Criar pedido |
| `GET` | `/api/pedido/{id}` | Buscar por ID |
| `PATCH` | `/api/pedido/{id}/aceitar` | Aceitar/recusar |
| `PATCH` | `/api/pedido/{id}/status` | Atualizar status |
| `GET` | `/api/pedido/restaurante/{id}/dashboard` | Dashboard |

#### Entregas
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/api/entregas` | Cadastrar entrega |
| `PATCH` | `/api/entregas/{id}` | Atualizar status |
| `GET` | `/api/entregas/entregador/{id}/dashboard` | Dashboard |

---

## 🔐 Variáveis de Ambiente

| Variável | Descrição | Obrigatório | Padrão |
|----------|-----------|:-----------:|--------|
| `DATABASE_URL` | URL do PostgreSQL | ✅ | - |
| `DATABASE_USERNAME` | Usuário do banco | ✅ | - |
| `DATABASE_PASSWORD` | Senha do banco | ✅ | - |
| `EMAIL_SENDER` | E-mail remetente | ✅ | - |
| `SENHA_EMAIL_SENDER` | Senha de app Gmail | ✅ | - |
| `AWESOMEAPI_KEY` | Chave API de CEP | ✅ | - |
| `FRONTEND_URL` | URL do frontend | ❌ | `http://localhost:4200` |
| `BACKEND_URL` | URL do backend | ❌ | `http://localhost:8084` |
| `PASSWORD_RECOVERY_URL` | URL recuperação senha | ❌ | `http://localhost:4200/reset-password?` |

---

## 🗄️ Banco de Dados

### Inicialização Automática

O projeto utiliza:
- **Hibernate DDL Auto**: `update` (cria/atualiza tabelas automaticamente)
- **data.sql**: Arquivo com dados iniciais

### 🌱 Dados Iniciais (Seed)

Após a primeira execução, o sistema cria:

| Tipo | Usuário | Senha |
|------|---------|-------|
| Admin | `admin_master` | `SenhaForte123` |
| Restaurante | `pizzaria_top` | `SenhaForte123` |
| Cliente | `cliente_joao` | `SenhaForte123` |
| Entregador | `motoboy_carlos` | `SenhaForte123` |

Além de produtos, endereços e um pedido de exemplo.

---

## 🧪 Testando a API

### Usando cURL

```bash
# Health Check
curl http://localhost:8084/api/health

# Buscar restaurante por ID
curl http://localhost:8084/api/restaurante/2
```

### Usando Postman/Insomnia

Importe a collection do Swagger ou acesse diretamente os endpoints documentados.

---

## 🐛 Troubleshooting

### ❌ Erro de Conexão com o Banco

```
org.postgresql.util.PSQLException: Connection refused
```

**Solução:**
1. Verifique se o PostgreSQL está rodando
2. Confirme as credenciais no `.env`
3. Teste a conexão: `psql -U seu_usuario -d comy_delivery`

### ❌ Erro ao Enviar E-mail

```
AuthenticationFailedException
```

**Solução:**
1. Ative a verificação em duas etapas no Gmail
2. Gere uma nova **Senha de App**
3. Use essa senha em `SENHA_EMAIL_SENDER`

### ❌ Porta 8084 já em uso

```
Port 8084 was already in use
```

**Solução:** Altere a porta no `application.properties`:

```properties
server.port=8085
```

---

## 📝 Scripts Úteis

```bash
# Limpar e compilar
./mvnw clean compile

# Rodar testes
./mvnw test

# Gerar JAR sem testes
./mvnw clean package -DskipTests

# Ver árvore de dependências
./mvnw dependency:tree

# Verificar atualizações
./mvnw versions:display-dependency-updates
```

---

## 👥 Equipe de Desenvolvimento

<table>
  <tr>
    <td align="center">
      <b>Arthur</b>
    </td>
    <td align="center">
      <b>Emilio</b>
    </td>
    <td align="center">
      <b>Heloisa</b>
    </td>
    <td align="center">
      <b>Jude</b>
    </td>
    <td align="center">
      <b>Sinara</b>
    </td>
  </tr>
</table>


---

## 📄 Licença

Este projeto é de propriedade da equipe **Comy Delivery**.

---

<div align="center">

⭐ **Desenvolvido com Spring Boot e ❤️**

[⬆ Voltar ao topo](#-comy-delivery---backend)

</div>
