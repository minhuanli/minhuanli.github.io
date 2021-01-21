---
layout: post
title: Configure A macOS with Intel chip From Scratch
description: A walk-through note on how to configure my familiar working system from a brand new macOS system, including Git token, Homebrew, Terminal color theme, Oh-my-zsh plugins, miniconda and jupyter kernel.
tag: tech
---

The new macOS Big Sur has an impressively pretty UI, so today I tried to install it on my old 2015 macbook pro. This is not my primary working computer, as I am not sure if the Big Sur is stable enough and compatible with all my software. 
As I mostly work with the command line and text editors, after the system installation, I reconfigured my favorite working environment from scratch. This is note could serve as a complete recipe when I (have enough money to) buy a new computer.

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
### 2. Set up Git config and Github HTTP/SSH token
Then set up Git config and Github token on the computer, you can interact (push and pull) with Github repos in a password-free manner. You should have a github account before this step, you can [register](https://github.com/) for free if you haven't.

First Config your github username and email in global parameters, s.t. Github serve will know who you are:
```shell
# Remove the quotation marks and replace the words inside with your account info
git config --global user.name "user-name"
git config --global user.email "user-email"
```
Check all configs:
```shell
git config --list
```
For a convenient password-free manner, you can use HTTP token (preferred) or SSH token:<br>

<p class="orangebox">
<i class='ge'>Update on Jan 18, 2021:</i><br>
Github makes a safety update that requires all personal user to use a personal access token for command line git access. See <a href="https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/">ref</a>. Previous password access will be no longer supported after August 13, 2021. How to update can be found <a href="https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token">here</a> and <a href="https://docs.github.com/en/github/using-git/updating-credentials-from-the-macos-keychain">here</a>
</p>

- **Set HTTP Token**<br>
  Change to Home Directory
  ```shell
  cd ~
  ```
  Create a text file containing your username and password
  ```shell
  touch .git-credentials
  vim .git-credentials
  # Input the following line into .git-credentials, no brackets 
  https://{username}:{password}@github.com
  ```
  Add the file into git config with the following command
  ```shell
  git config --global credential.helper store
  ```
  Then a `[credential] helper = store` line is in the `.gitconfig`
-  **Set SSH token**<br>
  Generate SSH Token, run the following codes with 2 following `Enter`
  ```shell 
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```
  Test if SSH setting is Ok
  ```shell
  ssh -T git@github.com
  ```

With either one of the above 2 methods, you can interact with Github in a password-free manner.


### 3. Install Miniconda
As I am mostly working with `python`, I use miniconda to manage python packages and virtual envs. Check [here](https://medium.com/dunder-data/anaconda-is-bloated-set-up-a-lean-robust-data-science-environment-with-miniconda-and-conda-forge-b48e1ac11646) to see why I choose Miniconda over standard Anaconda. 

To install miniconda, you have to download the installer according to your system [here](https://docs.conda.io/en/latest/miniconda.html)

Then, change to the directory with the installer in Command line, run:
```shell
bash Miniconda3-latest-MacOSX-x86_64.sh
```

### 4. Install Oh-my-zsh, theme and useful plugins
This is my favorite part. I use `zsh` instead of `bash` as my local shell because `zsh` has pretty themes as well as powerful plugins, and `Oh-my-zsh` provides an elegant way to manager them. 
Here is how to install them. 
> I am looking for a way to make this oh-my-zsh work on Harvard's Odyssey cluster  

First, change your shell to `zsh`. macOS has `zsh` as its default shell, but you can check and change shell with the following codes:<br>
- List all available shells<br>
```shell
cat /etc/shells
```
- Check current shell<br>
```shell
echo $SHELL
```
- Change shell to zsh<br>
```shell
chsh -s /bin/zsh
```

Then, according to their [documentation](https://ohmyz.sh/#install), install `oh-my-zsh` with:
```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
There will be a `.zshrc` text file in your home directory. 
You can easily change words inside and `source ~/.zshrc` to make a new configuration happen.
I have uploaded my configuration files, theme (I modify the af-magic theme) and Terminal color scheme in this [repo](https://github.com/minhuanli/personal_env_setting). 
Here is how my prompt looks like:
<center><img src="/public/image/prompt_look_like.png" alt="prompt look like" width="500"/></center>

You can explore your favorite themes [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes). 
Another (or main) highlight of `oh-my-zsh` is its convenient management of abundant powerful plugins, which will make the working process much more productive and enjoyable.
I list my favourite plugins here, there are more than 200 plugins you can explore [here]((https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)) 
#### 4.1 Easy-set plugins: *git*, *sublime*, *web-search*, *osx*, *vi-mode*
Easy-set plugins are really "easy to set", you simply add the plugin name in to the `plugins` line in `~/.zshrc` and source the file, like:
```shell
plugins=(git sublime web-search osx vi-mode)
```
- [*git*](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git):<br>
  provide useful alias regarding git commands, like `gst = git status`
- [*sublime*](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/sublime)<br>
  open file by sublime text with `st "file-name"`, you should have sublime installed first.
- [*web-search*](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/web-search)<br>
  Enable you to search through many engines in command line, like `google "something"`
- [*osx*](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/osx)<br>
  An extremely useful tools with a few utilities in macOS. Like you can open the current directory in finder by `ofd`, let the spotify play a music with `spotify play`.
  
#### 4.2 Have-to-install plugins: *zsh-autosuggestions*, *zsh-syntax-highlighting*, *autojump*
These plugins are not included in a standard `oh-my-zsh` distribution, but you can still easily install them by one more line
- [*zsh-autosuggestions*](https://github.com/zsh-users/zsh-autosuggestions)<br>
  A very useful tool to suggest commands as you type based on history and completions.<br> 
  You can install by:<br>
  clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`)
  ```shell
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  ```
  add the plugin name into `~/.zshrc` and source the file
  ```shell
  plugins=(... zsh-autosuggestions)
  ```
- [*zsh-syntax-highlighting*](https://github.com/zsh-users/zsh-syntax-highlighting)<br>
  This package provides syntax highlighting for the shell zsh. It enables highlighting of commands whilst they are typed at a zsh prompt into an interactive terminal. This helps in reviewing commands before running them, particularly in catching syntax errors.<br>
  You can install by:<br>
  clone this repository in oh-my-zsh's plugins directory:
  ```shell
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```
  add the plugin name into `~/.zshrc` and source the file
  ```shell
  plugins=(... zsh-syntax-highlighting)
  ```
- [autojump](https://github.com/wting/autojump)<br>
  autojump is a faster way to navigate your filesystem. It works by maintaining a database of the directories you use the most from the command line.
  You can install by:<br>
  install *autojump* by Homebrew
  ```shell
  brew install autojump
  ```
  add the plugin name into `~/.zshrc` and source the file
  ```shell
  plugins=(... autojump)
  ```

**References**
- <https://brew.sh/>
- <https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github>
- <https://ohmyz.sh/>
- <https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html>