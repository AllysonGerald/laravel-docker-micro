# 🚀 Laravel Backend - Guia Completo

Backend Laravel 12 API com Docker, suportando MySQL 8.0 e PostgreSQL 18, Redis, Nginx e Mailpit.

---

## 📋 Índice

- [Início Rápido](#-início-rápido)
- [Arquitetura](#-arquitetura)
- [Configuração de Banco de Dados](#-configuração-de-banco-de-dados)
- [Comandos Make](#-comandos-make)
- [Desenvolvimento](#-desenvolvimento)
- [Testes](#-testes)
- [Deploy](#-deploy)
- [Troubleshooting](#-troubleshooting)

---

## ⚡ Início Rápido

### Pré-requisitos

- Docker (versão 20.10+)
- Docker Compose (versão 2.0+)
- Make (opcional, mas recomendado)

### Primeira Instalação

```bash
# 1. Acesse a pasta backend
cd backend

# 2. Execute o setup automático
make init-project
```

Esse comando faz **tudo automaticamente**:
1. ✅ Constrói e inicia containers
2. ✅ Instala dependências do Composer
3. ✅ Copia e configura arquivo `.env`
4. ✅ Gera chave da aplicação
5. ✅ Executa migrations
6. ✅ Configura permissões

### Acesse a Aplicação

- **API**: http://localhost:8080
- **API Test Endpoint**: http://localhost:8080/api
- **Mailpit (Email Testing)**: http://localhost:32770

---

## 🏗️ Arquitetura

### Containers Docker

| Container | Tecnologia | Porta | Descrição |
|-----------|-----------|-------|-----------|
| **PHP** | PHP 8.4-FPM | 9000 | Aplicação Laravel |
| **Nginx** | Nginx Alpine | 8080 | Servidor web |
| **MySQL** | MySQL 8.0 | 3306 | Banco de dados |
| **PostgreSQL** | PostgreSQL 18 | 5432 | Banco de dados (alternativo) |
| **Redis** | Redis Alpine | 6379 | Cache e filas |
| **Mailpit** | Latest | 32770 (UI)<br>1025 (SMTP) | Teste de emails |

### Estrutura de Pastas

```
backend/
├── 📄 Makefile                 # 450+ comandos de automação (modular)
├── 📄 docker-compose.yml       # Orquestração Docker
│
├── 📂 makefiles/               # Módulos do Makefile (14 arquivos)
│   ├── Makefile.docker         # Docker Compose básico
│   ├── Makefile.docker-advanced # Docker avançado
│   ├── Makefile.laravel        # Laravel Artisan básico
│   ├── Makefile.laravel-make   # Comandos make (generators)
│   ├── Makefile.architecture   # Arquitetura avançada (Repository, Service, etc.)
│   ├── Makefile.database       # Banco de dados (migrations, backups)
│   ├── Makefile.git            # Git (70+ comandos)
│   ├── Makefile.packages       # Laravel packages (Sanctum, Telescope, etc.)
│   ├── Makefile.queue          # Queue e schedule
│   ├── Makefile.tests          # Testes
│   ├── Makefile.maintenance    # Manutenção e otimização
│   ├── Makefile.setup          # Setup e workflows
│   └── Makefile.utils          # Utilitários diversos
│
├── 📂 docker/                  # Configurações Docker
│   ├── php/
│   │   ├── dockerfile          # PHP 8.4 + extensões
│   │   └── local.ini          # Config PHP
│   ├── nginx/
│   │   ├── dockerfile
│   │   └── default.conf       # Config Nginx
│   ├── mysql/
│   │   └── my.cnf             # Config MySQL
│   └── postgres/
│       └── postgresql.conf    # Config PostgreSQL
│
└── 📂 laravel/                 # Aplicação Laravel 12
    ├── app/
    │   ├── Http/
    │   │   └── Controllers/
    │   ├── Models/
    │   └── ...
    ├── config/
    ├── database/
    │   ├── migrations/
    │   ├── seeders/
    │   └── factories/
    ├── routes/
    │   └── api.php            # Rotas da API
    ├── storage/
    ├── tests/
    ├── .env                   # Configurações (não versionado)
    ├── .env.example
    ├── artisan
    └── composer.json
```

### Mapeamento de Volumes

```yaml
# O Laravel está em backend/laravel/ e é montado em /var/www
volumes:
  - ./laravel:/var/www
```

**Isso significa:**
- Alterações no código refletem imediatamente (hot-reload)
- Você edita em `backend/laravel/`
- O container vê em `/var/www/`

---

## 🗄️ Configuração de Banco de Dados

O projeto suporta **MySQL 8.0** e **PostgreSQL 18** (lançado em setembro/2025).

### Escolhendo o Banco

Edite o arquivo `laravel/.env`:

**Para MySQL (padrão):**
```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_laravel
DB_USERNAME=developer
DB_PASSWORD=123456
```

**Para PostgreSQL:**
```env
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=db_laravel
DB_USERNAME=developer
DB_PASSWORD=123456
```

### Credenciais

| Banco | Tipo | Usuário | Senha | Database |
|-------|------|---------|-------|----------|
| **MySQL** | Developer | developer | 123456 | db_laravel |
| **MySQL** | Root | root | root | - |
| **PostgreSQL** | Developer | developer | 123456 | db_laravel |
| **PostgreSQL** | Superuser | postgres | (sem senha) | - |

### PostgreSQL 18 - Por que usar?

O PostgreSQL 18 é a **versão mais recente** (setembro/2025) e traz melhorias significativas:

| Recurso | Melhoria |
|---------|----------|
| **I/O Performance** | Até **3x mais rápido** |
| **JSON** | Manuseio aprimorado de JSON/JSONB |
| **Replicação** | Lógica mais confiável |
| **Memória** | Uso otimizado de recursos |
| **Upgrade** | Processo simplificado |

**Compatibilidade:**
- ✅ 100% compatível com Laravel 12
- ✅ Retrocompatível com PostgreSQL 17 e anteriores
- ✅ Todas as extensões PHP incluídas (pdo_pgsql, pgsql)

### Como Trocar de Banco

```bash
# 1. Parar containers
make down

# 2. Editar laravel/.env
# Altere DB_CONNECTION para mysql ou pgsql

# 3. Subir containers
make up

# 4. Executar migrations
make migrate
```

### Comandos de Banco de Dados

**MySQL:**
```bash
make db              # Conecta como root
make db-dev          # Conecta como developer
make bash-mysql      # Acessa bash do container
make logs-mysql      # Mostra logs
make restart-mysql   # Reinicia container
```

**PostgreSQL:**
```bash
make psql            # Conecta como developer
make psql-root       # Conecta como postgres
make bash-postgres   # Acessa bash do container
make logs-postgres   # Mostra logs
make restart-postgres # Reinicia container
```

**MongoDB:**
```bash
make mongo           # Conecta ao MongoDB (developer)
make mongo-root      # Conecta ao MongoDB (root)
make bash-mongodb    # Acessa bash do container
make logs-mongodb    # Mostra logs
make restart-mongodb # Reinicia container
```

**Redis:**
```bash
make redis-cli       # Acessa Redis CLI
make logs-redis      # Mostra logs
make restart-redis   # Reinicia container
```

---

## 🛠️ Comandos Make

O projeto inclui **450+ comandos** organizados em **14 módulos especializados** para facilitar a manutenção e navegação. A estrutura modular permite encontrar comandos rapidamente e manter o código organizado.

### Estrutura Modular

O Makefile principal (`backend/Makefile`) inclui automaticamente os seguintes módulos:

| Módulo | Descrição | Comandos |
|--------|-----------|----------|
| `Makefile.docker` | Docker Compose básico | up, down, restart, logs, bash |
| `Makefile.docker-advanced` | Docker avançado | volumes, networks, images, containers |
| `Makefile.laravel` | Laravel Artisan básico | tinker, route-list, about |
| `Makefile.laravel-make` | Generators (make commands) | make-model, make-controller, etc. |
| `Makefile.architecture` | Padrões arquiteturais | Repository, Service, Action, DTO, Module |
| `Makefile.database` | Banco de dados | migrations, backups, operações MySQL/Postgres/MongoDB |
| `Makefile.git` | Git (70+ comandos) | status, commit, push, branch, stash |
| `Makefile.packages` | Laravel packages | Sanctum, Telescope, Horizon, Passport, Scout |
| `Makefile.queue` | Queue e schedule | queue-work, schedule-run |
| `Makefile.tests` | Testes | test, test-coverage, pest, phpunit |
| `Makefile.maintenance` | Manutenção | cache, otimização, logs, limpeza |
| `Makefile.setup` | Setup e workflows | setup, init-project, workflows rápidos |
| `Makefile.utils` | Utilitários | composer, NPM, debug, tabelas úteis |
| `Makefile.quality` | Qualidade de código | PHP Insights, PHPStan, PHP CS Fixer, Pint, PHPMD, Psalm |

### Ver Todos os Comandos

```bash
make help
```

### Vantagens da Estrutura Modular

- ✅ **Organização**: Cada módulo tem uma responsabilidade específica
- ✅ **Manutenção**: Fácil encontrar e editar comandos
- ✅ **Escalabilidade**: Adicione novos comandos nos módulos corretos
- ✅ **Navegação**: Arquivos menores e mais legíveis

### Comandos Essenciais do Dia a Dia

#### 🐳 Docker (Containers)

```bash
make up              # Inicia todos os containers
make down            # Para todos os containers
make restart         # Reinicia todos os containers
make ps              # Lista status dos containers
make logs            # Mostra logs de todos os containers
make logs-php        # Logs apenas do PHP
make logs-nginx      # Logs apenas do Nginx
make logs-mysql      # Logs apenas do MySQL
make logs-postgres   # Logs apenas do PostgreSQL
make logs-mongodb    # Logs apenas do MongoDB
make logs-redis      # Logs apenas do Redis
```

#### 💻 Acesso aos Containers

```bash
make bash            # Acessa bash do container PHP
make bash-nginx      # Acessa bash do Nginx
make bash-mysql      # Acessa bash do MySQL
make bash-postgres   # Acessa bash do PostgreSQL
make bash-redis      # Acessa bash do Redis
```

#### 🎬 Setup e Instalação

```bash
make init-project    # Setup completo automático (primeira vez)
make setup           # Configura Laravel (env, key, permissions)
make install         # Instala dependências do Composer
make rebuild         # Rebuild dos containers
make rebuild-all     # Rebuild completo (limpa tudo)
```

#### 📦 Laravel Artisan

```bash
make artisan         # Executa comando artisan customizado
make tinker          # Abre Laravel Tinker
make about           # Informações da aplicação
make route-list      # Lista todas as rotas
make schedule-list   # Lista tarefas agendadas
make docs            # Abre documentação do Laravel
make pail            # Tail logs usando Pail (Laravel 12+)
make channel-list    # Lista canais de broadcast
```

#### 🗄️ Migrations e Database

```bash
make migrate         # Executa migrations pendentes
make migrate-fresh   # Dropa e recria o banco
make migrate-rollback # Desfaz última migration
make migrate-status  # Status das migrations
make migrate-install  # Instala repositório de migrations
make schema-dump     # Dump do schema do banco
make seed            # Executa seeders
make fresh           # Fresh + seed
```

#### 🧹 Cache

```bash
make clear-all       # Limpa TODOS os caches
make cache-clear     # Limpa cache da aplicação
make cache-forget    # Remove item específico do cache
make cache-prune-tags # Remove tags stale (Redis)
make config-clear    # Limpa cache de configuração
make config-publish  # Publica arquivos de configuração
make route-clear     # Limpa cache de rotas
make view-clear      # Limpa cache de views
make event-clear     # Limpa cache de eventos
make event-list      # Lista eventos e listeners
make clear-compiled  # Remove classe compilada
make cache           # Gera cache (config, route, view)
```

#### 🔍 Debugging e Status

```bash
make status          # Status completo do ambiente
make health          # Health check dos serviços
make info            # Informações detalhadas
make debug           # Informações de debug
make debug-config    # Debug de configuração
make debug-routes    # Debug de rotas
make logs-laravel    # Tail logs do Laravel
```

#### 🧪 Testes

```bash
make test            # Executa todos os testes
make test-unit       # Apenas testes unitários
make test-feature    # Apenas testes de feature
make test-coverage   # Testes com cobertura
make test-filter     # Filtra testes específicos
```

#### 📝 Criação de Arquivos (Generators)

```bash
# Models e relacionados
make make-model              # Criar model
make make-model-full         # Model + Migration + Factory + Seeder + Controller

# Controllers
make make-controller         # Criar controller
make make-api-controller     # Controller para API

# Outros
make make-migration          # Criar migration
make make-seeder             # Criar seeder
make make-factory            # Criar factory
make make-middleware         # Criar middleware
make make-request            # Criar form request
make make-resource           # Criar API resource
make make-policy             # Criar policy
make make-job                # Criar job
make make-event              # Criar event
make make-listener           # Criar listener
make make-mail               # Criar mail
make make-notification       # Criar notification
make make-command            # Criar comando artisan
make make-class              # Criar classe genérica
make make-enum               # Criar enum
make make-interface          # Criar interface
make make-trait              # Criar trait
make make-scope              # Criar scope para model
make make-view               # Criar view Blade
make make-config             # Criar arquivo de configuração
make make-job-middleware      # Criar middleware para jobs
```

**Exemplo de uso:**
```bash
# Criar model Post com tudo
make make-model-full name=Post

# Cria automaticamente:
# - Model: app/Models/Post.php
# - Migration: database/migrations/xxx_create_posts_table.php
# - Factory: database/factories/PostFactory.php
# - Seeder: database/seeders/PostSeeder.php
# - Controller: app/Http/Controllers/PostController.php
```

#### 🔐 Laravel Packages

```bash
# Laravel Sanctum (Autenticação de API)
make sanctum-install         # Instala Sanctum
make sanctum-publish         # Publica assets do Sanctum

# Laravel Telescope (Debug)
make telescope-install       # Instala Telescope
make telescope-publish       # Publica assets do Telescope

# Laravel Horizon (Filas)
make horizon-install         # Instala Horizon
make horizon                 # Inicia Horizon
make horizon-publish         # Publica assets do Horizon
```

#### 🧹 Manutenção

```bash
make clean           # Limpa arquivos temporários
make permissions     # Corrige permissões de storage e cache
make storage-link    # Cria link simbólico de storage
make storage-unlink  # Remove link simbólico
make docker-clean    # Limpeza do Docker (volumes órfãos)
make docker-clean-all # Limpeza COMPLETA (CUIDADO!)
make clean-volumes   # Remove todos os volumes (CUIDADO!)
```

#### 🔐 Segurança

```bash
make env-encrypt     # Criptografa arquivo .env
make env-decrypt     # Descriptografa arquivo .env
make auth-clear-resets # Limpa tokens de reset expirados
```

#### 📊 Composer

```bash
make composer        # Executa comando composer customizado
make composer-update # Atualiza dependências
make composer-dump   # Regenera autoload
make composer-install # Instala dependências
```

#### 🔀 Git - Versionamento (70+ comandos)

O projeto inclui uma seção completa de comandos Git para facilitar o versionamento:

```bash
# Status e Informações
make git-status      # Status do repositório
make git-log         # Histórico de commits
make git-log-all     # Histórico de todas branches (oneline, graph, decorate, all)
make git-branch      # Lista branches
make git-diff        # Mostra diferenças

# Commit e Push
make git-add         # Adiciona todos arquivos
make git-commit      # Faz commit
make git-commit-amend # Corrige último commit (sem alterar mensagem)
make git-push        # Push para origin
make git-push-force-lease # Push forçado seguro (--force-with-lease)
make git-pull        # Pull do origin

# Branch
make git-branch-create # Cria nova branch
make git-branch-switch # Muda para branch
make git-branch-merge  # Faz merge

# Stash
make git-stash       # Salva mudanças temporariamente
make git-stash-pop   # Restaura e remove stash

# Workflow Rápido
make git-quick-push  # Add + commit + push de uma vez
make git-sync        # Sincroniza com remote
```

Ver todos os comandos Git: `make help | grep git`

#### 🐳 Docker - Containers e Imagens (25+ comandos)

```bash
# Containers
make container-list-stopped    # Lista containers parados
make container-remove-stopped  # Remove containers parados
make container-remove         # Remove container específico
make container-stop-all        # Para todos containers

# Imagens
make image-list                # Lista todas imagens
make image-remove              # Remove imagem específica
make image-remove-dangling     # Remove imagens órfãs
make image-prune               # Remove imagens não utilizadas

# Limpeza
make docker-clean-containers   # Limpa containers parados
make docker-clean-images       # Limpa imagens não usadas
make docker-clean-build-cache  # Limpa build cache
make docker-info               # Informações de uso do Docker
```

Ver todos os comandos Docker: `make help | grep docker` ou `make help | grep container` ou `make help | grep image`

#### 🔍 Qualidade de Código (44 comandos)

```bash
# PHP Insights
make phpinsights-install      # Instala PHP Insights
make phpinsights-analyze      # Análise completa com métricas
make phpinsights-fix          # Corrige problemas automaticamente

# PHPStan
make phpstan-install          # Instala PHPStan
make phpstan-analyze          # Análise estática (nível 0)
make phpstan-analyze-strict   # Análise rigorosa (nível 9)
make phpstan-baseline         # Gera baseline

# PHP CS Fixer
make phpcs-install            # Instala PHP CS Fixer
make phpcs-check              # Verifica estilo (sem alterar)
make phpcs-fix                # Corrige estilo automaticamente

# Laravel Pint
make pint-install             # Instala Laravel Pint
make pint-check               # Verifica formatação
make pint-fix                 # Corrige formatação

# PHPMD
make phpmd-install            # Instala PHPMD
make phpmd-analyze            # Analisa código

# Psalm
make psalm-install            # Instala Psalm
make psalm-analyze            # Analisa código

# Workflows completos
make quality-check            # Executa todas as verificações
make quality-fix              # Corrige automaticamente
make quality-install-all      # Instala todas as ferramentas
```

Ver todos os comandos de qualidade: `make help | grep -E "quality|phpinsights|phpstan|phpcs|pint|phpmd|psalm"`

#### 📚 Documentação API

```bash
# Scramble (OpenAPI)
make scramble-install         # Instala Scramble
make scramble-generate        # Gera documentação OpenAPI
make scramble-generate-json   # Gera arquivo JSON
make scramble-generate-yaml   # Gera arquivo YAML

# Swagger (L5-Swagger)
make swagger-install          # Instala L5-Swagger
make swagger-publish          # Publica configuração
make swagger-generate         # Gera documentação Swagger
make swagger-ui               # Abre Swagger UI no navegador

# Scribe
make scribe-install           # Instala Scribe
make scribe-generate          # Gera documentação

# phpDocumentor
make phpdoc-install           # Instala phpDocumentor
make phpdoc-generate          # Gera documentação PHPDoc
```

Ver todos os comandos de documentação: `make help | grep -E "scramble|swagger|scribe|phpdoc"`

---

## 👨‍💻 Desenvolvimento

### Workflow Típico

```bash
# 1. Criar novo recurso
make make-model-full name=Product

# 2. Editar migration
# Edite: laravel/database/migrations/xxx_create_products_table.php

# 3. Executar migration
make migrate

# 4. Testar no Tinker
make tinker
>>> App\Models\Product::factory()->create()

# 5. Criar seeder
make make-seeder name=ProductSeeder

# 6. Executar seeder
make seed class=ProductSeeder

# 7. Listar rotas
make route-list

# 8. Ver logs
make logs-laravel
```

### Hot Reload

O código é montado como volume, então **alterações são instantâneas**:

1. Edite qualquer arquivo em `backend/laravel/`
2. Salve o arquivo
3. A alteração já está ativa no container
4. Recarregue a página/requisição

**Não precisa:**
- ❌ Reiniciar containers
- ❌ Rebuild das imagens
- ❌ Fazer deploy

**Exceções (precisa reiniciar):**
- Alterações no `docker-compose.yml`
- Alterações em Dockerfiles
- Mudanças em configurações do Nginx/PHP

### Acesso aos Logs

```bash
# Logs em tempo real
make logs             # Todos os containers
make logs-php         # Só PHP-FPM
make logs-nginx       # Só Nginx
make logs-mysql       # Só MySQL
make logs-postgres    # Só PostgreSQL
make logs-mongodb     # Só MongoDB
make logs-redis       # Só Redis

# Logs do Laravel
make logs-laravel     # Tail do storage/logs/laravel.log
```

### Debugging com Tinker

```bash
make tinker

# No Tinker:
>>> App\Models\User::all()
>>> App\Models\User::factory()->create()
>>> DB::connection()->getPdo()  # Testa conexão
>>> Cache::put('key', 'value', 60)
>>> Cache::get('key')
```

### Variáveis de Ambiente

O arquivo `laravel/.env` contém todas as configurações:

```env
# Application
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost:8080

# Database (MySQL)
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_laravel
DB_USERNAME=developer
DB_PASSWORD=123456

# Redis
REDIS_HOST=redis
REDIS_PASSWORD=null
REDIS_PORT=6379

# Mail (Mailpit)
MAIL_MAILER=smtp
MAIL_HOST=mailer
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=hello@example.com
MAIL_FROM_NAME="${APP_NAME}"

# Laravel Sanctum
SANCTUM_STATEFUL_DOMAINS=localhost,localhost:3000,127.0.0.1
SESSION_DRIVER=cookie
```

### Criar um Endpoint de API

**1. Criar Model e Migration:**
```bash
make make-model-full name=Post
```

**2. Editar Migration (`database/migrations/xxx_create_posts_table.php`):**
```php
public function up()
{
    Schema::create('posts', function (Blueprint $table) {
        $table->id();
        $table->string('title');
        $table->text('content');
        $table->timestamps();
    });
}
```

**3. Executar Migration:**
```bash
make migrate
```

**4. Editar Controller (`app/Http/Controllers/PostController.php`):**
```php
public function index()
{
    return Post::all();
}

public function store(Request $request)
{
    $validated = $request->validate([
        'title' => 'required|max:255',
        'content' => 'required'
    ]);
    
    return Post::create($validated);
}
```

**5. Adicionar Rotas (`routes/api.php`):**
```php
Route::apiResource('posts', PostController::class);
```

**6. Testar:**
```bash
# Listar rotas
make route-list

# Criar post via Tinker
make tinker
>>> App\Models\Post::create(['title' => 'Test', 'content' => 'Hello'])
```

---

## 🧪 Testes

### Estrutura de Testes

```
laravel/tests/
├── Feature/          # Testes de integração/feature
│   └── ExampleTest.php
└── Unit/             # Testes unitários
    └── ExampleTest.php
```

### Executando Testes

```bash
# Todos os testes
make test

# Apenas unitários
make test-unit

# Apenas feature
make test-feature

# Com cobertura
make test-coverage

# Filtrar testes específicos
make test-filter filter=ExampleTest

# Modo watch (reexecuta quando arquivos mudam)
make test-watch
```

### Criar Teste

```bash
# Teste unitário
make test-create name=UserTest

# Teste feature
make test-create-feature name=PostApiTest
```

### Exemplo de Teste de API

```php
// tests/Feature/PostApiTest.php
public function test_can_create_post()
{
    $response = $this->postJson('/api/posts', [
        'title' => 'Test Post',
        'content' => 'Test content'
    ]);

    $response->assertStatus(201)
             ->assertJson([
                 'title' => 'Test Post'
             ]);

    $this->assertDatabaseHas('posts', [
        'title' => 'Test Post'
    ]);
}
```

---

## 🚀 Deploy

### Preparação para Produção

```bash
# 1. Otimizações
make cache              # Gera caches
make composer-dump      # Otimiza autoload

# 2. Verificar ambiente
make about
make status

# 3. Testes
make test

# 4. Backup do banco
make backup-db
```

### Variáveis .env para Produção

```env
APP_ENV=production
APP_DEBUG=false
APP_URL=https://seu-dominio.com

# Use bancos dedicados
DB_HOST=seu-db-host
DB_DATABASE=seu_db

# Configure email real
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
# ...
```

### Segurança

O PHP já vem configurado com segurança:

```ini
expose_php = Off
display_errors = Off
log_errors = On
allow_url_fopen = Off
allow_url_include = Off
session.cookie_httponly = On
session.cookie_secure = On
session.use_strict_mode = On
```

---

## 🆘 Troubleshooting

### Containers não iniciam

```bash
# Ver logs
make logs

# Reconstruir
make down
make rebuild
make up
```

### Erro de permissão

```bash
make permissions
```

### Banco não conecta

```bash
# Health check
make health

# Ver logs do banco
make logs-mysql      # ou logs-postgres

# Verificar se banco está rodando
make ps
```

### Erro "could not find driver"

Significa que a extensão PHP do banco não está instalada:

```bash
# Rebuild do container PHP
make rebuild

# Verificar extensões PHP instaladas
make bash
php -m | grep pdo
```

### Cache travando

```bash
# Limpa todos os caches
make clear-all

# Ou individual
make cache-clear
make config-clear
make route-clear
make view-clear
```

### Composer lento

```bash
# Dentro do container
make bash
composer config --global repo.packagist composer https://packagist.org
composer install --optimize-autoloader
```

### Mailpit não funciona

```bash
# Ver logs
make logs-mailer

# Reiniciar
docker compose restart mailer

# Verificar portas
make info
```

### Ver informações de debug

```bash
make debug           # Info geral
make debug-config    # Config do Laravel
make debug-routes    # Rotas registradas
make about           # About do Laravel
```

### Redis não conecta

```bash
# Testar conexão
make redis-cli
> ping
# Deve retornar PONG

# Ver logs
make logs-redis

# Reiniciar
make restart-redis
```

### Verificar saúde do ambiente

```bash
make health

# Saída esperada:
# ✓ MySQL OK (ou PostgreSQL OK)
# ✓ Redis OK
# ✓ PHP-FPM OK
```

---

## 📊 Estatísticas do Projeto

```bash
# Linhas de código
make project-stats

# Estrutura de pastas
make tree

# Modelos e controllers
make list-models
make list-controllers
```

---

## 🔗 Links Úteis

- **Laravel 12 Docs**: https://laravel.com/docs/12.x
- **Docker Docs**: https://docs.docker.com/
- **PostgreSQL 18 Docs**: https://www.postgresql.org/docs/18/
- **MySQL 8.0 Docs**: https://dev.mysql.com/doc/refman/8.0/en/
- **Laravel Sanctum**: https://laravel.com/docs/12.x/sanctum
- **Redis**: https://redis.io/documentation

---

## ✅ Checklist de Desenvolvimento

Antes de começar a desenvolver:

- [ ] Containers rodando (`make ps`)
- [ ] Banco de dados configurado (`make health`)
- [ ] Migrations executadas (`make migrate-status`)
- [ ] Testes passando (`make test`)
- [ ] Variáveis `.env` configuradas
- [ ] Consegue acessar http://localhost:8080

---

## 🎯 Próximos Passos

1. **Configure autenticação**: [Laravel Sanctum](https://laravel.com/docs/12.x/sanctum)
2. **Crie seus models**: `make make-model-full name=SeuModel`
3. **Implemente sua lógica**: Controllers, Services, etc.
4. **Escreva testes**: `make test-create-feature`
5. **Deploy**: Prepare para produção

---

## 📞 Suporte

- 📖 **Documentação Principal**: `../README.md`
- 🐛 **Reportar Bug**: Abra uma issue
- 💬 **Dúvidas**: Use as discussions

---

**Bom desenvolvimento! 🚀**
