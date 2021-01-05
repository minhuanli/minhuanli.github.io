---
layout: post
title: Configure A macOS From Scratch
description: A walk-through note on how to configure my familiar working system from a brand new macOS system, including Git token, Homebrew, Terminal color theme, Oh-my-zsh plugins, miniconda and jupyter kernel.
tag: tech
---

The new macOS Big Sur has an impressively pretty UI, so today I tried to install it on my old 2015 macbook pro. This is not my primary working computer, as I am not sure if the Big Sur is stable enough and compatible with all my software. 
After the system installation, I reconfigured my favorite working environment from scratch. This is note could serve as a complete recipe when I (have enough money to) buy a new computer.

My system version is macOS 11.1, with Intel chip. 

* This will become a table of contents (this text will be scrapped).
{:toc}

### 1. Command Line Tools and Homebrew

On a brand new system, first install the basic command line tool and [Homebrew](https://brew.sh/) package manager. 

Run following codes in the Terminal, it should prompt an installation GUI to get you through, just follow their instructions.
```shell
xcode-select --install
```
> It is possible that you have installed command line tools before.
> If that is the case, you will see some words like "xcode-select: error: command line tools are already installed".
> It is totally Ok, just move to the Homebrew installation.

Then install Homebrew with:
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
After the installation, run `brew` in the Terminal, if you see some brew tutorial words as "Example usage...", you are ok with the step.
### 2. Set up Git config and Github HTTP token
Then set up Git config and Github token on the computer, you can interact (push and pull) with Github repos in a password-free manner. You should have a github account before this step, you can [register](https://github.com/) for free if you haven't.

Then config your github username and email in global parameters, s.t. Github serve will know who you are:
```shell
# Remove the quotation marks and replace the words inside with your account info
git config --global user.name "user-name"
git config --global user.email "user-email"
# Check all configs
git config --list
```
For a convenient password-free manner, you can use HTTP token (preferred) or SSH token:
```shell
# Set HTTP Token
# Change to Home Directory
cd ~
# Create a text file containing your username and password
touch .git-credentials
vim .git-credentials
# Input the following line into .git-credentials, no brackets 
https://{username}:{password}@github.com
# Add the file into git config with the following command 
# Then a "[credential] helper = store" line is in the .gitconfig
git config --global credential.helper store
```
I also list how to set SSH token here:
```shell
# Generate SSH Token, run the following codes with 2 following Enter
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# Test if SSH setting is Ok
ssh -T git@github.com
```
Then you can interact with Github in a password-free manner.
### 3. Install Oh-my-zsh, theme and useful plugins
This is my favorite part. I use `zsh` instead of `bash` as my local shell because `zsh` has pretty themes as well as powerful plugins, and `Oh-my-zsh` provides an elegant way to manager them. 
Here is how to install them. 

First, change your shell to `zsh`. macOS has `zsh` as its default shell, but you can check and change shell with the following codes:
```shell
# List all available shells
cat /etc/shells
# Check current shell
echo $SHELL
# Change shell to zsh
chsh -s /bin/zsh
```

#### 3.1 Easy-set plugins: `git`, `sublime`, `web-search`, `osx`, `vi-mode`

#### 3.2 Have-to-install plugins: `zsh-autosuggestions`, `zsh-syntax-highlighting`, `git-open`, `autojump`

### 4. Install Miniconda, set Jupyter kernel, and Julia

### References

- <https://brew.sh/>
- <https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github>