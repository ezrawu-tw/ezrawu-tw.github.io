---
slug: llm-rag-docker-2
copyright: true
title: AnythingLLM Installation — MacOS
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
slug: llm-rag-docker-2

# How to Install AnythingLLM on MacOS

## Step 1: Install Homebrew (if not already installed)
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew doctor
```

## Step 2: Install Docker Desktop for Mac

```
brew install --cask docker
open -a Docker  # Launch Docker Desktop; first launch may require manual authorization
```

After launching, wait for the Docker whale icon in the menu bar to turn green, indicating a successful start.
Verify the installation:

```
docker --version
```

## Step 3: Install Node.js and Yarn

```
brew install node
npm install -g yarn
```

Confirm the Node.js version is 18 or above:
```
node -v
```

## Step 4: Create a folder and pull the AnythingLLM image

```
export STORAGE_LOCATION=$HOME/anythingllm
mkdir -p "$STORAGE_LOCATION"
touch "$STORAGE_LOCATION/.env"
docker pull mintplexlabs/anythingllm
```

## Step 5: Run AnythingLLM with Docker

```
docker run -d -p 3001:3001 \
  --cap-add SYS_ADMIN \
  --add-host=host.docker.internal:host-gateway \
  -v ${STORAGE_LOCATION}:/app/server/storage \
  -v ${STORAGE_LOCATION}/.env:/app/server/.env \
  -e STORAGE_DIR="/app/server/storage" \
  mintplexlabs/anythingllm
```

After running, a container ID similar to the following will be returned:

```
a1b2c3d4e5f6...
```

## Step 6: Use AnythingLLM

Open your browser and go to:

```
http://localhost:3001
```
You should see the AnythingLLM Web UI.

## Bonus: Connecting to a Local Ollama Model

1. Make sure Ollama is installed and running.
2. Edit the .env file as follows (you can use nano, vim, or code):
```
echo 'OLLAMA_BASE_PATH=http://host.docker.internal:11434' >> "$STORAGE_LOCATION/.env"
echo 'EMBEDDING_BASE_PATH=http://host.docker.internal:11434' >> "$STORAGE_LOCATION/.env"

```
3. Restart the container (stop then start):

```
docker ps  # find the Container ID
docker stop <CONTAINER_ID>
docker start <CONTAINER_ID>
```
