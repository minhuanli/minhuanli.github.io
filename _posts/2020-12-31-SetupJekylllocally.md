---
layout: post
title: Setup Jekyll
description: These github pages are built with Jekyll framework. This is a note about how to setup Ruby and Jekyll development env locally, through direct installation or docker.
tags: tech blog
---

Jekyll is a static site generator. It takes text written in your favorite markup language and uses layouts to create a static website. 
Most personal blogs held by Github pages are generated with this framework. For example, my blog is mainly based on Jekyll [Hyde](https://github.com/poole/hyde) theme, with some personal customizations to make myself happy. 
You can easily fork [this repo](https://github.com/minhuanli/minhuanli.github.io) and modify it to be your customized blog site.

Setting up Ruby and Jekyll development locally is not quite trivial for macOS system (it becomes nearly impossible for a Windows system, you can use the docker solution here). And the package management of Ruby is quite an annoying experience. 
So, after fixing all the bugs, i write this note to describe two recipes about how to setting up Jekyll locally, via direct installation or docker. There is a tradeoff between the two ways: direct installation is a little complex but faster, docker is quite easy but slow while compiling.

My system version is macOS Catalina 10.15.7

* This will become a table of contents (this text will be scrapped).
{:toc}

### Direct Installation via Homebrew and Bundler, on macOS

1. Prepare command line tools and `Homebrew`, you might have already done the two things:
    ```shell
   # Step0, make sure the command line tool is installed
   xcode-select --install

   # Step1: Install Homebrew
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
2. Install Ruby and Jekyll. macOS has its system default Ruby installed, which is usually out-of-date. 
   We have to install the newer one and set the new one as the default Ruby.
   ```shell
   # Step2: Install Ruby with Homebrew
   brew install ruby

   # Step3: Add the new ruby into PATH
   echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc
   ## If you're using Bash
   echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile

   ## Source the setting file .zshrc or .bash_profile, you should see
   >>> which ruby
   /usr/local/opt/ruby/bin/ruby

   # Step4: Install Jekyll
   gem install --user-install bundler jekyll

   # Step5: Add related variables into PATH
   # If you're using Zsh
   echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc
   # If you're using Bash
   echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile
   ## The above path might change on different computers, for example, is can be like
   echo 'export PATH="$HOME/.local/share/gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc

   ## Again, source the setting file .zshrc or .bash_profile
   ## Make sure `jekyll` is executable after source
   ## You can check the GEM PATH with following commands
   gem env
   ```
3. Change to your project root directory, install all needed gem packages via `bundler`
   ```shell
   # If you don't have a Gemfile in the folder, this will create one
   bundle init
   
   # Add necessary gem terms to the Gemfile
   bundle add webrick
   
   # If you have a `Gemfile` already, you can ignore the above two steps, just:
   bundle install
   ```
4. Then you can run the website locally:
   ```shell
   bundle exec jekyll serve
   ```

### Through docker

`docker` is a very powerful tool to setting up development environments. I suppose this method should also work for Windows user, but haven't verified it.
1. Make sure you have already installed and run docker on your computer, docker has well-written [documentations](https://docs.docker.com/get-docker/)
2. Pull images from official Jekyll hub
   ```shell
   docker pull jekyll/jekyll:pages
   ```
3. Compose following `docker-compose.yml` in the root directory of your site project. You should have a `Gemfile` here. This can be easily constructed through any text editor.
   ```shell
   jekyll:
        image: jekyll/jekyll:pages
        command: >
            sh -c "bundle install &&
                   bundle exec jekyll serve --watch --host 0.0.0.0"
        ports:
            - 4000:4000
        volumes:
            - .:/srv/jekyll
   ```
4. Run it, this process is slow (~15s) on my side
   ```shell
   docker-compose run
   ```

### References

1. <https://jekyllrb.com/docs/installation/macos/>
2. <http://archerwq.cn/2017/09/21/setup-jekyll-locally-with-docker/>