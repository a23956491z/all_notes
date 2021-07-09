# install
remove old version:
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

install:
```bash
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
	
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```


verify:
```
$ sudo docker run hello-world

$ sudo docker run docker/whalesay cowsay hello-world!
```

# basic 
## RUN
`docker run `runs a image, if not exist it would download it

run with command
`docker run ubuntu sleep 5`

run container in background (detach):
`docker run -d IMAGE`

attach cotainer in background:
`docker attach ID/NAME`

execute command in container
`docker exec ID/NAME COMMAND` 
## PS
check running container:
`docker ps`
check exists container:
`docker ps -a`

check downloaded images:
`docker images`

## stop/remove
stop running container:
`docker stop ID\NAME`
remove container:
`docker rm ID\NAME`
remove  image :
`docker rmi IMAGE`

download image and not run:
`docker pull IMAGE`

remove with image name:
```bash
docker rm $(docker ps -a -f ancestor=mikebirdgeneau/jupyterlab -q)
```
# More Run
## TAG
tag(specific version)
default tag is *latest*
run with image and its tag
`docker run IMAGE:TAG`

## STDIN
provide input to container
`docker run -i IMAGE`

iterative container(with input and output)
`docker run -it IMAGE`

Assign name and allocate pseudo-TTY
`docker run --name python_test -it python:3.8.7`
## PORT
![](https://i.imgur.com/AuAjo9b.png)
every container has it's ip
mapping container ip:port to host ip:port

Expose port
`docker run -p 8001:80 python:3.8.7 bash`

`docker run -p 81:8888 -w ~ -it with_jupyter python -m jupyterlab --allow-root --ip=0.0.0.0`

## VOLUME
![](https://i.imgur.com/kfSmsqk.png)

mount host directory to container
`docker run -v /opt/datadir:/var/lib/mysql mysql`


## LOG
`docker logs ID/NAME`

# ENV variable 
![](https://i.imgur.com/f4CUfFC.png)

# IMAGE / Dockerfile
dockerfile: automatically make a image
```dockerfile
FROM Ubuntu
RUN apt-get update
RUN apt-get install python

RUN pip install flask
RUN pip install flask-mysql

COPY . /opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```

build image with dockerfile
`docker build Dockerfile -t acoount_NAME/image`

push image to docker hub
`docker push account_NAME/image_NAME`

## Dockerfile command
* FROM
* RUN
* COPY
* ENTRYPOINT
* CMD
* ENV

## CMD
run a "full" command
```dockerfile
CMD bash
CMD ["sleep","5"]
```

## ENTRYPOINT
only give a start of a command
need fill argument by user
```dockerfile
FROM Ubuntu

ENTRYPOINT ["sleep"]
```

we can use like this:
`docker run ubuntu-sleeper 10`
which means `docker run ubuntu-sleeper sleep 10`

provide a default argument
```dockerfile
FROM Ubuntu

ENTRYPOINT ["sleep"]

CMD ["5"]
```

we can even assign entrypoint at run
`docker run --entrypoint sleep2.0 ubuntu-sleeper 10`

# Network
![](https://i.imgur.com/OrcoRul.png)

default network use bridge(NAT)
`docker run ubuntu --network=none;host`

user-defined network
```bash
docker network create\
	--driver bridge \
	--subnet 182.18.0.0/16
	custom-isolated-network
```
```bash
docker network ls
```
```bash
docker inspect ID/NAME 
```

---

# Storage

## docker file architeture
* `/var/lib/docker` docker directory
	* volumes 


## layered architecture
docker **reuse the same layer**
![](https://i.imgur.com/1eyyHbY.png)

so if we updated our source code only, we can do fast deploy
![](https://i.imgur.com/l9FFse7.png)


the layers created in building are read only
when we run a container we have a container layer
all container build from same image, use the **same container layer**
![](https://i.imgur.com/LIIZIAm.png)

if we modify "read only" file,
docker make a copy to container layer
this is COPY-ON_WRITE mechanism
mechanism
## volumes : persistent storage
### volume mount
![](https://i.imgur.com/LeHkyxJ.png)

if we don't have such volume when running, docker create one

### bind mount
assign volume which is not from default folder:
`docker run -v /data/mysql:/var/lib/mysql mysql`
![](https://i.imgur.com/cMo2WuQ.png)

same meaning, but better:
```bash
docker run\
	--mount type=bind, source=/data/mysql, target=/var/lib/mysql\
	mysql
```

## Storage driver
different OS use differnt default storage drvier
* AUFS : like Ubuntu
* ZFS
* BTRFS
* Device Mapper

---
# Compose

---
# Registry

---

1. start container:

Directly into bash with run
(-rm automaically remove when exist)
`docker run --name ubuntu_bash --rm -i -t ubuntu bash`

3. run bash:
`docker exec -it ubuntu_bash bash`


# using
run jupyterlab and assign port
`docker run -p 8001:8888 mikebirdgeneau/jupyterlab`

with volume mapping
`docker run -v /home/enip/zawarudo/codebase/deep-learning-research:/opt/app/data -p 8001:8888 mikebirdgeneau/jupyterlab`

with automatically remove after exit
`docker run --rm -v /home/enip/zawarudo/codebase/deep-learning-research:/opt/app/data -p 8001:8888 mikebirdgeneau/jupyterlab`



# permission denied
```bash
sudo groupadd docker
```

```bash
$ sudo usermod -aG docker $USER
```

```bash
$ newgrp docker
```

```bash
$ docker info
```
