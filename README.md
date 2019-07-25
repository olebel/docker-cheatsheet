Docker Cheatsheet
===
Table of content
---
1. [Install](#1-install)
2. [First Containers](#2-first-containers)
3. [container commands](#3-container-commands)
4. [images commands](#4-images-commands)
5. [Dockerfile](#5-dockerfile)
100. [Links](#100-links)


## 1. Install

### 1.1 CentOS 7.x installation
[link](https://docs.docker.com/install/linux/docker-ce/centos/)
##### install
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl enable docker
sudo systemctl start docker
```
##### verify
```
sudo systemctl status docker
sudo docker info
sudo docker run hello-world
```
### 1.2 CentOS 7.6 with Vagrant/Virtualbox
```
cd centos-configured
vagrant up
vagrant ssh
```
### 1.3 Ubuntu 18.04 installation
[link](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
##### install
```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
##### verify
```
sudo systemctl status docker
sudo docker info
sudo docker run hello-world
```
## 2. First Containers
##### hello-world
```
docker run hello-world
```
##### centos
```
docker run -it centos
cat /etc/centos-release
du -sh / 2>/dev/null
```
##### ubuntu
```
docker run -it ubuntu
cat /etc/debian_version
cat /etc/issue
du -sh / 2>/dev/null
```
##### alpine
```
docker run -it alpine
cat /etc/alpine-release
cat /etc/issue
du -sh / 2>/dev/null
```
##### busybox
```
docker run -it busybox
du -sh /
```
## 3. Containers commands
### 3.1 List
```
# show running containers
docker ps
# show last container
docker ps -l
# show all containers ( including stopped )
docker ps -a
# show container sizes
docker ps -s
```
##### full container ID
```
[root@desktop-08ut1lq ~]# docker ps -lq --no-trunc
cb9defb0841671a779f1527e5e30aa6c8b03d9bad9a42e61875368a9de6ae5f7
[root@desktop-08ut1lq ~]# docker ps -l
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
cb9defb08416        busybox             "sh"                11 minutes ago      Exited (0) 11 minutes ago                       gracious_villani
```
### 3.2 Run
```
# run in interactive mode
docker run -it ubuntu
# run in background
docker run -d httpd
# detach: Ctrl^P, Ctrl^Q
# attach <cid>
docker attach fe8
# run interactive in background
docker run -itd ubuntu
# check running
docker ps
```
### 3.3 Stop
```
# try gracefully stop container (SIGTERM, 10s wait)
docker stop <cid>
# just kill
docker kill <cid>
```
### 3.4 Read Logs
```
# show logs
docker logs <cid>
# show last 5 lines
docker logs --tail 5 <cid>
# tail -f
docker logs --tail 5 --follow <cid>
```
##### httpd example
```
docker run -d -P httpd
docker port $(docker ps -lq)
-> 80/tcp -> 0.0.0.0:32768
# on another console generate load
while sleep 1; do curl localhost:32768; done
# on main console
docker logs --tail 1 --follow $(docker ps -lq)
```
### 3.5 Exec
```
# exec something in running container
docker exec -it <cid> '/bin/bash'
```
## 4. Images commands
```
# list
docker images
# download
docker pull
# delete
docker rm
```
## 5. Dockerfile
### 5.1 nslookup
##### v1
```
# create environment
cd /vagrant
touch Dockerfile
# edit ...
```
##### cat Dockerfile
```
FROM centos
RUN yum install -y bind-utils
```
##### build
```
# docker build -t tag, nslookup - image name
docker build -t nslookup .
```
##### v2
```
FROM centos
RUN yum install -y bind-utils
ENTRYPOINT ["nslookup"]
CMD ["google.com"]
```
### 5.2 Dockerfile basic instructions
`FROM` - define which container loaded on current step. Used to define starting build point
```
FROM centos
```
`RUN` - define command which run in container in current step. Used to record actions in container
```
RUN yum clean && yum update metadata && yum update
RUN wget https://artifactory.intranet/generic-windows/app.msi
```
`ENTRYPOINT` - define command that run during container starting
`CMD` - does the same.
`ENTRYPOINT` vs `CMD` diff: ENTRYPOINT not overrided during container run
```
ENTRYPOINT ["echo"]
CMD ["hello"]
```
`COPY` - copy files into docker containers, from context and other containers
```
COPY /app /opt
```

```
FROM ubuntu as 'builder'
RUN ...
...
COPY --from /opt/hello/hello /bin/hello
```

`ENV` - set container environment variable
```
FROM ubuntu
ENV PG_MAJOR 9.3
ENV PG_VERSION 9.3.4
...
```

`EXPOSE` - expose container networking ports
```
EXPOSE 80
EXPOSE 80/tcp
EXPOSE 80/udp
```
### 5.3 flask-hello example
https://pythonspot.com/flask-hello-world/
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```
commands:
```
docker run -it centos
# centos
yum install -y epel-release
yum install -y pip
pip install flask
```
### 5.4 multistage example
```c
int main () {
  puts("Hello, world!");
  return 0;
}
```
commands:
```
yum install gcc make
make hello
```

## 6 Docker volumes
```
docker volume create app_config
docker volume rm app_config
docker volume ls
docker volume inspect
```

```
# docker volume create app_config
# docker run -d -P -v app_config:/opt/config nginx

# mkdir /opt/nginx_config
# docker run -d -P -v /opt/nginx_config:/opt/config nginx
```
## 100. Links
**https://container.training/  - BiS**

** https://github.com/wsargent/docker-cheat-sheet - comprehensive cheat-sheet**

https://docs.docker.com/ - official documentation
ENTRYPOINT vs CMD: https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/
