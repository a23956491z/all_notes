## overview
using [`urre/wordpress-nginx-docker-compose`](https://github.com/urre/wordpress-nginx-docker-compose) repository

with Bedrock's Wrodpress stack & nginx

## Requirements
* docker
* mkcert

### OS
install on virtualbox with windows 10 host
using `ubuntu server 20.04.3 LTS` as operating system
virtual hardware:
* RAM : 3096 MB
* Processor : 1 vCPU (Intel i7-9750H @ 2.6GHz) with Execution Cap 100%

some useful tools I installed on ubuntu:
 * `SSH` to get remote access
 * `mosh` to make ssh connection more stable
 * `tmux` to have multiple sessions with detached functionality
 * `Fish` & `omf` to get better shell


### Install docker
from [docker official website](https://docs.docker.com/engine/install/ubuntu/)
1. remove old version
```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

2. install basic tool for add a new repository
```bash
$ sudo apt-get update

$  sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

3. add docker's GPG key
```bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

4. add `stable` repository
```bash
$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

5. install docker
```bash
$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

6. make this user is able to use docker

```bash
sudo groupadd docker
```

```bash
$ sudo usermod -aG docker $USER
```linux tail

```bash
$ newgrp docker
```

7. test docker
```bash
$ docker info
```

### Install mkcert

1. install `certutil`
```bash
$ sudo apt install libnss3-tools
```

2. install `homebrew`
```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

If you use bash for your shell *(default)*:
```bash
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
```

Or Fish for your shell:
```bash
set -U fish_user_paths /home/linuxbrew/.linuxbrew/bin $fish_user_paths
```

use homebrew to install `mkcert`
```bash
brew install mkcert
```

## Configuration

1. docker configuration
copy `.env.example` to `.env` 
```bash
$ cp .env.example .env
```

edit the `.env` file, for example
```bash
IP=134.O.O.O
APP_NAME=enip_blog
DOMAIN="blog.eniplab.com"
DB_HOST=mysql
DB_NAME=enip_blog
DB_ROOT_PASSWORD=OOO
DB_TABLE_PREFIX=wp_
```

2. WordPress 

