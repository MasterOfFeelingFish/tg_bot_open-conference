<p align="center">
<img src="./assets/logo-3071751.jpg">
</p>

# 🤖️ TeleChat

[英文](README.md) | [中文](README_CN.md)

<p align="center">
  <a href="https://t.me/+_01cz9tAkUc1YzZl">
    <img src="https://img.shields.io/badge/Join Telegram Group-blue?&logo=telegram">
  </a>
  <a href="https://t.me/chatgpt68_bot">
    <img src="https://img.shields.io/badge/Telegram Bot-grey?&logo=Probot">
  </a>
   <a href="https://hub.docker.com/repository/docker/yym68686/chatgpt">
    <img src="https://img.shields.io/docker/pulls/yym68686/chatgpt?color=blue" alt="docker pull">
  </a>
</p>

ChatGPT Telegram 机器人是一个强大的 Telegram 机器人，支持兼容 OpenAI 格式的大语言模型 API。它使用户能够在 Telegram 上进行高效的对话和信息搜索。对于 Anthropic, Gemini, Vertex AI, Azure, AWS, xai, Cohere, Groq, Cloudflare, OpenRouter 等其他提供商的模型的支持，请使用我的另一个项目 [uni-api](https://github.com/yym68686/uni-api) 进行集成，以减少维护成本，感谢您的理解。

## ✨ 功能

- **多种AI模型**：支持兼容 OpenAI 格式的 API。对于 Anthropic, Gemini, Vertex AI, Azure, AWS, xai, Cohere, Groq, Cloudflare, OpenRouter 等其他提供商的模型，请使用 [uni-api](https://github.com/yym68686/uni-api) 进行集成。同时支持 one-api/new-api。利用自研 API 请求后端 [SDK](https://github.com/yym68686/aient)，不依赖 OpenAI SDK。
- **多模态问答**：支持语音、音频、图像和 PDF/TXT/MD/python 文档的问答。用户可以直接在聊天框中上传文件使用。
- **群聊主题模式**: 支持在群聊中启用主题模式，在主题之间隔离API、对话历史、插件配置和偏好设置。
- **丰富的插件系统**：支持网页搜索（DuckDuckGo和Google）、URL 总结、ArXiv 论文总结和代码解释器。
- **用户友好界面**：允许在聊天窗口内灵活切换模型，并支持类似打字机效果的流式输出。支持精确的 Markdown 消息渲染，利用了我的另一个[项目](https://github.com/yym68686/md2tgmd)。
- **高效消息处理**：异步处理消息，多线程回答问题，支持隔离对话，并为不同用户提供独特对话。
- **长文本消息处理**: 自动合并长文本消息，突破Telegram的单条消息长度限制。当机器人的回复超过Telegram的限制时，它将被拆分成多条消息。
- **多用户对话隔离**：支持对话隔离和配置隔离，允许在多用户和单用户模式之间进行选择。
- **问题预测**: 自动生成后续问题，预测用户可能会接下来询问的问题。
- **多语言界面**：支持简体中文、繁体中文、俄文和英文界面。
- **白名单、黑名单和管理员设置**：支持设置白名单、黑名单和管理员。
- **内联模式**：允许用户在任何聊天窗口中 @ 机器人以生成答案，而无需在机器人的聊天窗口中提问。
- **方便部署**：支持一键部署到 koyeb、Zeabur、Replit，真正零成本和傻瓜式部署流程。还支持 kuma 防休眠，以及 Docker 和 fly.io 部署。
- **模型分组系统**: 将AI模型组织成逻辑组，便于选择。模型可以按提供商（GPT、Claude等）或按功能进行分组。没有明确指定组的模型会自动放入"OTHERS"组。这使得模型选择更直观，特别是当有很多模型可用时。

## 🍃 环境变量

以下是与机器人核心设置相关的环境变量列表：

| 变量名称 | 描述 | 是否必需? |
|---------------|-------------|-----------|
| BOT_TOKEN | Telegram 机器人令牌。 在 [BotFather](https://t.me/BotFather) 上创建一个机器人以获取 BOT_TOKEN。 | **是** |
| API_KEY | OpenAI 或第三方 API 密钥。 | 是 |
| MODEL | 设置默认的QA模型；默认是：`gpt-5`。此项可以使用机器人的"info"命令自由切换，原则上不需要设置。 | 否 |
| WEB_HOOK | 每当电报机器人收到用户消息时，消息将被传递到 WEB_HOOK，机器人将在此监听并及时处理收到的消息。 | 否 |
| BASE_URL | 如果您使用的是OpenAI官方API，则无需设置此项。如果您使用的是第三方API，则需要填写第三方代理网站。默认值是：https://api.openai.com/v1/chat/completions | 否 |
| NICK | 默认是空的，NICK 是机器人的名字。机器人只会在用户输入的消息以 NICK 开头时才会响应，否则机器人会响应任何消息。特别是在群聊中，如果没有 NICK，机器人会回复所有消息。 | 否 |
| GOOGLE_API_KEY | 如果你需要使用谷歌搜索，你需要设置它。如果你不设置这个环境变量，机器人将默认提供duckduckgo搜索。 | No |
| GOOGLE_CSE_ID | 如果你需要使用谷歌搜索，你需要和 GOOGLE_API_KEY 一起设置。 | 否 |
| whitelist | 设置哪些用户可以访问机器人，并用 ',' 连接被授权使用机器人的用户ID。默认值是 `None`，这意味着机器人对所有人开放。 | 否 |
| BLACK_LIST | 设置哪些用户禁止访问机器人，并用 ',' 连接被授权使用机器人的用户ID。默认值是 `None` | 否 |
| ADMIN_LIST | 设置管理员列表。只有管理员可以使用 `/info` 命令配置机器人。 | 否 |
| GROUP_LIST | 设置可以使用机器人的群组列表。使用逗号（'，'）连接群组ID。即使群组成员不在白名单中，只要群组ID在GROUP_LIST中，群组的所有成员都可以使用机器人。 | 否 |
| CUSTOM_MODELS | 设置自定义模型名称列表。使用逗号（','）连接模型名称。如果需要删除默认模型，请在默认模型名称前添加连字符（-）。如果要删除所有默认模型，请使用 `-all`。要创建模型组，使用分号（';'）分隔组，使用冒号（':'）定义组名及其模型，例如：`CUSTOM_MODELS=-all,command,grok-2;GPT:gpt-5,gpt-3.5-turbo;Claude:claude-3-opus,claude-3-sonnet;OTHERS`。没有特定组的模型将自动放入"OTHERS"组。 | 否 |
| CHAT_MODE | 引入多用户模式，不同用户的配置不共享。当 CHAT_MODE 为 `global` 时，所有用户共享配置。当 CHAT_MODE 为 `multiusers` 时，用户配置彼此独立。 | 否 |
| temperature | 指定 LLM 的温度。默认值是 `0.5`。 | 否 |
| GET_MODELS | 指定是否通过 API 获取支持的模型。默认值为 `False`。 | 否 |
| SYSTEMPROMPT | 指定系统提示，系统提示是字符串，例如：`SYSTEMPROMPT=You are ChatGPT, a large language model trained by OpenAI. Respond conversationally`。默认是 `None`。系统提示的设置仅在 `CHAT_MODE` 为 `global` 时，系统提示的设置才会有效。当 `CHAT_MODE` 为 `multiusers` 时，系统提示的环境变量无论是任何值都不会修改任何用户的系统提示，因为用户不希望自己设置的系统系统被修改为全局系统提示。 | 否 |
| LANGUAGE | 指定机器人显示的默认语言，包括按钮显示语言和对话语言。默认是 `English`。目前仅支持设置为下面四种语言：`English`，`Simplified Chinese`，`Traditional Chinese`，`Russian`。同时也可以在机器人部署后使用 `/info` 命令设置显示语言 | 否 |
| CONFIG_DIR | 指定存储用户配置文件夹。CONFIG_DIR 是用于存储用户配置的文件夹。每次机器人启动时，它都会从 CONFIG_DIR 文件夹读取配置，因此用户每次重新启动时不会丢失之前的设置。您可以在本地使用 Docker 部署时，通过使用 `-v` 参数挂载文件夹来实现配置持久化。默认值是 `user_configs`。 | 否 |
| RESET_TIME | 指定机器人每隔多少秒重置一次聊天历史记录，每隔 RESET_TIME 秒，机器人会重置除了管理员列表外所有用户的聊天历史记录，每个用户重置时间不一样，根据每个用户最后的提问时间来计算下一次重置时间。而不是所有用户在同一时间重置。默认值是 `3600` 秒，最小值是 `60` 秒。 | 否 |

以下是与机器人偏好设置相关的环境变量列表，偏好设置也可以通过机器人启动后使用 `/info` 命令，点击 `偏好设置` 按钮来设置：

| 变量名称 | 描述 | 必需的? |
|---------------|-------------|-----------|
| PASS_HISTORY | 默认值是 `9999`。机器人会记住对话历史，并在下次回复时考虑上下文。如果设置为 `0`，机器人将忘记对话历史，只考虑当前对话。PASS_HISTORY 的值必须大于或等于 0。对应于偏好设置里面的名为 `对话历史` 的按钮。 | 否 |
| LONG_TEXT | 如果用户的输入消息的文本长度超出了 Telegram 的限制，并在很短的时间内连续发送多个消息，机器人会将这些多个消息视为一个。默认值是 `True`。对应于偏好设置里面的名为 `长文本合并` 的按钮。 | 否 |
| IMAGEQA | 是否启用图像问答，默认设置是模型可以回答图像内容，默认值为 `True`。对应于偏好设置里面的名为 `图片问答` 的按钮。 | 否 |
| LONG_TEXT_SPLIT | 当机器人的回复超过Telegram限制时，它将被拆分为多个消息。默认值是 `True`。对应于偏好设置里面的名为 `长文本分割` 的按钮。 | 否 |
| FILE_UPLOAD_MESS | 当文件或图像上传成功并且机器人处理完成时，机器人将发送一条消息，提示上传成功。默认值为 `True`。对应于偏好设置里面的名为 `文件上传成功提示消息` 的按钮。 | 否 |
| FOLLOW_UP | 自动生成多个相关问题供用户选择。默认值为 `False`。对应于偏好设置里面的名为 `猜你想问` 的按钮。 | 否 |
| TITLE | 是否在机器人回复的开头显示模型名称。默认值为 `False`。对应于偏好设置里面的名为 `模型标题` 的按钮。 | 否 |
| REPLY | 机器人是否应以"回复"格式回复用户的消息。默认值为 `False`。对应于偏好设置里面的名为 `回复消息` 的按钮。 | 否 |
<!-- | TYPING | 是否在机器人回复时显示"正在输入"状态。默认值为 `False`。 | 否 | -->


以下是与机器人插件设置相关的环境变量列表：

| 变量名称 | 描述 | 必需的？ |
|---------------|-------------|-----------|
| get_search_results | 是否启用搜索插件。默认值为 `False`。 | 否 |
| get_url_content | 是否启用URL摘要插件。默认值为 `False`。 | 否 |
| download_read_arxiv_pdf | 是否启用arXiv论文摘要插件。默认值为 `False`。 | 否 |
| run_python_script | 是否启用代码解释器插件。默认值为 `False`。 | 否 |
| generate_image | 是否启用图像生成插件。默认值为 `False`。 | 否 |
| get_time | 是否启用日期插件。默认值为 `False`。 | 否 |


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
