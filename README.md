# 🏗️ Laravel Docker - Monorepo

Projeto Laravel API com arquitetura de microserviços usando Docker. Estrutura de monorepo pronta para desenvolvimento com backend (Laravel) e frontend separados.

---

## 📋 Índice

- [Visão Geral da Arquitetura](#-visão-geral-da-arquitetura)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Tecnologias](#-tecnologias)
- [Como Começar](#-como-começar)
- [Diagrama de Containers](#-diagrama-de-containers)
- [Fluxo de Requisição](#-fluxo-de-requisição)
- [Documentação Detalhada](#-documentação-detalhada)

---

## 🎯 Visão Geral da Arquitetura

Este projeto implementa uma **arquitetura de microserviços** usando Docker, com separação clara entre backend (API) e frontend. O backend é uma **API Laravel 12** com autenticação via **Laravel Sanctum**, rodando em containers Docker totalmente configurados.

### Características Principais

- ✅ **Monorepo**: Backend e frontend em um único repositório
- ✅ **Dockerizado**: Todos os serviços rodando em containers isolados
- ✅ **Hot Reload**: Alterações no código refletem imediatamente
- ✅ **450+ Comandos Make**: Automação completa (Docker, Laravel, Git, Frontend, Qualidade)
- ✅ **Multi Database**: Suporte para MySQL 8.0, PostgreSQL 18 e MongoDB 8.0
- ✅ **API-First**: Backend preparado para consumo por qualquer frontend
- ✅ **Autenticação**: Laravel Sanctum pré-configurado
- ✅ **Frontend Ready**: Makefile completo para Vue, React, Next.js, Nuxt e outros
- ✅ **Qualidade de Código**: PHP Insights, PHPStan, PHP CS Fixer, Pint, PHPMD, Psalm
- ✅ **Documentação API**: Scramble, Swagger, Scribe integrados

---

## 📁 Estrutura do Projeto

```
laravel-docker-micro/
│
├── 📄 README.md                 # ← Este arquivo (Arquitetura geral)
│
├── 📂 backend/                  # Backend - Laravel API
│   ├── 📄 README.md             # Documentação completa do backend
│   ├── 📄 Makefile              # 450+ comandos de automação (modular)
│   ├── 📄 docker-compose.yml    # Orquestração dos containers
│   │
│   ├── 📂 makefiles/            # Módulos do Makefile (14 arquivos)
│   │   ├── Makefile.docker      # Docker Compose básico
│   │   ├── Makefile.laravel     # Laravel Artisan
│   │   ├── Makefile.git         # Git (70+ comandos)
│   │   ├── Makefile.quality     # Qualidade de código (44 comandos)
│   │   └── ...                  # +10 módulos especializados
│   │
│   ├── 📂 docker/               # Configurações Docker
│   │   ├── 📂 php/              # PHP-FPM 8.4
│   │   ├── 📂 nginx/            # Nginx
│   │   ├── 📂 mysql/            # MySQL 8.0
│   │   ├── 📂 postgres/         # PostgreSQL 18
│   │   └── 📂 mongodb/          # MongoDB 8.0 (configs opcionais)
│   │
│   └── 📂 laravel/              # Aplicação Laravel 12
│       ├── app/
│       ├── config/
│       ├── database/
│       ├── routes/
│       └── ...
│
└── 📂 frontend/                 # Frontend - Frameworks e Ferramentas
    ├── 📄 README.md             # Documentação completa do frontend
    ├── 📄 Makefile              # 40+ comandos para frontend (Vue, React, etc.)
    └── 📄 ...                   # Projetos frontend criados aqui
```

### Organização dos Volumes

O projeto Laravel fica em `backend/laravel/` e é montado em `/var/www` dentro dos containers:

```yaml
# backend/docker-compose.yml
volumes:
  - ./laravel:/var/www
```

Isso permite:
- **Hot-reload**: Alterações no código aparecem instantaneamente
- **Separação**: Docker configs ficam em `backend/docker/`
- **Organização**: Código Laravel isolado em `backend/laravel/`

---

## 🛠️ Tecnologias

### Backend

| Tecnologia | Versão | Descrição |
|-----------|--------|-----------|
| **PHP** | 8.4 | Linguagem de programação |
| **Laravel** | 12.x | Framework PHP (API Mode) |
| **Laravel Sanctum** | 4.2 | Autenticação de API com tokens |
| **MySQL** | 8.0 | Banco de dados relacional |
| **PostgreSQL** | 18 (Alpine) | Banco de dados relacional (mais recente) |
| **MongoDB** | 8.0 | Banco de dados NoSQL |
| **Redis** | Alpine | Cache e gerenciamento de filas |
| **Nginx** | Alpine | Servidor web reverse proxy |
| **Mailpit** | Latest | Servidor SMTP para testes de email |

> **Escolha seu banco:** Configure MySQL, PostgreSQL ou MongoDB através do arquivo `.env` do Laravel.

### DevOps

- **Docker** (20.10+): Container runtime
- **Docker Compose** (2.0+): Orquestração de containers
- **Make**: Automação com 450+ comandos organizados em 14 módulos
- **Ferramentas de Qualidade**: PHP Insights, PHPStan, PHP CS Fixer, Laravel Pint, PHPMD, Psalm
- **Documentação API**: Scramble, Swagger (L5-Swagger), Scribe, phpDocumentor

---

## 🚀 Como Começar

### Pré-requisitos

- Docker (versão 20.10 ou superior)
- Docker Compose (versão 2.0 ou superior)
- Make (opcional, mas recomendado)

### Instalação - Método Automático (Recomendado)

```bash
# 1. Acesse a pasta do backend
cd backend

# 2. Inicialize o projeto (faz tudo automaticamente)
make init-project
```

Esse comando irá:
1. ✅ Verificar estrutura de pastas
2. ✅ Construir e iniciar os containers
3. ✅ Instalar dependências do Laravel
4. ✅ Configurar variáveis de ambiente
5. ✅ Gerar chave da aplicação
6. ✅ Executar migrations
7. ✅ Configurar permissões

### Instalação - Método Manual

```bash
cd backend

# 1. Subir containers
make up

# 2. Configurar Laravel
make setup

# 3. Executar migrations
make migrate
```

### Acessar a Aplicação

Após a instalação:

- **API Laravel**: http://localhost:8080
- **Endpoint de teste**: http://localhost:8080/api
- **Mailpit (Web UI)**: http://localhost:32770

---

## 🐳 Diagrama de Containers

```
┌───────────────────────────────────────────────────────────────┐
│                   Docker Network                              │
│               setup-laravel-network                           │
│                                                               │
│  ┌────────────┐    ┌────────────┐    ┌───────────────────┐    │
│  │            │    │            │    │                   │    │
│  │   Nginx    │───▶│  PHP-FPM   │───▶│  MySQL / Postgres │    │
│  │  (Alpine)  │    │   (8.4)    │    │   (8.0 / 18)      │    │
│  │            │    │            │    │                   │    │
│  │ Port: 8080 │    │ Port: 9000 │    │ Port: 3306/5432   │    │
│  └────────────┘    └──────┬─────┘    └───────────────────┘    │
│                           │                                   │
│                    ┌──────▼──────┐    ┌───────────────────┐   │
│                    │             │    │                   │   │
│                    │   Redis     │    │     MongoDB       │   │
│                    │  (Alpine)   │    │      (8.0)        │   │
│                    │             │    │                   │   │
│                    │ Port: 6379  │    │ Port: 27017       │   │
│                    └─────────────┘    └───────────────────┘   │
│                                                               │
│  ┌────────────┐                                               │
│  │            │                                               │
│  │  Mailpit   │                                               │
│  │ (Latest)   │                                               │
│  │            │                                               │
│  │Port: 32770 │ (Web UI)                                      │
│  │Port: 1025  │ (SMTP)                                        │
│  └────────────┘                                               │
│                                                               │
└───────────────────────────────────────────────────────────────┘
```

### Comunicação entre Containers

Os containers se comunicam através de uma **rede Docker interna**:

- **Nginx** ↔ **PHP-FPM**: FastCGI (porta 9000)
- **PHP-FPM** ↔ **MySQL/Postgres**: Conexão TCP (3306/5432)
- **PHP-FPM** ↔ **MongoDB**: Conexão TCP (27017)
- **PHP-FPM** ↔ **Redis**: Conexão TCP (6379)
- **PHP-FPM** ↔ **Mailpit**: SMTP (porta 1025)

---

## 🔄 Fluxo de Requisição

```
Cliente (Browser/Postman/Frontend)
        │
        │ HTTP Request (Port 8080)
        ▼
┌────────────────┐
│     Nginx      │  ← Recebe requisição HTTP
│  (Web Server)  │  ← Serve arquivos estáticos
└───────┬────────┘  ← Roteamento
        │
        │ FastCGI (Port 9000)
        ▼
┌────────────────┐
│    PHP-FPM     │  ← Executa código Laravel
│ (Application)  │  ← Lógica de negócio + Eloquent ORM
└───────┬────────┘  ← Processa requisição
        │
        ├──────────┬───────────┬─────────────┬────────────┐
        │          │           │             │            │
        ▼          ▼           ▼             ▼            ▼
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│  MySQL   │ │Postgres  │ │ MongoDB  │ │  Redis   │ │ Mailpit  │
│(Database)│ │(Database)│ │(Database)│ │  (Cache) │ │  (Mail)  │
│          │ │          │ │          │ │          │ │          │
│Port:3306 │ │Port:5432 │ │Port:27017│ │Port:6379 │ │Port:1025 │
└──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘
        │          │          │             │             │
        └──────────┴──────────┴─────────────┴─────────────┘
                              │
                        JSON Response
                              │
                              ▼
                           Cliente
```

### Detalhes do Fluxo

1. **Cliente** envia requisição HTTP para `http://localhost:8080/api/endpoint`
2. **Nginx** recebe e verifica se é arquivo estático ou código PHP
3. **PHP-FPM** processa a requisição através do Laravel
4. **Laravel** acessa banco de dados (MySQL/Postgres/MongoDB) ou cache (Redis)
5. **Resposta JSON** retorna através de Nginx para o cliente

---

## 📚 Documentação Detalhada

### Para Desenvolvedores Backend

👉 **[backend/README.md](backend/README.md)**

Contém:
- ✅ Guia completo de uso do backend
- ✅ **450+ comandos Make organizados em 14 módulos** (Docker, Laravel Artisan, Git, Qualidade)
- ✅ Estrutura modular do Makefile (makefiles/)
- ✅ Configuração de banco de dados (MySQL/PostgreSQL/MongoDB)
- ✅ Como criar controllers, models, migrations, etc.
- ✅ **44 comandos de qualidade de código** (PHP Insights, PHPStan, PHP CS Fixer, Pint, PHPMD, Psalm)
- ✅ **Documentação API** (Scramble, Swagger, Scribe, phpDocumentor)
- ✅ Troubleshooting e debugging
- ✅ Configurações de cache, queue, email
- ✅ Integração com Redis e Mailpit
- ✅ Comandos Git para versionamento (70+ comandos)
- ✅ Testes e CI/CD

### Para Desenvolvedores Frontend

👉 **[frontend/README.md](frontend/README.md)**

Contém:
- ✅ **40+ comandos Make** para criação de projetos (Vue, React, Next.js, Nuxt, Angular, Svelte, etc.)
- ✅ Como integrar com a API Laravel
- ✅ Autenticação com Laravel Sanctum
- ✅ Exemplos de requisições e integração
- ✅ CORS e configurações
- ✅ **Guia completo de Laravel Livewire** (alternativa fullstack)
- ✅ Comandos para componentes, páginas, stores, composables
- ✅ Setup de TypeScript, ESLint, Prettier, Tailwind CSS

---

## 🎯 Casos de Uso

### Desenvolvimento de API REST

O backend está configurado como **API pura**:

```bash
# Criar um endpoint completo
cd backend
make make-model-full name=Post

# Isso cria:
# - Model (app/Models/Post.php)
# - Migration (database/migrations/xxx_create_posts_table.php)
# - Factory (database/factories/PostFactory.php)
# - Seeder (database/seeders/PostSeeder.php)
# - Controller (app/Http/Controllers/PostController.php)
```

### Integração com Frontend

O frontend pode ser qualquer tecnologia:

- ✅ **React** / Next.js
- ✅ **Vue.js** / Nuxt
- ✅ **Angular**
- ✅ **Svelte** / SvelteKit
- ✅ **Mobile** (React Native, Flutter)

A autenticação é feita via **Laravel Sanctum** com tokens:

```javascript
// Exemplo de requisição do frontend
const response = await fetch('http://localhost:8080/api/posts', {
  headers: {
    'Authorization': 'Bearer ' + token,
    'Accept': 'application/json'
  }
});
```

### Criar Projeto Frontend

O diretório `frontend/` inclui um Makefile completo com 40+ comandos:

```bash
cd frontend

# Criar projetos
make create-vue      # Vue 3 com Vite
make create-react    # React com Vite
make create-next     # Next.js
make create-nuxt     # Nuxt 3

# Ver todos os comandos
make help
```

Veja detalhes completos em **[frontend/README.md](frontend/README.md)**.

---

## 🔧 Comandos Rápidos

```bash
cd backend

# Iniciar ambiente
make up              # Sobe todos os containers
make down            # Para todos os containers

# Desenvolvimento
make bash            # Acessa container PHP
make logs            # Mostra logs em tempo real
make tinker          # Laravel Tinker

# Banco de dados
make migrate         # Executa migrations
make seed            # Executa seeders
make fresh           # Recria banco com seed

# Testes
make test            # Executa testes PHPUnit
make test-coverage   # Testes com cobertura

# Status
make status          # Status completo do ambiente
make health          # Health check dos serviços
make info            # Informações detalhadas

# Qualidade de código
make quality-check   # Verifica qualidade (PHP Insights, PHPStan, etc.)
make quality-fix     # Corrige problemas automaticamente
make phpinsights-analyze  # Análise com PHP Insights
make phpstan-analyze      # Análise estática com PHPStan

# Documentação API
make scramble-generate    # Gera documentação OpenAPI (Scramble)
make swagger-generate    # Gera documentação Swagger
make scribe-generate     # Gera documentação com Scribe

# Frontend
cd ../frontend
make help            # Lista 40+ comandos frontend
make create-vue      # Cria projeto Vue 3
make create-react    # Cria projeto React
make create-next     # Cria projeto Next.js

# Ver todos os comandos
make help            # Lista 450+ comandos disponíveis
```

---

## 🗄️ Bancos de Dados

O projeto suporta **MySQL 8.0**, **PostgreSQL 18** (a versão mais recente, lançada em setembro de 2025) e **MongoDB 8.0**.

### Como Escolher

Edite `backend/laravel/.env`:

**Para MySQL:**
```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
```

**Para PostgreSQL:**
```env
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
```

**Para MongoDB:**
```env
DB_CONNECTION=mongodb
DB_HOST=mongodb
DB_PORT=27017
```

### Credenciais Padrão

| Banco | Usuário | Senha | Database |
|-------|---------|-------|----------|
| MySQL | developer | 123456 | db_laravel |
| PostgreSQL | developer | 123456 | db_laravel |
| MongoDB | developer | 123456 | db_laravel |

### Por que PostgreSQL 18?

- ⚡ **I/O até 3x mais rápido**
- 📦 **Melhor manuseio de JSON**
- 🔄 **Replicação lógica melhorada**
- 💾 **Gerenciamento de memória otimizado**

### Por que MongoDB 8.0?

- 📄 **Documentos flexíveis** - Ideal para dados não estruturados
- 🚀 **Alta performance** - Escalabilidade horizontal
- 🔍 **Consultas poderosas** - Suporte a queries complexas
- 💾 **Armazenamento eficiente** - Otimizado para big data

Veja detalhes completos em **[backend/README.md](backend/README.md)**.

---

## 🔐 Segurança

### PHP

- `expose_php = Off` - Oculta versão do PHP
- `display_errors = Off` - Não expõe erros em produção
- `allow_url_fopen = Off` - Previne RFI
- `allow_url_include = Off` - Previne inclusão remota
- Session cookies com `httponly` e `secure`

### Laravel

- Laravel Sanctum para autenticação de API
- CSRF protection habilitado
- Rate limiting configurado
- Variáveis sensíveis em `.env` (não versionado)

---

## 📊 Performance

### Otimizações Incluídas

- ✅ **Redis** para cache e sessões
- ✅ **Opcache** habilitado no PHP
- ✅ **Nginx** com compressão gzip
- ✅ **PostgreSQL 18** com I/O otimizado
- ✅ **Volumes Docker** para hot-reload eficiente

### Comandos de Cache

```bash
make cache-clear     # Limpa cache da aplicação
make config-cache    # Cache de configuração
make route-cache     # Cache de rotas
make view-cache      # Cache de views
```

---

## 🆘 Troubleshooting

### Containers não iniciam

```bash
make down
make rebuild
make up
```

### Erro de permissão

```bash
make permissions
```

### Banco de dados não conecta

```bash
make health          # Verifica status dos serviços
make logs-mysql      # Ou logs-postgres ou logs-mongodb
```

### Cache travando

```bash
make clear-all       # Limpa TODOS os caches
```

### Ver logs detalhados

```bash
make logs            # Todos os containers
make logs-php        # Apenas PHP
make logs-nginx      # Apenas Nginx
```

---

## 🤝 Contribuindo

Este projeto é open source e aceita contribuições. Sinta-se livre para:

- Reportar bugs
- Sugerir melhorias
- Enviar pull requests
- Melhorar a documentação

---

## 📞 Suporte

- 📖 **Documentação Backend**: [backend/README.md](backend/README.md)
- 📖 **Documentação Frontend**: [frontend/README.md](frontend/README.md)
- 🐛 **Issues**: Reporte problemas nas issues do GitHub
- 💬 **Discussões**: Use as discussions para dúvidas

---

## 📄 Licença

Este projeto é open source e está disponível sob a licença MIT.

---

## 🎉 Pronto para Começar!

```bash
# Clone o projeto
git clone <seu-repositorio>

# Acesse o backend
cd laravel-docker-micro/backend

# Inicie tudo automaticamente
make init-project

# Aguarde e acesse:
# - API: http://localhost:8080
# - Mailpit: http://localhost:32770
```

**Bom desenvolvimento! 🚀**
