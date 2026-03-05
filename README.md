# GrtFood 2.0

Sistema de gestão de pedidos de refeição — Garten.

## Estrutura

Este repositório usa **Git Submodules** para organizar backend e frontend como projetos independentes:

```
grtnovo/
├── backend/   → submodule: Grtfood-backend (FastAPI + SQLModel)
├── frontend/  → submodule: Grtfood-frontend (Next.js + TypeScript)
└── README.md
```

## Clonando o projeto

```bash
git clone --recurse-submodules https://github.com/markzapxd/Grtfood-2.0.git
```

Ou, se já clonou sem `--recurse-submodules`:

```bash
git submodule init
git submodule update
```

## Atualizando submodules

```bash
git submodule update --remote --merge
```

## Backend

- **Stack:** FastAPI, SQLModel, Uvicorn, APScheduler
- **Repo:** https://github.com/markzapxd/Grtfood-backend

```bash
cd backend
pip install -e .
uvicorn app.main:app --reload
```

## Frontend

- **Stack:** Next.js 15, TypeScript, Tailwind CSS
- **Repo:** https://github.com/markzapxd/Grtfood-frontend

```bash
cd frontend
npm install
npm run dev
```

## Rodando com Docker (build único)

Na raiz do projeto (`grtnovo/`):

```bash
docker compose up --build
```

Aplicação unificada:

- Frontend + Backend: http://localhost:8082

Comandos úteis:

```bash
# subir em background
docker compose up -d --build

# ver logs
docker compose logs -f

# parar e remover containers
docker compose down
```

### Usando banco PostgreSQL já existente na máquina

O `docker-compose.yml` atual sobe apenas a aplicação e usa o banco externo via `DATABASE_URL`.

No arquivo `backend/.env`, ajuste:

```dotenv
DATABASE_URL=postgresql://USUARIO:SENHA@host.docker.internal:5432/NOME_DO_BANCO
```

Depois suba normalmente:

```bash
docker compose up -d --build
```
