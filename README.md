# Docker Study
[Docker Hub Repository](https://hub.docker.com/r/andy30sh/ubuntu)

## Ubuntu version tags
1. 23.10 (latest)
2. 22.10
3. 20.04
4. 18.04


## Basic configuration
sshd at port 22 enabled remote root login by password or authorized_key;

sudo, openssh;

shared volumes at /shared and /storage

root default password: passwd


## Package configuration
#### Editors
1. vim
2. nano

### Network tools
1. net-tools
2. wget
3. curl

### Version control
1. git
2. subversion

### Programming languages
1. C/C++
2. Java
3. Python, pip
3. Javascript (NodeJS), npm

## Command build images
1. docker build -t [image_id]:[tag] ./[dockfile_dir]/ --no-cache
```bash
e.g. docker build -t andy30sh/ubuntu:23.10 -t andy30sh/ubuntu:latest ./ubuntu23/ --no-cache
```

## Publish to Docker Hub
1. docker login

2. docker image push andy30sh/ubuntu:[tag]
```bash
e.g. docker image push --all-tags andy30sh/ubuntu
```

## <ins>Useful docker command</ins>

1. show container's volumes
```js 
docker inspect -f '{{.Mounts}}' [ContainerID]
```