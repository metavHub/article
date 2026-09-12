This is a guide to installing Stable Diffusion Forge locally, with an eye on how you'll actually use it after the install is done. It's written for people who want to get Forge running first and pick up the background knowledge later.

## What Stable Diffusion Forge is

Stable Diffusion is an AI system for generating images locally, and Forge is one of the tools built to run it. There are several such tools out there, and what sets Stable Diffusion Forge (hereafter Forge) apart is that it's light and fast.

The terminology around Stable Diffusion can get confusing, so here's how the pieces fit together:

- **Stable Diffusion**: the image generation mechanism itself (the model). It's released for free, but on its own it's unusable without programming knowledge.
- **WebUI**: software that puts Stable Diffusion in the browser, so you drive it through buttons, input fields, and other UI elements.
- **AUTOMATIC1111**: the most widely used of those WebUIs. The developer's account name became the name of the software.
- **Stable Diffusion Forge**: built on AUTOMATIC1111 above, with the processing made lighter and faster so it runs on machines with less VRAM.

How much faster it gets depends on your GPU, and the key point is that the less VRAM you have, the bigger the gain. The official figures put it at a 30–45% speedup on 8GB of VRAM. On high-end GPUs it's only a few percent, so there's not much difference.

In other words, it's a strong option when you want to run Stable Diffusion on a GPU that isn't high-end. Development on AUTOMATIC1111, the base it was built from, has largely stalled, so if you're starting now, Forge is the practical choice.

## System requirements (Windows)

- **OS**: Windows 10 / 11 (64-bit)
- **GPU**: NVIDIA. 8GB of VRAM or more recommended (4–6GB will run, but what you can do is limited)
  - Note: the RTX 50 series requires a different procedure and is out of scope for this article.
- **Memory**: 16GB or more
- **Storage**: 100GB or more of free space recommended

**A note on storage**: the program itself is around 10GB, but the "models" that generate the images are 2–7GB each, and they pile up as you use Forge. It's better to account for that and lay out your directory structure at install time. (See "Creating the directories" below for specifics.)

## Required software

Forge can't be installed or run on its own — it needs two other programs.

### What is Python?

Both Stable Diffusion and Forge are programs written in a language called Python. Python is the foundation that runs them, and without it installed on your system, Forge — being written in Python — won't run either. (Python is also the language generally used for building AI programs.)

The thing to watch out for is that newer isn't automatically better. Forge is built on the assumption of the 3.10 series, so 3.11 or 3.12 will error out partway through the install. Match the version.

### What is Git?

Git was originally a platform for collaborating on projects such as application development — managing and sharing work and its history across multiple people to keep development running smoothly — but it's also used to distribute finished programs and projects to the public.

Programs are uploaded to and shared from an area on GitHub's servers called a "repository." People working on a project pull the program from that repository down to their local machine, update or add to it, and push it back to the repository, and that's how the collaboration proceeds.

Here, you need it to clone (download) Forge's program from its repository on GitHub to your local machine.

**About installing Python and Git**: the zip package in "Installation method 1" already includes Python and Git, so if you install Forge from the zip, installing them beforehand isn't strictly required. But you do need them if you install from the repository via "Installation method 2," and with an eye toward how you'll use things going forward, this guide assumes you're installing Python and Git.

## Creating the directories

### Creating directories for AI programs and data, with later use in mind

Before installing, set up the install location and directory structure first. With future use in mind, the rest of the install assumes a layout like the following.

### Example directory layout

```
D:\AI
│
├─ apps
│   ├─ webui-forge
│   ├─ kohya_ss
│   └─ comfyui
│
├─ models
│   ├─ checkpoints
│   ├─ Lora
│   ├─ VAE
│   ├─ embeddings
│   └─ controlnet
│
├─ dataset
│   ├─ train
│   └─ raw
│
├─ output
│   ├─ images
│   └─ training
│
└─ tools
```

### The idea behind the layout

The point is to keep AI programs like Stable Diffusion and kohya_ss together under a single directory (`apps`), and to keep model data and output data in separate directories of their own. That way you can share model data across multiple AI apps to save space, avoid having output data accumulate inside the app, and keep backups and management manageable. Model data in particular tends to be large, so making it shareable across multiple AI apps is worth doing just for efficient storage use.

Note: for now, just create the directories roughly as shown. Actually pointing Forge at them comes after Forge is installed.

## Checking for the required software

### Checking what's already installed

You install the prerequisites before installing Forge, but in some cases they may already be on your machine. If you're not sure, check as follows.

**Checking whether Python is installed**

Open a terminal (Command Prompt) and enter:

```
python --version
```

Output:

```
Python 3.10.x
```

If a version like this appears, Python is installed. If not, install it.

**Checking whether Python 3.10 is installed**

Even if Python is already installed, it won't work if the version doesn't match, so if you know Python is there but aren't sure which version, check it.

In a terminal (Command Prompt), enter:

```
py --list
```

The installed versions are listed. If 3.10.x isn't installed, install it.

**Checking whether Git is installed**

Open a terminal (Command Prompt) and enter:

```
git --version
```

Output:

```
git version 2.41.0.windows.1
```

If the installed Git version is displayed like this, it's already installed. If the Git version isn't displayed, install it.

Note: any Git version that runs on your computer is fine.

## 1. Installing Python

The version to install is Python 3.10.x, and 3.10.6–3.10.9 seem to be the stable range.

- Here, the example uses 3.10.9 — stable, and as recent as possible within that range.
- Forge's Git repository documentation recommends 3.10.6, so that works too.

### Python 3.10.9 download page

In the "Files" section toward the bottom of the page, download the build that matches your environment.

Note: since we're installing on a Windows PC here, choose "Windows installer (64-bit)."

**1. Launching the installer**

Double-click the downloaded .exe file to launch the installer.

Note: save the .exe anywhere you like and launch it from there.

**2. Installing**

Check the required boxes and start the install with "Install Now."

Checkbox: ☑ Add Python to PATH — this adds the path to Python to your environment variables. If you install and manage multiple Python versions, you can leave it unchecked.

When the completion message appears, close the window to finish.

**3. Verifying the install**

In a terminal (Command Prompt), enter:

```
python --version
```

Output:

```
Python 3.10.9
```

If the Python version is displayed like this, the install succeeded.

## 2. Installing Git

For Git, any version that works should be fine.

### Git download page

**1. Launching the installer**

Double-click the downloaded .exe file to launch the installer.

Note: save the .exe anywhere you like and launch it from there.

**2. Installing**

Follow the steps from "Next."

There are more steps than the Python install, but you're basically clicking "Next" the whole way through.

Once "Next" turns into "Install," the installation begins.

When the completion message appears, close the window to finish.

**3. Verifying the install**

In a terminal (Command Prompt), enter:

```
git --version
```

Output:

```
git version 2.41.0.windows.1
```

If the Git version is displayed, the install succeeded.

## 3. Installing stable-diffusion-webui-forge

With the groundwork — Git and Python — in place, it's time to install Stable Diffusion Forge itself. There are two methods.

First, go to the Git URL below.

### stable-diffusion-webui-forge download page

### Installation method 1: downloading and installing the zip file

Toward the bottom of the repository page, under the "Installing Forge" section:

Clicking the link downloads the zip file.

```
>>> Click Here to Download One-Click Package (CUDA 12.1 + Pytorch 2.3.1) <<<
```

Download it into `apps`, inside the AI app directory structure you prepared earlier.

**Extracting the downloaded file**

Extract and unpack:

```
webui_forge_cu121_torch231.7z
```

### Installation method 2: cloning the repository with Git

From the "Code" button on the repository page, copy the HTTPS link and use `git clone` to clone the repository into `apps`, inside the AI app directory structure you prepared earlier.

Note: copy the URL and clone.

Once it's installed, set it up with the steps below.

**1. Running the update**

In the extracted

```
webui_forge_cu121_torch231
```

folder, click

```
update.bat
```

to launch it. A prompt opens and the download proceeds, so wait a while. When it finishes successfully and the prompt ends with

```
... Press any key to continue
```

press Enter to finish (the terminal closes).

**2. Running Forge**

In the same `webui_forge_cu121_torch231` folder, double-click

```
run.bat
```

to launch it.

Note: `run.bat` is inside the installed folder.

If the Forge screen comes up in your browser, you've succeeded. Congratulations!

That's it for the installation. Next time, I'll cover the initial setup, including how to point Forge at the directories created above.
