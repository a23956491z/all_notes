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


check running container:
`docker ps`
check exists container:
`docker ps -a`
check downloaded images:
`docker images`

docker run -w /home/enip/zawarudo/codebase/backtesting-project -it python:3.8.7
1. start container:
Assign name and allocate pseudo-TTY
`docker run --name python_test -it python:3.8.7`
Directly into bash with run
(-rm automaically remove when exist)
`docker run --name ubuntu_bash --rm -i -t ubuntu bash`
Expose port
`docker run -p 8001:80 python:3.8.7 bash`

`docker run -p 81:8888 -w ~ -it with_jupyter python -m jupyterlab --allow-root --ip=0.0.0.0`
3. run bash:
`docker exec -it ubuntu_bash bash`