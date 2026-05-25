---
slug: llm-rag-docker
copyright: true
title:  Anything LLM 安裝 Windows 篇
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
slug: llm-rag-docker

# Windows Install

```
WSL (Windows Subsystem for Linux) 是微軟開發的一項功能，允許使用者在 Windows 10/11 或 Windows Server 上，不需虛擬機 (VM) 或雙開機，即可原生執行 Linux 二進制可執行檔
```
## 使用WSL (Ubuntu22.4) 安裝 docker 
### 步驟 1: 檢查 WSL 版本

```
wsl -v
```

### 步驟 2: 安裝 Ubuntu 22.04 LTS
```
wsl --install -d Ubuntu-22.04
```
安裝完成後，會要求你創建一個 UNIX 用戶帳戶，你創建了用戶名 。
### 步驟 3: 在 WSL 中安裝 Docker

```
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
newgrp docker  # 讓群組設定立即生效

```

### 步驟 4: 安裝 Node.js 與 Yarn

```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g yarn
```

### 步驟 5: 建立本機資料夾並拉取映像檔(image)

```
export STORAGE_LOCATION=$HOME/anythingllm
mkdir -p $STORAGE_LOCATION
touch "$STORAGE_LOCATION/.env"
docker pull mintplexlabs/anythingllm

```

### 步驟 6: 使用 Docker 執行 AnythingLLM

```
docker run -d -p 3001:3001 \
  --cap-add SYS_ADMIN \
  --add-host=host.docker.internal:host-gateway \
  -v ${STORAGE_LOCATION}:/app/server/storage \
  -v ${STORAGE_LOCATION}/.env:/app/server/.env \
  -e STORAGE_DIR="/app/server/storage" \
  mintplexlabs/anythingllm
```
執行完成後，系統回傳了容器 ID

### 步驟 7: 使用 AnythingLLM
打開瀏覽器並訪問：
```
http://localhost:3001

```

## Ollama Docker

## 拉取ollama 鏡像
```
docker pull ollama/ollama:0.14.3-rc3
```

### 運行ollama
```
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```







