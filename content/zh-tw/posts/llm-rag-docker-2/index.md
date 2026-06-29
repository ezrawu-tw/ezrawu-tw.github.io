---
slug: llm-rag-docker-2
copyright: true
title: Anything LLM 安裝 MacOS 篇
date: 2026-01-23 11:00:00
updated:
tags:
categories:
  - Note
keywords:
description:
top_img:
cover:
---


# MacOS 如何安裝 Anything LLM

## 步驟 1：安裝 Homebrew（如未安裝）
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew doctor
```

## 步驟 2：安裝 Docker Desktop for Mac

```
brew install --cask docker
open -a Docker  # 啟動 Docker Desktop，首次啟動可能需手動授權
```

啟動後，請等候 Docker 小鯨魚圖示變成綠色，表示成功啟動。
確認安裝成功：

```
docker --version
```

## 步驟 3：安裝 Node.js 和 Yarn

```
brew install node
npm install -g yarn
```

確認 Node.js 版本為 18 或以上：
```
node -v
```

## 步驟 4：建立資料夾並拉取 AnythingLLM 映像檔

```
export STORAGE_LOCATION=$HOME/anythingllm
mkdir -p "$STORAGE_LOCATION"
touch "$STORAGE_LOCATION/.env"
docker pull mintplexlabs/anythingllm
```

## 步驟 5：使用 Docker 執行 AnythingLLM

```
docker run -d -p 3001:3001 \
  --cap-add SYS_ADMIN \
  --add-host=host.docker.internal:host-gateway \
  -v ${STORAGE_LOCATION}:/app/server/storage \
  -v ${STORAGE_LOCATION}/.env:/app/server/.env \
  -e STORAGE_DIR="/app/server/storage" \
  mintplexlabs/anythingllm
```

執行後會返回類似這樣的容器 ID：

```
a1b2c3d4e5f6...
```

## 步驟 6：使用 AnythingLLM

打開瀏覽器前往：

```
http://localhost:3001
```
應該會看到 AnythingLLM 的 Web UI

## 補充：接上本機的 Ollama 模型

1. 請先安裝並啟動 Ollama。
2. 修改 .env 檔案內容如下（可使用 nano、vim 或 code 編輯）：
```
echo 'OLLAMA_BASE_PATH=http://host.docker.internal:11434' >> "$STORAGE_LOCATION/.env"
echo 'EMBEDDING_BASE_PATH=http://host.docker.internal:11434' >> "$STORAGE_LOCATION/.env"

```
3. 重新啟動容器（先停止再重啟）：

```
docker ps  # 找到 Container ID
docker stop <CONTAINER_ID>
docker start <CONTAINER_ID>
```