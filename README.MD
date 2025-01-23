# cursor-api

将 Cursor 编辑器转换为 OpenAI 兼容的 API 接口服务。

## 项目简介

本项目提供了一个代理服务，可以将 Cursor 编辑器的 AI 能力转换为与 OpenAI API 兼容的接口，让您能够在其他应用中复用 Cursor 的 AI 能力。

## 使用前准备

1. 访问 [www.cursor.com](https://www.cursor.com) 并完成注册登录（赠送 500 次快速响应，可通过删除账号再注册重置）
2. 在浏览器中打开开发者工具（F12）
3. 找到 应用-Cookies 中名为 `WorkosCursorSessionToken` 的值并保存(相当于 openai 的密钥)

## 接口说明

### 基础配置

- 接口地址：`http://localhost:3000/v1/chat/completions`
- 请求方法：POST
- 认证方式：Bearer Token（使用 WorkosCursorSessionToken 的值，支持英文逗号分隔的 key 入参）

### 请求格式和响应格式参考 openai

## 生产环境部署

> 注意：系统会根据您提供的 WorkosCursorSessionToken 自动生成合适的 checksum，无需手动设置。

### Docker 方式一：直接运行

```bash
docker run -d --name cursor-api -p 3000:3000 301redirect/cursor2api:latest
```

### Docker 方式二：Docker Compose

创建 `docker-compose.yml` 文件：

```yaml
version: '3.8'

services:
  cursor2api:
    image: 301redirect/cursor2api:latest
    ports:
      - "3000:3000"
    environment:
      - TZ=Asia/Shanghai
    restart: unless-stopped
    # 如果需要持久化存储，可以取消下面的注释
    # volumes:
    #   - ./data:/app/data
```

运行服务：
```bash
docker compose up -d
```

## 本地开发

```bash
cd cursor-api
npm install
npm run dev
```

## 注意事项

- 请妥善保管您的 WorkosCursorSessionToken，不要泄露给他人
- 本项目仅供学习研究使用，请遵守 Cursor 的使用条款

## 原始项目

- 本项目基于 [cursorToApi](https://github.com/luolazyandlazy/cursorToApi) 项目进行优化，感谢原作者的贡献

## 许可证

MIT License