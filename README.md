# WordPress 多容器部署方案（Docker Compose）

基于 Docker Compose 编排的 WordPress 生产级环境，包含 Nginx 反向代理、MySQL 数据库和 WordPress 应用。配置了健康检查、启动依赖和重定向修正，适合学习容器编排、反向代理及云原生应用部署。

## 特性

- **多容器编排**：Nginx + WordPress + MySQL 分离部署，职责清晰。
- **数据持久化**：数据库和网站文件使用 Docker 命名卷保存，重启不丢失。
- **健康检查与启动依赖**：MySQL 容器配置健康检查，WordPress 等待数据库完全就绪后再启动，避免连接失败。
- **Nginx 反向代理与重定向修正**：配置 `proxy_redirect` 解决 WordPress 在反向代理后的地址跳转问题。
- **开箱即中文**：容器网络经 DNS 优化，安装时自动获取中文语言包，无需手动配置。
- **配置安全**：敏感信息通过 `.env` 文件管理（不上传公开仓库），公开仓库使用占位符。

## 快速开始

### 1. 环境要求

- [Docker](https://docs.docker.com/engine/install/) 20.10+
- [Docker Compose](https://docs.docker.com/compose/install/) 2.0+（支持 `docker compose` 命令）
- 确保 **8080 端口**未被占用（如需修改，请编辑 `docker-compose.yml` 中 nginx 服务的 `ports` 字段）
- 虚拟机/服务器需能访问外网（用于下载语言包和插件）。  
  *若使用仅主机模式，请改用 NAT 或桥接模式。*

### 2. 克隆项目

```bash
git clone https://github.com/oreo-Calar/docker-wordpress-deploy.git
cd docker-wordpress-deploy