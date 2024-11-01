<div align="center">

<img width="160" src="https://raw.githubusercontent.com/perfect-panel/ppanel-assets/refs/heads/main/logo.svg">

<h1>PPanel 快速部署指南</h1>

这是由 PPanel 提供支持快速部署脚本

[英文](./README.md)
·
中文
</div>

## 注意事项
- 请确保 Docker 和 Docker Compose 已正确安装。
- 修改环境变量文件以适应您的实际部署需求，确保配置正确无误。

## Docker 和 Docker Compose 安装
请确保 Docker 和 Docker Compose 已正确安装。可以参考以下链接进行安装：
- [Docker 安装指南](https://docs.docker.com/get-docker/)
- [Docker Compose 安装指南](https://docs.docker.com/compose/install/)

## Git 仓库克隆
首先克隆项目的 Git 仓库：
```sh
git clone https://github.com/perfect-panel/ppanel-script.git
cd ppanel-script
```
## 开始部署

### 1. 管理端部署 [环境变量说明](https://docs.ppanel.dev/zh-CN/docs/admin#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)
```sh
 docker-compose -f ppanel-admin-web.yml up -d
```

### 2. 用户端部署 [环境变量说明](https://docs.ppanel.dev/zh-CN/docs/user#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)
```sh
 docker-compose -f ppanel-user-web.yml up -d
```

### 3. 前端部署（适用于管理端和用户端, 环境变量同上）
```sh
 docker-compose -f ppanel-web.yml up -d
```




