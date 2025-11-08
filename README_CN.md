## Docker 本地部署

启动容器

```bash
docker run -p 80:8080 --name chatbot -dit \
    -e BOT_TOKEN=your_telegram_bot_token \
    -e API_KEY= \
    -e BASE_URL= \
    -v ./user_configs:/home/user_configs \
    yym68686/chatgpt:latest
```

或者如果你想使用 Docker Compose，这里有一个 docker-compose.yml 示例：

```yaml
version: "3.5"
services:
  chatgptbot:
    container_name: chatgptbot
    image: yym68686/chatgpt:latest
    environment:
      - BOT_TOKEN=
      - API_KEY=
      - BASE_URL=
    volumes:
      - ./user_configs:/home/user_configs
    ports:
      - 80:8080
```

在后台运行 Docker Compose 容器

```bash
docker compose pull
docker compose up -d

# uni-api
docker compose -f docker-compose-uni-api.yml up -d
```

将存储库中的Docker镜像打包并上传到Docker Hub

```bash
docker buildx build --platform linux/amd64,linux/arm64 -t yym68686/chatgpt:latest -f Dockerfile.build --no-cache --push .
docker push yym68686/chatgpt:latest
```

一键重启 Docker 镜像

```bash
set -eu
docker pull yym68686/chatgpt:latest
docker rm -f chatbot
docker run -p 8080:8080 -dit --name chatbot \
-e BOT_TOKEN= \
-e API_KEY= \
-e BASE_URL= \
-e GOOGLE_API_KEY= \
-e GOOGLE_CSE_ID= \
-e claude_api_key= \
-v ./user_configs:/home/user_configs \
yym68686/chatgpt:latest
docker logs -f chatbot
```

该脚本用于通过单个命令重启Docker镜像。它首先删除名为"chatbot"的现有Docker容器（如果存在）。然后，它运行一个名为"chatbot"的新Docker容器，暴露端口8080并设置各种环境变量。使用的Docker镜像是"yym68686/chatgpt:latest"。最后，它跟踪"chatbot"容器的日志。
