# Documentação Técnica — frete-frontend-challenge

## Visão Geral

- **Nome do projeto:** frete-frontend-challenge  
- **Propósito:** disponibilizar uma interface web administrativa para gestão de operações de frete.  
- **Função principal:** permitir o cadastro, consulta, edição e remoção de fretes, transportadoras, motoristas e veículos, consumindo uma API HTTP backend.

## Stack Tecnológica

### Linguagens de programação
- TypeScript
- JavaScript (ecossistema de build e dependências)
- CSS

### Frameworks e bibliotecas principais
- **Front-end:** React 18
- **Roteamento:** React Router DOM
- **Gerenciamento de estado assíncrono/cache:** TanStack React Query
- **HTTP client:** Axios
- **Formulários e validação:** React Hook Form + Zod + @hookform/resolvers
- **UI e componentes:** Tailwind CSS, Radix UI, shadcn/ui, Lucide React, Phosphor Icons, Sonner
- **Utilitários:** date-fns, clsx, class-variance-authority, tailwind-merge

### Banco(s) de dados utilizados
- Este repositório representa apenas a camada de front-end e **não implementa acesso direto a banco de dados**.
- A persistência de dados é delegada ao serviço backend acessado via API REST.

### Build, versionamento e infraestrutura
- **Build tooling:** Vite + TypeScript Compiler (tsc)
- **Qualidade de código:** ESLint
- **Estilização/pipeline CSS:** PostCSS + Autoprefixer + Tailwind CSS
- **Gerenciador de pacotes:** npm
- **Versionamento:** Git (repositório GitHub)
- **CI/CD:** não há pipelines de CI/CD versionadas neste repositório.

## Integrações Externas

### API backend (REST)
- **Base URL configurada:** `http://localhost:8080` (arquivo `src/services/api.ts`)
- **Propósito:** fornecer operações CRUD e consultas para os domínios da aplicação.

#### Recursos consumidos
- `/freight` e `/freight/{id}`: gestão de fretes.
- `/transporter` e `/transporter/{id}`: gestão de transportadoras.
- `/driver` e `/driver/{id}`: gestão de motoristas.
- `/vehicle` e `/vehicle/{id}`: gestão de veículos.

> Não foram identificadas integrações com gateways de pagamento, provedores de e-mail/SMS ou serviços externos de autenticação neste código-fonte.

## Arquitetura do Sistema

### Padrão arquitetural adotado
- Aplicação **SPA (Single Page Application)** em React.
- Arquitetura de front-end orientada a componentes, com separação por páginas de domínio (`freights`, `transporters`, `drivers`, `vehicles`).
- Comunicação com backend por camada de serviço HTTP centralizada (`api` via Axios).
- Gerenciamento de estado remoto e sincronização de cache com React Query.

### Fluxo de dados (descrição textual)
1. O usuário navega pelas rotas definidas em `src/routes/index.tsx`.
2. Cada página executa consultas (`useQuery`) para buscar dados no backend.
3. A camada `api` (Axios) envia requisições HTTP para os endpoints REST.
4. As respostas alimentam os componentes de tabela e formulários.
5. Ações de criação/edição/remoção usam mutações (`useMutation`).
6. Após mutações, o cache é invalidado para recarregar os dados atualizados.
7. Feedback de sucesso/erro é exibido via notificações toast (Sonner).

### Justificativa arquitetural
- A combinação **React + React Query + Axios** reduz complexidade no gerenciamento de estado assíncrono e padroniza chamadas HTTP.
- O uso de **React Hook Form + Zod** centraliza validação e consistência dos dados de entrada.
- A divisão por domínios e componentes reutilizáveis melhora manutenção e evolução da interface.

## Contato do Desenvolvedor

- **Responsável técnico (repositório):** Damaso Magno  
- **Contato:** https://github.com/DamasoMagno

