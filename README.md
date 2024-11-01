<div align="center">

<img width="160" src="https://raw.githubusercontent.com/perfect-panel/ppanel-assets/refs/heads/main/logo.svg">

<h1>PPanel Quick Deployment Guide</h1>

This script is provided by PPanel for fast deployment.

English
·
[中文](./README.zh-CN.md)
</div>

## Important Notes
- Please ensure that Docker and Docker Compose are properly installed.
- Modify the environment variable file to suit your actual deployment needs and ensure that the configuration is correct.

## Docker and Docker Compose Installation
Make sure Docker and Docker Compose are installed properly. You can refer to the following links for installation:
- [Docker Installation Guide](https://docs.docker.com/get-docker/)
- [Docker Compose Installation Guide](https://docs.docker.com/compose/install/)

## Clone Git Repository
First, clone the Git repository of the project:
```sh
git clone https://github.com/perfect-panel/ppanel-script.git
cd ppanel-script
```
## Start Deployment

### 1. Admin Panel Deployment [Environment Variables Explanation](https://docs.ppanel.dev/en-US/docs/admin#environment-variables)
```sh
 docker-compose -f ppanel-admin-web.yml up -d
```

### 2. User Panel Deployment [Environment Variables Explanation](https://docs.ppanel.dev/en-US/docs/user#environment-variables)
```sh
 docker-compose -f ppanel-user-web.yml up -d
```

### 3. Frontend Deployment (Applies to both Admin and User Panels, same environment variables as above)
```sh
 docker-compose -f ppanel-web.yml up -d
```
