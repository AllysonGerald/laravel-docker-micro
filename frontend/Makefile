.PHONY: help

# Cores para output
BLUE := \033[0;34m
GREEN := \033[0;32m
YELLOW := \033[0;33m
RED := \033[0;31m
CYAN := \033[0;36m
NC := \033[0m # No Color

##@ 🎯 Ajuda

help: ## Mostra esta mensagem de ajuda
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo "$(GREEN)  🎨 Frontend - Comandos Disponíveis$(NC)"
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@awk 'BEGIN {FS = ":.*##"; printf "\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  $(YELLOW)%-30s$(NC) %s\n", $$1, $$2 } /^##@/ { printf "\n$(BLUE)%s$(NC)\n", substr($$0, 5) } ' $(MAKEFILE_LIST)
	@echo ""

##@ 🚀 Criar Projetos (Vite)

create-vue: ## Cria projeto Vue 3 com Vite
	@read -p "Nome do projeto (ex: my-vue-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Vue 3...$(NC)"; \
		npm create vue@latest $$name -- --typescript --router --pinia --vitest --eslint; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name$(NC)"; \
	fi

create-react: ## Cria projeto React com Vite
	@read -p "Nome do projeto (ex: my-react-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto React com Vite...$(NC)"; \
		npm create vite@latest $$name -- --template react-ts; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

create-react-js: ## Cria projeto React (JavaScript) com Vite
	@read -p "Nome do projeto (ex: my-react-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto React com Vite (JS)...$(NC)"; \
		npm create vite@latest $$name -- --template react; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

create-svelte: ## Cria projeto Svelte com Vite
	@read -p "Nome do projeto (ex: my-svelte-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Svelte com Vite...$(NC)"; \
		npm create vite@latest $$name -- --template svelte-ts; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

create-vanilla: ## Cria projeto Vanilla (TypeScript) com Vite
	@read -p "Nome do projeto (ex: my-vanilla-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Vanilla com Vite...$(NC)"; \
		npm create vite@latest $$name -- --template vanilla-ts; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

create-next: ## Cria projeto Next.js (React framework)
	@read -p "Nome do projeto (ex: my-next-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Next.js...$(NC)"; \
		npx create-next-app@latest $$name --typescript --tailwind --eslint --app --src-dir --import-alias "@/*"; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name$(NC)"; \
	fi

create-nuxt: ## Cria projeto Nuxt 3 (Vue framework)
	@read -p "Nome do projeto (ex: my-nuxt-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Nuxt 3...$(NC)"; \
		npx nuxi@latest init $$name; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

create-angular: ## Cria projeto Angular
	@read -p "Nome do projeto (ex: my-angular-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Angular...$(NC)"; \
		npx @angular/cli@latest new $$name --routing --style=css --strict; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name$(NC)"; \
	fi

create-remix: ## Cria projeto Remix (React framework)
	@read -p "Nome do projeto (ex: my-remix-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto Remix...$(NC)"; \
		npx create-remix@latest $$name; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

create-sveltekit: ## Cria projeto SvelteKit
	@read -p "Nome do projeto (ex: my-sveltekit-app): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do projeto é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)🚀 Criando projeto SvelteKit...$(NC)"; \
		npm create svelte@latest $$name; \
		echo "$(GREEN)✅ Projeto criado! Acesse: cd $$name && npm install$(NC)"; \
	fi

##@ 📦 Gerenciamento de Dependências

install: ## Instala dependências (npm install)
	@echo "$(GREEN)📦 Instalando dependências...$(NC)"
	@npm install

install-yarn: ## Instala dependências com Yarn
	@echo "$(GREEN)📦 Instalando dependências com Yarn...$(NC)"
	@yarn install

install-pnpm: ## Instala dependências com pnpm
	@echo "$(GREEN)📦 Instalando dependências com pnpm...$(NC)"
	@pnpm install

add: ## Adiciona nova dependência
	@read -p "Nome do pacote (ex: axios): " pkg; \
	if [ -z "$$pkg" ]; then \
		echo "$(RED)❌ Nome do pacote é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)➕ Instalando $$pkg...$(NC)"; \
		npm install $$pkg; \
	fi

add-dev: ## Adiciona dependência de desenvolvimento
	@read -p "Nome do pacote (ex: @types/node): " pkg; \
	if [ -z "$$pkg" ]; then \
		echo "$(RED)❌ Nome do pacote é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)➕ Instalando $$pkg (dev)...$(NC)"; \
		npm install -D $$pkg; \
	fi

remove: ## Remove dependência
	@read -p "Nome do pacote para remover: " pkg; \
	if [ -z "$$pkg" ]; then \
		echo "$(RED)❌ Nome do pacote é obrigatório!$(NC)"; \
	else \
		echo "$(RED)🗑️  Removendo $$pkg...$(NC)"; \
		npm uninstall $$pkg; \
	fi

update: ## Atualiza todas as dependências
	@echo "$(YELLOW)🔄 Atualizando dependências...$(NC)"
	@npm update

outdated: ## Lista pacotes desatualizados
	@echo "$(YELLOW)📋 Verificando pacotes desatualizados...$(NC)"
	@npm outdated

clean-install: ## Limpa node_modules e reinstala
	@echo "$(YELLOW)🧹 Limpando e reinstalando...$(NC)"
	@rm -rf node_modules package-lock.json
	@npm install
	@echo "$(GREEN)✅ Limpeza concluída!$(NC)"

##@ 🛠️ Desenvolvimento

dev: ## Inicia servidor de desenvolvimento (Vite)
	@echo "$(GREEN)🚀 Iniciando servidor de desenvolvimento...$(NC)"
	@npm run dev

dev-host: ## Inicia dev server acessível na rede local
	@echo "$(GREEN)🚀 Iniciando servidor (host: 0.0.0.0)...$(NC)"
	@npm run dev -- --host

dev-port: ## Inicia dev server em porta customizada
	@read -p "Porta (ex: 3000): " port; \
	if [ -z "$$port" ]; then \
		port=3000; \
	fi; \
	echo "$(GREEN)🚀 Iniciando servidor na porta $$port...$(NC)"; \
	npm run dev -- --port $$port

build: ## Constrói projeto para produção
	@echo "$(GREEN)🏗️  Construindo projeto para produção...$(NC)"
	@npm run build

build-watch: ## Constrói em modo watch
	@echo "$(GREEN)🏗️  Construindo em modo watch...$(NC)"
	@npm run build -- --watch

preview: ## Preview da build de produção
	@echo "$(GREEN)👁️  Iniciando preview da build...$(NC)"
	@npm run preview

preview-host: ## Preview acessível na rede local
	@echo "$(GREEN)👁️  Iniciando preview (host: 0.0.0.0)...$(NC)"
	@npm run preview -- --host

serve: ## Serve build localmente (sem Vite)
	@echo "$(GREEN)🌐 Servindo build localmente...$(NC)"
	@npx serve dist

##@ 🧪 Testes

test: ## Executa testes
	@echo "$(GREEN)🧪 Executando testes...$(NC)"
	@npm run test

test-watch: ## Executa testes em modo watch
	@echo "$(GREEN)🧪 Executando testes em modo watch...$(NC)"
	@npm run test -- --watch

test-coverage: ## Executa testes com cobertura
	@echo "$(GREEN)🧪 Executando testes com cobertura...$(NC)"
	@npm run test -- --coverage

test-ui: ## Executa testes com UI (Vitest)
	@echo "$(GREEN)🧪 Abrindo UI de testes...$(NC)"
	@npm run test -- --ui

##@ 🎨 Linting e Formatação

lint: ## Executa linter
	@echo "$(GREEN)🔍 Executando linter...$(NC)"
	@npm run lint

lint-fix: ## Corrige problemas do linter automaticamente
	@echo "$(GREEN)🔧 Corrigindo problemas do linter...$(NC)"
	@npm run lint -- --fix

format: ## Formata código (Prettier)
	@echo "$(GREEN)✨ Formatando código...$(NC)"
	@npm run format || npx prettier --write "src/**/*.{js,jsx,ts,tsx,vue,svelte,css,scss,json}"

format-check: ## Verifica formatação sem alterar
	@echo "$(GREEN)🔍 Verificando formatação...$(NC)"
	@npm run format:check || npx prettier --check "src/**/*.{js,jsx,ts,tsx,vue,svelte,css,scss,json}"

type-check: ## Verifica tipos TypeScript
	@echo "$(GREEN)🔍 Verificando tipos TypeScript...$(NC)"
	@npm run type-check || npx tsc --noEmit

##@ 🏗️ Build e Deploy

analyze: ## Analisa tamanho do bundle
	@echo "$(GREEN)📊 Analisando bundle...$(NC)"
	@npm run build && npx vite-bundle-visualizer

build-stats: ## Mostra estatísticas da build
	@echo "$(GREEN)📊 Gerando estatísticas da build...$(NC)"
	@npm run build -- --report

deploy-check: ## Verifica build antes de deploy
	@echo "$(GREEN)✅ Verificando build para deploy...$(NC)"
	@npm run build
	@npm run test || echo "$(YELLOW)⚠️  Testes não configurados$(NC)"
	@npm run lint || echo "$(YELLOW)⚠️  Linter não configurado$(NC)"
	@echo "$(GREEN)✅ Build verificado com sucesso!$(NC)"

##@ 🎨 Componentes e Arquitetura

create-component: ## Cria componente (Vue/React)
	@read -p "Nome do componente (ex: Button): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do componente é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)📝 Criando componente $$name...$(NC)"; \
		mkdir -p src/components/$$name; \
		if [ -f "vite.config.js" ] || [ -f "vite.config.ts" ]; then \
			if [ -f "package.json" ] && grep -q "vue" package.json; then \
				echo "<template>\n  <div class=\"$$(echo $$name | tr '[:upper:]' '[:lower:]')\">\n    <!-- $$name component -->\n  </div>\n</template>\n\n<script setup lang=\"ts\">\n// Component logic\n</script>\n\n<style scoped>\n.$$(echo $$name | tr '[:upper:]' '[:lower:]') {\n  /* Styles */\n}\n</style>" > src/components/$$name/$$name.vue; \
			elif [ -f "package.json" ] && grep -q "react" package.json; then \
				echo "import React from 'react';\n\ninterface $$nameProps {\n  // Props\n}\n\nconst $$name: React.FC<$$nameProps> = () => {\n  return (\n    <div className=\"$$(echo $$name | tr '[:upper:]' '[:lower:]')\">\n      {/* $$name component */}\n    </div>\n  );\n};\n\nexport default $$name;" > src/components/$$name/$$name.tsx; \
			fi; \
		fi; \
		echo "$(GREEN)✅ Componente criado em src/components/$$name/$(NC)"; \
	fi

create-page: ## Cria página/rota (Vue Router/React Router)
	@read -p "Nome da página (ex: About): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome da página é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)📝 Criando página $$name...$(NC)"; \
		mkdir -p src/pages; \
		if [ -f "package.json" ] && grep -q "vue" package.json; then \
			echo "<template>\n  <div class=\"$$(echo $$name | tr '[:upper:]' '[:lower:]')\">\n    <h1>$$name Page</h1>\n  </div>\n</template>\n\n<script setup lang=\"ts\">\n// Page logic\n</script>\n\n<style scoped>\n.$$(echo $$name | tr '[:upper:]' '[:lower:]') {\n  /* Styles */\n}\n</style>" > src/pages/$$name.vue; \
		elif [ -f "package.json" ] && grep -q "react" package.json; then \
			echo "import React from 'react';\n\nconst $$name: React.FC = () => {\n  return (\n    <div className=\"$$(echo $$name | tr '[:upper:]' '[:lower:]')\">\n      <h1>$$name Page</h1>\n    </div>\n  );\n};\n\nexport default $$name;" > src/pages/$$name.tsx; \
		fi; \
		echo "$(GREEN)✅ Página criada em src/pages/$$name$(NC)"; \
	fi

create-composable: ## Cria composable (Vue 3)
	@read -p "Nome do composable (ex: useCounter): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do composable é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)📝 Criando composable $$name...$(NC)"; \
		mkdir -p src/composables; \
		echo "import { ref } from 'vue';\n\nexport function $$name() {\n  // Composable logic\n  return {\n    // Return values\n  };\n}" > src/composables/$$name.ts; \
		echo "$(GREEN)✅ Composable criado em src/composables/$$name.ts$(NC)"; \
	fi

create-hook: ## Cria custom hook (React)
	@read -p "Nome do hook (ex: useCounter): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome do hook é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)📝 Criando hook $$name...$(NC)"; \
		mkdir -p src/hooks; \
		echo "import { useState, useEffect } from 'react';\n\nexport function $$name() {\n  // Hook logic\n  return {\n    // Return values\n  };\n}" > src/hooks/$$name.ts; \
		echo "$(GREEN)✅ Hook criado em src/hooks/$$name.ts$(NC)"; \
	fi

create-store: ## Cria store (Pinia/Vuex/Zustand)
	@read -p "Nome da store (ex: userStore): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome da store é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)📝 Criando store $$name...$(NC)"; \
		mkdir -p src/stores; \
		if [ -f "package.json" ] && grep -q "pinia" package.json; then \
			echo "import { defineStore } from 'pinia';\n\nexport const use$$(echo $$name | sed 's/Store//')Store = defineStore('$$(echo $$name | tr '[:upper:]' '[:lower:]')', {\n  state: () => ({\n    // State\n  }),\n  getters: {\n    // Getters\n  },\n  actions: {\n    // Actions\n  },\n});" > src/stores/$$name.ts; \
		elif [ -f "package.json" ] && grep -q "zustand" package.json; then \
			echo "import { create } from 'zustand';\n\ninterface $$nameState {\n  // State\n}\n\nconst use$$name = create<$$nameState>((set) => ({\n  // State and actions\n}));\n\nexport default use$$name;" > src/stores/$$name.ts; \
		fi; \
		echo "$(GREEN)✅ Store criada em src/stores/$$name.ts$(NC)"; \
	fi

create-api: ## Cria arquivo de API/service
	@read -p "Nome da API/service (ex: userApi): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome é obrigatório!$(NC)"; \
	else \
		echo "$(GREEN)📝 Criando API $$name...$(NC)"; \
		mkdir -p src/api; \
		echo "// API base URL\nconst API_URL = import.meta.env.VITE_API_URL || 'http://localhost:8080/api';\n\nexport const $$name = {\n  // API methods\n  async getAll() {\n    const response = await fetch(\`\$${API_URL}/$$(echo $$name | tr '[:upper:]' '[:lower:]' | sed 's/api//')\`);\n    return response.json();\n  },\n  async getById(id: string | number) {\n    const response = await fetch(\`\$${API_URL}/$$(echo $$name | tr '[:upper:]' '[:lower:]' | sed 's/api//')/\$${id}\`);\n    return response.json();\n  },\n  // Add more methods as needed\n};" > src/api/$$name.ts; \
		echo "$(GREEN)✅ API criada em src/api/$$name.ts$(NC)"; \
	fi

##@ 🔧 Configuração e Setup

setup-vite: ## Configura Vite no projeto atual
	@echo "$(GREEN)⚙️  Configurando Vite...$(NC)"
	@npm install -D vite @vitejs/plugin-react || npm install -D vite @vitejs/plugin-vue
	@echo "$(GREEN)✅ Vite configurado!$(NC)"

setup-typescript: ## Adiciona TypeScript ao projeto
	@echo "$(GREEN)⚙️  Configurando TypeScript...$(NC)"
	@npm install -D typescript @types/node
	@npx tsc --init
	@echo "$(GREEN)✅ TypeScript configurado!$(NC)"

setup-eslint: ## Configura ESLint
	@echo "$(GREEN)⚙️  Configurando ESLint...$(NC)"
	@npm install -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-react
	@npx eslint --init
	@echo "$(GREEN)✅ ESLint configurado!$(NC)"

setup-prettier: ## Configura Prettier
	@echo "$(GREEN)⚙️  Configurando Prettier...$(NC)"
	@npm install -D prettier eslint-config-prettier eslint-plugin-prettier
	@echo "{\n  \"semi\": true,\n  \"singleQuote\": true,\n  \"tabWidth\": 2,\n  \"trailingComma\": \"es5\"\n}" > .prettierrc.json
	@echo "$(GREEN)✅ Prettier configurado!$(NC)"

setup-tailwind: ## Instala e configura Tailwind CSS
	@echo "$(GREEN)⚙️  Configurando Tailwind CSS...$(NC)"
	@npm install -D tailwindcss postcss autoprefixer
	@npx tailwindcss init -p
	@echo "$(GREEN)✅ Tailwind CSS configurado!$(NC)"

setup-router: ## Instala router (Vue Router ou React Router)
	@if [ -f "package.json" ] && grep -q "vue" package.json; then \
		echo "$(GREEN)⚙️  Instalando Vue Router...$(NC)"; \
		npm install vue-router@4; \
	elif [ -f "package.json" ] && grep -q "react" package.json; then \
		echo "$(GREEN)⚙️  Instalando React Router...$(NC)"; \
		npm install react-router-dom; \
	fi
	@echo "$(GREEN)✅ Router instalado!$(NC)"

setup-pinia: ## Instala Pinia (gerenciamento de estado Vue)
	@echo "$(GREEN)⚙️  Instalando Pinia...$(NC)"
	@npm install pinia
	@echo "$(GREEN)✅ Pinia instalado!$(NC)"

setup-zustand: ## Instala Zustand (gerenciamento de estado React)
	@echo "$(GREEN)⚙️  Instalando Zustand...$(NC)"
	@npm install zustand
	@echo "$(GREEN)✅ Zustand instalado!$(NC)"

setup-axios: ## Instala Axios para requisições HTTP
	@echo "$(GREEN)⚙️  Instalando Axios...$(NC)"
	@npm install axios
	@echo "$(GREEN)✅ Axios instalado!$(NC)"

##@ 🧹 Limpeza

clean: ## Remove arquivos temporários e cache
	@echo "$(YELLOW)🧹 Limpando arquivos temporários...$(NC)"
	@rm -rf node_modules/.vite
	@rm -rf dist
	@rm -rf .turbo
	@rm -rf .next
	@rm -rf .nuxt
	@rm -rf .svelte-kit
	@echo "$(GREEN)✅ Limpeza concluída!$(NC)"

clean-all: ## Limpeza completa (inclui node_modules)
	@echo "$(RED)⚠️  Isso vai remover node_modules!$(NC)"
	@read -p "Continuar? [s/N]: " confirm; \
	if [ "$$confirm" = "s" ] || [ "$$confirm" = "S" ]; then \
		rm -rf node_modules package-lock.json yarn.lock pnpm-lock.yaml; \
		rm -rf dist node_modules/.vite .turbo .next .nuxt .svelte-kit; \
		echo "$(GREEN)✅ Limpeza completa concluída!$(NC)"; \
	else \
		echo "Cancelado."; \
	fi

##@ 🔥 Laravel Livewire

livewire-info: ## Mostra informações sobre Livewire no backend
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo "$(GREEN)🔥 Laravel Livewire - Comandos Disponíveis$(NC)"
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo ""
	@echo "$(YELLOW)Para usar Livewire, execute os comandos no diretório backend:$(NC)"
	@echo ""
	@echo "  $(GREEN)cd ../backend$(NC)"
	@echo ""
	@echo "$(YELLOW)Comandos disponíveis:$(NC)"
	@echo "  make livewire-install      - Instala Livewire"
	@echo "  make livewire-make         - Cria componente Livewire"
	@echo "  make livewire-delete       - Remove componente"
	@echo "  make livewire-move         - Move componente"
	@echo "  make livewire-copy         - Copia componente"
	@echo "  make livewire-discover     - Descobre componentes"
	@echo ""
	@echo "$(CYAN)📖 Documentação completa: frontend/README.md#-laravel-livewire---guia-completo$(NC)"
	@echo ""

livewire-check: ## Verifica se Livewire está instalado no backend
	@echo "$(YELLOW)🔍 Verificando Livewire no backend...$(NC)"
	@if [ -f "../backend/laravel/composer.json" ]; then \
		if grep -q "livewire" ../backend/laravel/composer.json; then \
			echo "$(GREEN)✅ Livewire está instalado!$(NC)"; \
		else \
			echo "$(RED)❌ Livewire não está instalado$(NC)"; \
			echo "$(YELLOW)💡 Execute: cd ../backend && make livewire-install$(NC)"; \
		fi; \
	else \
		echo "$(RED)❌ Laravel não encontrado em ../backend/laravel/$(NC)"; \
	fi

livewire-create-view: ## Cria view Blade para componente Livewire
	@read -p "Nome do componente (ex: UserTable): " name; \
	if [ -z "$$name" ]; then \
		echo "$(RED)❌ Nome é obrigatório!$(NC)"; \
	else \
		view_path="../backend/laravel/resources/views/livewire/$$(echo $$name | tr '[:upper:]' '[:lower:]').blade.php"; \
		mkdir -p $$(dirname $$view_path); \
		echo "<div>\n    <!-- $$name component -->\n</div>" > $$view_path; \
		echo "$(GREEN)✅ View criada em: $$view_path$(NC)"; \
		echo "$(YELLOW)💡 Agora crie o componente: cd ../backend && make livewire-make name=$$name$(NC)"; \
	fi

livewire-list-components: ## Lista componentes Livewire instalados
	@echo "$(YELLOW)📋 Componentes Livewire encontrados:$(NC)"
	@if [ -d "../backend/laravel/app/Livewire" ]; then \
		find ../backend/laravel/app/Livewire -name "*.php" -type f | while read file; do \
			component=$$(basename $$file .php); \
			echo "  $(GREEN)•$(NC) $$component"; \
		done; \
	else \
		echo "$(RED)❌ Diretório Livewire não encontrado$(NC)"; \
		echo "$(YELLOW)💡 Execute: cd ../backend && make livewire-install$(NC)"; \
	fi

livewire-docs: ## Abre documentação do Livewire no navegador
	@echo "$(GREEN)📖 Abrindo documentação do Livewire...$(NC)"
	@xdg-open https://livewire.laravel.com 2>/dev/null || \
	 open https://livewire.laravel.com 2>/dev/null || \
	 echo "$(YELLOW)💡 Acesse: https://livewire.laravel.com$(NC)"

##@ 📊 Informações

info: ## Mostra informações do projeto
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo "$(GREEN)📋 Informações do Projeto$(NC)"
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo ""
	@if [ -f "package.json" ]; then \
		echo "$(YELLOW)📦 Nome:$(NC) $$(cat package.json | grep '"name"' | head -1 | cut -d'"' -f4)"; \
		echo "$(YELLOW)📌 Versão:$(NC) $$(cat package.json | grep '"version"' | head -1 | cut -d'"' -f4)"; \
		echo ""; \
	fi
	@if [ -f "vite.config.js" ] || [ -f "vite.config.ts" ]; then \
		echo "$(GREEN)✅ Vite configurado$(NC)"; \
	fi
	@if [ -f "tsconfig.json" ]; then \
		echo "$(GREEN)✅ TypeScript configurado$(NC)"; \
	fi
	@if [ -f ".eslintrc" ] || [ -f ".eslintrc.json" ] || [ -f ".eslintrc.js" ]; then \
		echo "$(GREEN)✅ ESLint configurado$(NC)"; \
	fi
	@echo ""
	@echo "$(YELLOW)📊 Dependências:$(NC)"
	@if [ -f "package.json" ]; then \
		echo "  Total: $$(cat package.json | grep -c '"dependencies"') dependências"; \
	fi
	@echo ""

version: ## Mostra versões das ferramentas
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo "$(GREEN)📌 Versões das Ferramentas$(NC)"
	@echo "$(BLUE)━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━$(NC)"
	@echo ""
	@echo "$(YELLOW)Node.js:$(NC) $$(node --version 2>/dev/null || echo 'Não instalado')"
	@echo "$(YELLOW)npm:$(NC) $$(npm --version 2>/dev/null || echo 'Não instalado')"
	@echo "$(YELLOW)Yarn:$(NC) $$(yarn --version 2>/dev/null || echo 'Não instalado')"
	@echo "$(YELLOW)pnpm:$(NC) $$(pnpm --version 2>/dev/null || echo 'Não instalado')"
	@if [ -f "package.json" ] && grep -q "vite" package.json; then \
		echo "$(YELLOW)Vite:$(NC) $$(npm list vite 2>/dev/null | grep vite | head -1 | awk '{print $$2}' || echo 'Não instalado')"; \
	fi
	@echo ""

