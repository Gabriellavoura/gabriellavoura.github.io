---
title: How to Run Ollama on Google Colab - A Quick Guide
date: 2025-03-21 23:30:00 -0300
categories: [Ollama, AI, HowTo]
tags: [ai, ollama, Howto]   # TAG names should always be lowercase
pin: true
---

Ok, this is just another "how-to google colab" tutorial... but the propose of this post is  more a note for the future self.

## Step 1 - Install colab-xterm
So first of all we need to have access to a terminal within the google colab code cell, this way we can install ollama via a shell script.

```shell
!pip install colab-xterm  
%load_ext colabxterm
```

This script will installs the [colab-xterm](https://github.com/InfuseAI/colab-xterm) package (Perhaps, awesome tool! thanks @popcornylu, you're awesome), which allows us to use a terminal within our colab notebook.
## Step 2 - Open a Terminal and install Ollama

To open a terminal just run the following command in a new cell
```shell
%xterm
#curl -fsSL https://ollama.com/install.sh|sh
#ollama serve & ollama pull llama3.2
```
Then, paste the curl and ollama commands in the shell and wait, then you've done!

## Step 3 - Test the installation

Create a new cell and run

```shell
! ollama list
```

It should return the name, ID, size and last modified date.

If it is all good, now you should have an running ollama server with llama3.2 model with 3b parameters prepared to be used.

A note from the past: you're welcome Gabriel ;)