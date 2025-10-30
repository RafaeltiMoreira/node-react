# Web + API — Projeto (simplificado)

Repositório com 2 apps -> `api` (backend em Node/TypeScript + Fastify) e `web` (frontend em React + Vite).

## Tecnologias principais

- API: Node.js, TypeScript, Fastify, Drizzle ORM, Zod, PostgreSQL (pg), tsx
- Web: React, TypeScript, Vite
- Monorepo: pnpm (workspace)
- Ferramentas dev: TypeScript, Vite, tsx, Drizzle CLI

## Pré-requisitos

- Node.js (recomenda-se v18+)
- pnpm (instale via `npm i -g pnpm` ou conforme preferir)
- Docker (opcional, usado para banco se quiser rodar via `docker-compose`)

## Instalação (rápida)

No diretório raiz do projeto:

```powershell
pnpm install
```

Isto instalará as dependências do workspace. Também é possível instalar separadamente em cada pacote (`api` / `web`) se preferir.

## Rodando localmente

1) API

- Entre na pasta da API e rode em modo desenvolvimento:

```powershell
cd api
pnpm install
pnpm dev
```

- O script `dev` usa `tsx` para watch e `.env` (ver `api/.env`). Por padrão os logs indicam que a API ficará disponível em `http://localhost:3333` e a documentação em `http://localhost:3333/docs`.

- Migrations / Drizzle:

```powershell
pnpm db:generate   # gerar tipos/schema (drizzle-kit)
pnpm db:migrate    # aplicar migrations
pnpm db:studio     # abrir studio
```

- Alternativa com Docker (se desejar rodar DB via compose):

```powershell
cd api
docker-compose up -d
```

2) Web (frontend)

```powershell
cd web
pnpm install
pnpm dev
```

- Por padrão o Vite abre em `http://localhost:5173` (ou outra porta livre).

3) Build / preview do front

```powershell
cd web
pnpm build
pnpm preview
```

## Variáveis de ambiente

- A API usa um arquivo `.env` na pasta `api/` (já existe um arquivo `.env` no repositório). Verifique e preencha valores como `DATABASE_URL`, `PORT` ou outras variáveis necessárias.

## Endpoints úteis

- A rota de listagem de webhooks está registrada em `src/routes/list-webhooks.ts` (API).
- A documentação OpenAPI/Swagger fica em `/docs` (ex.: `http://localhost:3333/docs`).

## Estrutura (resumida)

- `api/` — backend (TypeScript)
  - `src/server.ts` — inicialização do Fastify
  - `src/routes/` — rotas (ex.: `list-webhooks.ts`)
  - `db/` — migrations e configurações do Drizzle
- `web/` — frontend (Vite + React)
  - `src/` — código React

## Como testar rápido

1. Rodar API (ver seção acima)
2. Rodar web
3. Acessar o front e executar ações que disparem chamadas para a API ou abrir `http://localhost:3333/docs` para testar endpoints via Swagger

## Observações e boas práticas

- Use `pnpm` para aproveitar o workspace (instala as dependências com rapidez e consistência).
- Antes de rodar a API, verifique `api/.env` e o estado do banco (migrations). Use `pnpm db:migrate` após configurar o banco.
- Se houver dúvidas sobre scripts, confira `api/package.json` e `web/package.json` — os scripts principais são `dev`, `build` (web) e `dev`, `start`, `db:migrate` (api).

---

Se quiser, posso também:

- Adicionar exemplos de `.env` (modelo) com as variáveis mínimas exigidas pela API.
- Criar um README separado e mais detalhado dentro de `api/` e `web/`.