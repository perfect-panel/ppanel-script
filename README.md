<div align="center">

<img width="160" src="https://raw.githubusercontent.com/perfect-panel/ppanel-assets/refs/heads/main/logo.svg">

<h1>PPanel Quick Deployment Guide</h1>

This is a quick deployment script provided by PPanel

English · [中文](./README.zh-CN.md)

</div>

### Script Deployment

Run the following commands to deploy PPanel:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/perfect-panel/ppanel-script/refs/heads/main/install.sh)
```

```bash
bash <(wget -qO- https://raw.githubusercontent.com/perfect-panel/ppanel-script/refs/heads/main/install.sh)
```

### Local Development

`compose.yaml` brings up the whole stack on your machine. This is the `develop`
environment: everything runs locally, nothing is published, and there are no
hostnames — you reach it over `localhost`.

```bash
docker compose up -d
```

| Service | Address |
| --- | --- |
| Backend API | `http://localhost:8080` |
| Admin web | `http://localhost:3001` |
| User web | `http://localhost:3002` |
| PostgreSQL | `localhost:5432`, database `ppanel`, data in `./db` |
| Redis | `localhost:6379`, data in `./cache` |

Backend settings live in `config/ppanel.yaml`. The default administrator is
`admin@ppanel.dev` / `password` — change it before exposing this to anything.

## Everything is built from local source

All three services are built by compose from **sibling repositories**, not pulled
from upstream — `ppanel/*:latest` contains none of this fork's changes, so
developing against it means you are not running your own code at all.

```
~/github/phenix3443/ppanel/
├── ppanel-script/     ← you are here
├── ppanel-server/
└── ppanel-frontend/
```

Override the paths if your layout differs:

```sh
PPANEL_SERVER_PATH=/path/to/server PPANEL_FRONTEND_PATH=/path/to/frontend \
  docker compose up -d --build
```

**Whatever branch each repo has checked out is what gets built.** Check out the
branch you want to verify, then rebuild:

```sh
docker compose up -d --build ppanel-server     # rebuild the backend only
docker compose up -d --build ppanel-admin      # rebuild the admin app only
```

For high-frequency frontend work `bun dev` (HMR) is far faster than rebuilding
an image; rebuild only when you need to check the packaged result.

`develop` has its own database and shares nothing with the `test` deployment.

## Upgrading from the MySQL stack

`./db` holds a MySQL data directory; Postgres refuses to initialise into a
non-empty directory and will fail to start. Local data is disposable:

```sh
docker compose down && rm -rf ./db && docker compose up -d
```
