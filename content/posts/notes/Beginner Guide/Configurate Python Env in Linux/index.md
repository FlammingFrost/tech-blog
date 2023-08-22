---
title: Configurate Python Env in Linux
seo_title: Config Pyenv in Linux
summary: Configurate Python Env in Linux. Using Virtualenv.
description:
slug: bg/config-py
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-07-28
lastmod:  # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - 
tags:
  - Linux
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

## SSH server setup

### Connect to server

> This part is specific for server of Department of Statistics, SUSTech. It could be different for other servers.

Using vscode to connect to server is recommended.

1. Install Remote SSH extension in vscode. It is usually installed by automatically when you first time connect to server.

2. Open vscode, press `F1` and type `Remote-SSH: Connect to Host...`. Then type `ssh username@server_address` to connect to server. In SUStech, use `ssh root@address -p port` to connect to server. The address and port should be provided by the administrator of server.

3. After connected to server, you can use vscode as a local editor. You can also use terminal in vscode to run commands in server.

   Try to enter one of the folder to check if you have successfully connected to server. You can use GUI provided by vscode to check the files in server. Or you can use `ls` command to check the files in terminal.

### Setup ssh key to avoid password input

> If you don't set up ssh key, you need to input password every time you connect to server. It is annoying.

1. Generate ssh key in local machine. 

  Use `ssh-keygen` command to generate ssh key. The default path is `~/.ssh/id_rsa`. You can change the path if you want.

2. Copy the public key to server.

  In local machine, use `ssh-copy-id username@server_address` to copy the public key to server. You need to input password of server. After that, you can connect to server without password.

  For example, in SUSTech, use `ssh-copy-id root@address -p port` to copy the public key to server.

  > If you want to connect to server with different username, you need to generate ssh key for each username.

3. Setting in vscode

  Enter `~/.ssh/config` in vscode. Add the following content to the file.

  ```bash
  Host server_name
      HostName server_address
      User username
      Port port
      IdentityFile ~/.ssh/id_rsa # The path of private key
  ```

  Save the file. Then you should be able to connect to server without password.

## Python environment setup

In this article, I will use Virtualenv to manage python environment. It is a simple and easy-to-use tool. You can also use Anaconda to manage python environment.

### Install Virtualenv & Virtualenvwrapper

Use `pip install virtualenv` to install Virtualenv.

Use `pip install virtualenvwrapper` to install Virtualenvwrapper.

### Configurate Virtualenvwrapper

#### If you server is finely configured

You can directly use `mkvirtualenv env_name` to create a new environment.

#### Setup Virtualenvwrapper

If above command output `mkvirtualenv: command not found`, you need to setup Virtualenvwrapper.

1. Check the path of Virtualenvwrapper.

  Use `echo $VIRTUALENVWRAPPER_PYTHON` to check the path of Virtualenvwrapper. If it is empty, you need to set it.

2. Obtain the path of Virtualenvwrapper.

  Use `which virtualenvwrapper.sh` to obtain the path of Virtualenvwrapper. Usually, it is `/usr/local/bin/virtualenvwrapper.sh`.

3. Set the path of Virtualenvwrapper.

  Enter `~/.bashrc` in vscode. 
  
  `vim ~/.bashrc` or `nano ~/.bashrc`, here I use `vim` to edit the file.
  
  Add the following content to the file. You can add it at the end of the file.

  > Enter the editor mode by pressing `i`. Then you can edit the file. After editing, press `Esc` to exit the editor mode. Then type `:wq` to save the file and exit.

  ```bash
  export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3 # The path of python3
  export WORKON_HOME=/usr/local/bin/virtualenv # Set the path of virtualenv
  source /usr/local/bin/virtualenvwrapper.sh # The path of virtualenvwrapper, which is obtained in step 2
  ```

4.Run `source ~/.bashrc` to make the changes take effect.

  You can used
  
  ```bash
  echo $VIRTUALENVWRAPPER_PYTHON
  echo $VIRTUALENVWRAPPER_VIRTUALENV
  ```
  
  to check if the path is set correctly. If the path is set correctly, you can use `mkvirtualenv env_name` to create a new environment.

### Manage python environment

#### Create a new environment

- Use `mkvirtualenv env_name` to create a new environment. 
- Use `mkvirtualenv -p python3 env_name` to create a new environment with python3.
- Use `mkvirtualenv -P /usr/bin/python3 env_name` to create a new environment with python3. The path of python3 is `/usr/bin/python3`.

#### Enter an environment

- Use `workon env_name` to enter an environment.
- Use `source `/.virtualenvs/env_name/bin/activate` to enter an environment.
- In vscode, you can use the GUI provided by Virtualenvwrapper to enter an environment.

  - Install Python Environments extension in vscode (intall on server).
  - Click the bottom left corner of vscode. Then you can see the GUI provided by Virtualenvwrapper. Click the environment you want to enter.

#### Exit an environment

- Use `deactivate` to exit an environment.
- Click the bottom left corner of vscode. Then you can see the GUI provided by Virtualenvwrapper. Click the `deactivate` button.

#### Delete an environment

- Use `rmvirtualenv env_name` to delete an environment.

#### List all environments

- Use `lsvirtualenv` to list all environments.

## Setup A Python Environment for a git project

### Create a new environment

1. Enter the folder of the project.

2. Use `mkvirtualenv env_name` to create a new environment.

3. Use `workon env_name` to enter the environment.

4. Use `pip install -r requirements.txt` to install the packages in `requirements.txt`. This is usually provided by the project.


 

