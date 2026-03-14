# OpenClaw Docker Compose

这是一个用于快速部署 [OpenClaw](https://github.com/openclaw/openclaw) 的 Docker Compose 配置文件。
用于以安全的容器化方式快速部署 OpenClaw

## 引用

- **Docker Hub 镜像**: [alpine/openclaw](https://hub.docker.com/r/alpine/openclaw)
- **GitHub 仓库**: [openclaw/openclaw](https://github.com/openclaw/openclaw)

---

## 项目组成

本配置包含两个主要服务：

1.  **openclaw-gateway**: 核心网关服务，处理所有外部请求和跨平台通信。
2.  **openclaw-cli**: 命令行工具，用于初始化配置、管理渠道和工作区。

## 配置与使用方法

### 1. 准备工作

确保你的系统中已安装 [Docker](https://www.docker.com/) 和 [Docker Compose](https://docs.docker.com/compose/)。

### 2. 获取配置文件

将 [docker-compose.yml](https://github.com/wangyucode/openclaw-docker-compose/docker-compose.yml) 下载到本地目录。

### 3. 修改配置

在启动服务之前，**必须修改** `docker-compose.yml` 中的 `OPENCLAW_GATEWAY_TOKEN`。

```yaml
environment:
  - OPENCLAW_GATEWAY_TOKEN=your-secret-token  # 请在此处替换为你的强密码令牌
```

确保 `openclaw-gateway` 和 `openclaw-cli` 的 `OPENCLAW_GATEWAY_TOKEN` 保持一致。

### 4. 启动服务

在终端中进入 `docker-compose.yml` 所在的目录，运行以下命令启动网关：

```bash
docker-compose up -d openclaw-gateway
```

### 5. 使用 CLI 进行初始化

使用 `openclaw-cli` 容器进入交互式命令行，进行初始化（如 onboarding）：

```bash
docker-compose run --rm openclaw-cli
```

在容器内部，你可以运行 `openclaw` 命令。例如，开始初始化流程：

```bash
openclaw onboard
```

### 6. 数据持久化

默认情况下，所有的配置和工作区数据将保存在当前目录下的 `./openclaw` 文件夹中。

## 端口说明

- `18789`: 网关主端口，用于 API 请求。
- `18790`: 桥接端口。

## 干净卸载

1. 停止所有服务：
    ```bash
    docker-compose down
    ```
2. 删除镜像：
    ```bash
    docker image prune
    ```
3. 删除./openclaw 目录：
    ```bash
    rm -rf ./openclaw
    ```



