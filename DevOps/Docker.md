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