---
title: Coding Python in Linux Server
seo_title: Coding Python in Linux Server
summary: Configurate Python Env. in Linux. Connect to server with VSCode.
description:
slug: bg/config-py
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-07-28
lastmod:  2023-10-09 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - 
tags:
  - Linux
  - Server
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---
# Configurate Python Environment in Linux

If you are a machine learning learner, for example a PhD student, you may need to use a server to train your model. In this article, I will introduce how to connect to server with vscode and how to setup python environment in server.

---

## Part I: SSH server setup

Technically, you can use **any** software to connect to server. Consider the convenience for ML learner to code and debug, I recommend to use vscode to connect to server. It is easy to use and has a lot of useful extensions. (i.e. Remote SSH, Python Environments, etc.)

### Connect to server

To connect to server, you need to know the address and port of server. You also need to know the username and password of server, which is usually provided by the administrator of server.

To check the validity of the address and port, first try to connect to server in VSCode. Type in the top bar of vscode:
  
  ```vscode
  ssh username@address -p port_number
  ```
  then press `Enter`. If you can connect to server, you will be asked to input password. (Otherwise, you will get an error message.)

After that, you should be free to explore the files and folders in server.

### Setup ssh key to avoid password input

> It can be annoying to input password every time you connect to server. You can setup ssh key to avoid password input. The key concept is to copy your public key to server. Then server can recognize you without password.

1. Generate your ssh key in local machine. 

  Use `ssh-keygen` command in cmd to generate ssh key. The default path is `~/.ssh/id_rsa`. You can change the path if you want, just follow the instructions.

  The command will generate two files: `id_rsa` and `id_rsa.pub`. The former is your private key, which should be kept secret. The latter is your public key, which can be shared to others. We will upload the public key to server.

2. Copy the public key to server.

  a. Login in your server. Enter `/root/.ssh/` folder. If your server does not have `.ssh` folder, you can create one.

  ```bash
  ssh localhost # Login in your server
  ```
  
  b. Concatenate the content of `id_rsa.pub` to `authorized_keys` file:
  
  ```bash
  cat id_rsa.pub >> authorized_keys
  ```
  This command will append the content of `id_rsa.pub` to `authorized_keys` file. If `authorized_keys` does not exist, it will create a new file.

  c. Change the permission. First, enter `/root` folder. Then change the permission of `.ssh` folder and `authorized_keys` file.

  ```bash
  chmod 700 .ssh
  chmod 600 .ssh/authorized_keys
  ```

3. Setting in vscode

  Edit the file `~/.ssh/config` in vscode. (Or click the bottom left corner of vscode `Open a Remotew Window`. Then click the `Connect to Host`. Then click the `Configure SSH Hosts...` button. Then click the `~/.ssh/config` button.)

  Add the following content to the file.
  ```bash
  Host server_name
      HostName server_address
      User username
      Port port
      IdentityFile ~/.ssh/id_rsa # The path of private key, use the private key (not public key)
  ```

  Save the file. Then you should be able to connect to server without password.

---

## Part II: Python Environment Setup

In this article, I will use Virtualenv to manage python environment. It is a simple and easy-to-use tool. You can also use Anaconda to manage python environment.

### Install Virtualenv & Virtualenvwrapper

Use `pip install virtualenv` to install Virtualenv.

Use `pip install virtualenvwrapper` to install Virtualenvwrapper.

### Configurate Virtualenvwrapper

If you server is finely configured, you can should be able to directly use `mkvirtualenv env_name` to create a new environment.

#### Setup Virtualenvwrapper

If above command output `mkvirtualenv: command not found`, you need to setup Virtualenvwrapper.

1. Check the path of Virtualenvwrapper.

  Use `echo $VIRTUALENVWRAPPER_PYTHON` to check the path of Virtualenvwrapper. If it is empty, you need to set it.

2. Obtain the path of Virtualenvwrapper.

  Use `which virtualenvwrapper.sh` to obtain the path of Virtualenvwrapper. Usually, it is `/usr/local/bin/virtualenvwrapper.sh`.

3. Set the path of Virtualenvwrapper.

  Find the file `~/.bashrc`. You can use
  
  `vim ~/.bashrc` or `nano ~/.bashrc` to edit the file, here I use `vim`.

  (You can also use vscode to edit the file)
  
  Add the following content to the file. You can add it at the end of the file.

  > Enter the editor mode by pressing `i`. Then you can edit the file. After editing, press `Esc` to exit the editor mode. Then type `:wq` to save the file and exit.

  ```bash
  export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3 # The path of python3
  export WORKON_HOME=/usr/local/bin/virtualenv # Set the path of virtualenv, this is the path where the virtualenv will be created
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

Note that you can only create python version that you have installed. For example, if you want to install a virtual environment of python 3.7, you need to install python 3.7 first.

- Use `mkvirtualenv env_name` to create a new environment. 
- Use `mkvirtualenv -p python3 env_name` to create a new environment with python3.
- Use `mkvirtualenv -P /usr/bin/python3 env_name` to create a new environment with python3. The path of python3 is `/usr/bin/python3`. It will create an environment having the same python version as you provided.

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

---

## Setup New Environment for Experiment

### Create a new environment according to the requirements.txt

1. Enter the folder of the project.

2. Use `mkvirtualenv env_name` to create a new environment.

3. Use `workon env_name` to enter the environment.

4. Use `pip install -r requirements.txt` to install the packages in `requirements.txt`. This is usually provided by the project.

---

Reference:

[1] https://www.cnblogs.com/doublexi/p/15783355.html

[2] https://blog.csdn.net/qq_42571592/article/details/122902266
 

