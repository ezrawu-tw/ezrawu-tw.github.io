---
slug: llm-rag-docker
copyright: true
title: AnythingLLM Installation — Windows
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
WSL (Windows Subsystem for Linux) is a feature developed by Microsoft that allows users to natively run Linux binary executables on Windows 10/11 or Windows Server without needing a virtual machine (VM) or dual-boot setup.
```
## Installing Docker via WSL (Ubuntu 22.04)
### Step 1: Check WSL Version

```
wsl -v
```

### Step 2: Install Ubuntu 22.04 LTS
```
wsl --install -d Ubuntu-22.04
```
After the installation is complete, you will be prompted to create a UNIX user account and set a username.

### Step 3: Install Docker inside WSL

```
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
newgrp docker  # apply the group change immediately

```

### Step 4: Install Node.js and Yarn

```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g yarn
```

### Step 5: Create a local folder and pull the image

```
export STORAGE_LOCATION=$HOME/anythingllm
mkdir -p $STORAGE_LOCATION
touch "$STORAGE_LOCATION/.env"
docker pull mintplexlabs/anythingllm

```

### Step 6: Run AnythingLLM with Docker

```
docker run -d -p 3001:3001 \
  --cap-add SYS_ADMIN \
  --add-host=host.docker.internal:host-gateway \
  -v ${STORAGE_LOCATION}:/app/server/storage \
  -v ${STORAGE_LOCATION}/.env:/app/server/.env \
  -e STORAGE_DIR="/app/server/storage" \
  mintplexlabs/anythingllm
```
After it runs, the system will return a container ID.

### Step 7: Use AnythingLLM
Open your browser and navigate to:
```
http://localhost:3001

```

## Ollama Docker

## Pull the Ollama image
```
docker pull ollama/ollama:0.14.3-rc3
```

### Run Ollama
```
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```
