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

# IMAGE
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
`docker build Dockerfile -t acoount_NAME/image_NAME`

push image to docker hub
`docker push account_NAME/image_NAME`


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

