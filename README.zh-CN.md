<div align="center">

<img width="160" src="https://raw.githubusercontent.com/perfect-panel/ppanel-assets/refs/heads/main/logo.svg">

<h1>PPanel 快速部署指南</h1>

这是由 PPanel 提供支持的快速部署脚本

[英文](./README.md) · 中文

</div>

## 脚本部署

运行以下命令来部署 PPanel：

```sh
bash <(curl -fsSL https://raw.githubusercontent.com/perfect-panel/ppanel-script/refs/heads/main/install.sh)
```

```sh
bash <(wget -qO- https://raw.githubusercontent.com/perfect-panel/ppanel-script/refs/heads/main/install.sh)
```

## 本地开发

`compose.yaml` 在本机拉起整套服务。这就是 `develop` 环境：全部跑在本地，
不发布任何东西，也没有域名——通过 `localhost` 访问。

```sh
docker compose up -d
```

| 服务 | 地址 |
| --- | --- |
| 后端 API | `http://localhost:8080` |
| 管理端 | `http://localhost:3001` |
| 用户端 | `http://localhost:3002` |
| PostgreSQL | `localhost:5432`，库 `ppanel`，数据在 `./db` |
| Redis | `localhost:6379`，数据在 `./cache` |

后端配置在 `config/ppanel.yaml`。默认管理员是 `admin@ppanel.dev` / `password`，
往任何能被别人访问的地方放之前先改掉。

## 跑的是本地源码

三个服务都由 compose 从**相邻仓库的源码**构建，不拉上游镜像——上游的
`ppanel/*:latest` 里没有我们 fork 的任何东西，拿它开发等于没跑。

```
~/github/phenix3443/ppanel/
├── ppanel-script/     ← 你在这里
├── ppanel-server/     ← 后端源码
└── ppanel-frontend/   ← 前端源码
```

路径不是这样的话用环境变量覆盖：

```sh
PPANEL_SERVER_PATH=/path/to/server PPANEL_FRONTEND_PATH=/path/to/frontend docker compose up -d --build
```

**构建的是各仓库当前 checkout 的那个分支。** 想验某个分支就先切过去再 `--build`。

改完代码重建单个服务：

```sh
docker compose up -d --build ppanel-server     # 只重建后端
docker compose up -d --build ppanel-admin      # 只重建管理端
```

前端改样式这类高频改动，用 `bun dev`（HMR，秒级）比重建镜像快得多；
要验「打成镜像之后还对不对」时才走上面这条。

`develop` 有自己独立的数据库，和 `test` 部署不共享任何东西。

## 从 MySQL 版升上来

`./db` 里是 MySQL 的数据目录，Postgres 拒绝往非空目录初始化，会起不来。
本机数据没有保留价值，直接删掉重来：

```sh
docker compose down && rm -rf ./db && docker compose up -d
```
