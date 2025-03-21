---
title: How to Install CUDA on WSL2
date: 2025-03-20 23:30:00 -0300
categories: [WSL2, CUDA, HowTo]
tags: [wsl2]   # TAG names should always be lowercase
pin: true
---

Hello again!

This time I was trying to get my Ollama setup running on the GPU because I noticed that, by default, it was only using my CPU cores. I suspected that my CUDA drivers weren't set up correctly on WSL2.

Here are the steps I followed to install it on my machine:

First, I searched on google and found Microsoft's documentation, which you can access here: [Enable NVIDIA CUDA on WSL](https://learn.microsoft.com/en-us/windows/ai/directml/gpu-cuda-in-wsl)

The firsts steps envolve ensuring you have a WSL instance running with a glibc-based distribution, such as Ubuntu or Debian.

> Just a side note: By default, when you install the CUDA drivers on a windows machine, they also include a fully supported driver for WSL2. Therefore, running precompiled CUDA applications shouldn't be a problem. However, if you need to compile a CUDA application targeting a Linux or WSL2 backend, you must follow these steps to install the latest CUDA Toolkit for x86 Linux.

Now, let's get started.

## Get started with NVIDIA CUDA

Updated instructions can be found in the [NVIDIA CUDA on WSL User Guide](https://docs.nvidia.com/cuda/wsl-user-guide/index.html), but I will summarize the steps in this article.

## Step 1 - Check for WSL updates

Open a PowerShell instance and run the following command:

```shell
wsl.exe --update
```
This ensures that you have the latest WSL kernel available.

## Step 2 - Remove the old GPG Key

```shell
sudo apt-key del 7fa2af80
```

## Step 3 - Install the Linux x86 CUDA Toolkit Using WSL-Ubuntu Package

Detailed instructions can be found at [CUDA Toolkit 12.8 Update 1](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local). However, for convenience, I will replicated them here. I still recommend checking the URL above to ensure you're using the latest available instructions.


## Step 4 - Download and Organize the Files

First, download the base installer:
```shell
$ wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
```

Move it to the correct location:
```shell
$ sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
```

Next, download the `.deb` package:
```shell
$ wget https://developer.download.nvidia.com/compute/cuda/12.8.1/local_installers/cuda-repo-wsl-ubuntu-12-8-local_12.8.1-1_amd64.deb
```

## Step 5 - Install the `.deb` Package and Copy the Key

Use `dpkg -i` to install the `.deb` package:
```shell
$ sudo dpkg -i cuda-repo-wsl-ubuntu-12-8-local_12.8.1-1_amd64.deb
```

Copy the generated key (which will be prompted in your shell—pay attention!) and replace `*` in the following command:
```
$ sudo cp /var/cuda-repo-wsl-ubuntu-12-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
```

## Step 6 - Run `apt update` and Install CUDA

Now, lets run  `apt-get update` to reload package information and ensure we have the lastest versions:

```shell
$ sudo apt-get update
```

Finally, install the CUDA Toolkit:
```shell
$ sudo sudo apt-get -y install cuda-toolkit-12-8
```

Additional installation options are detailed [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/#meta-packages) 

That's it! You're all set.




    


