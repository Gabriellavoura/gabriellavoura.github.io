---
title: How to Run Ollama on Docker - A Quick Guide
date: 2025-03-13 23:30:00 -0300
categories: [Docker, Ollama, AI, HowTo]
tags: [ai, docker, ollama, howto]   # TAG names should always be lowercase
pin: true
---

Hi it's me again!

Over the past few days, I've been testing multiples ways to work with LLMs locally, and so far, Ollama was the best tool (ignoring UI and other QoL aspects) for setting up a fast environment to test code and features.

I've tried GPT4ALL  and other tools before, but they seem overly bloated when the goal is simply to set up a running model to connect with a LangChain API (on Windows with WSL).

Ollama provides an extremely straightforward experience. Because of this, today I decided to install and use it via Docker containers — and it's surprisingly easy and powerful..

With just five commands, we can set up the environment. Let's take a look.
## Step 1 - Pull the latest Ollama Docker image

```bash
docker pull ollama/ollama
```
If you want to download an older version, you can specify the corresponding tag after the container name. By default, the `:latest` tag is downloaded. You can check a list of available Ollama tags [here] (https://hub.docker.com/r/ollama/ollama/tags).
## Step 2 - Create a Docker network

Since we'll typically use and connect multiple containers, we need to specify a shared communication channel. To achieve this, it's a  good practice create a Docker [network](https://hub.docker.com/r/ollama/ollama/tags).

```bash
docker network create <network-name>
```

You can check a list of created Docker networks by running the following command:

```bash
docker network list
```

## Step 3 - Run the Ollama container

In this tutorial, we're going to run Ollama with CPU only. If you need to use GPU, the [official documentation](https://hub.docker.com/r/ollama/ollama) provide a step-by-step guide.

The command is listed in the documentation, but we need to specify which network it should connect to, so we must add the `--netowk` parameter.
```bash
docker run -d --netowk <network-name> -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```


## Step 4 - Run commands inside the Ollama container

To download Ollama models, we need to run `ollama pull` command.

To do this, we simply execute the command below, which enables the execution inside the container by enabling the interative mode (`-it` parameter).  Then, we run `ollama pull` to download the `llama3.2:latest` (3B), quantized model:

```bash
docker exec -it ollama ollama pull llama3.2
```

Visit the Ollama website to check the list of [available models](https://ollama.com/search).

## Step 5 - Check the downloaded models

To list the locally available models, just run:
```shell
ollama list
```

You should get this output:


So you're done! Now you have Ollama running `llama3.2:latest` model locally (using only the CPU). To run it with a GPU, check the documentation link in **Step 3**.

I'll share more short notes on working with Ollama and LangChain in the next few days. Stay tuned!