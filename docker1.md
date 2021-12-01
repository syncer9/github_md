## .md 미리보기 창
crtl + shift + v


## .md 미리보기 창
crtl + shift + v

<!-- Heading -->

## Container 실행(example)
- Docker image 리스트, 현재 실행중인 컨테이너 리스트 확인
* hi

# abc
## abc
### abc

<!-- Line -->
---

<!-- text attributes -->
This is the **bold** 
This is the *italic*
this is the ~~strikethrouth~~

---

<!-- Quote -->
> Don't forget to code youre dream.

---

<!-- Link -->
click [naver](http://naver.com)

---

<!-- Image -->
|feature|Description|
|--|--|
|aaaa|![image description](img/wm.png)|
|aaa|<img src="img/wm.png" width=200>


<!-- Table -->
|table|table|
|--:|:--|
|a|a|
|a|a|
|a|a|

---
<!-- Code -->
To print message in the console, user `console.log('your message')` and .....

---
<span style="color:yellow">To add a worker</span> to this swarm, run the following command:
<span style="color:red">To add a worker</span> to this swarm, run the following command:

---
```
console.log('your message')
```

```ts
console.log('your message')
```

---

---

# 컨테이너 포트 외부로 노출하기
- port-forwarding
- Container port를 외부로 노출시켜 외부 연결 허용

```
-p hostPort:ContainerPort
-p ContainerPort
-p
```

```
$ docker run -d --name web1 -p 80:80 nginx<span style="color:yellow">To add a worker</span> to this swarm, run the following command:
<span style="color:yellow">To add a worker</span> to this swarm, run the following command:

$ docker run -d --name web3 -P nginx
<span style="color:yellow">To add a worker</span> to this swarm, run the following command:
<span style="color:yellow">To add a worker</span> to this swarm, run the following command:
<span style="color:yellow">To add a worker</span> to this swarm, run the following command:

```

# user-defined bridge network 생성
```
$ docker network create --driver bridge \
--subnet 192.168.100.0/24 \
--gateway 192.168.100.254 \
mynet

$ docker network create --driver bridge --subnet 192.168.100.0/24 --gateway 192.168.100.254 mynet
9508565a22725724e500fc62f4a091e36d256e886ddcb42cd63713a1249b50e2

$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
31e28a22f632   bridge    bridge    local
6125daae4746   host      host      local
9508565a2272   mynet     bridge    local
f2234de08cff   none      null      local

$ docker inspect mynet
```

```
$ docker run -it --name c1 --net mynet --ip 192.168.100.100 busybox

/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
19: eth0@if20: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
    link/ether 02:42:c0:a8:64:64 brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.100/24 brd 192.168.100.255 scope global eth0
       valid_lft forever preferred_lft forever
```

# 컨테이너를 이용한 server & client 서비스운영
- wordpress, mysql 컨테이너 서비스 운영

![aaad](./img/wm.png)

## 예1) multi-tier 구성하기
### mysql + wp 연동

- wp network create
```
docker network create --driver=bridge wp-network
```
- mysql & wp create
```
docker run -d --name=wp_db --network wp-network \
-e MYSQL_ROOT_PASSWORD=password \
-e MYSQL_DATABASE=wp \
-v /home/wp_db:/var/lib/mysql \
mysql:5.7

docker run -d --name wp --network wp-network \
-e MYSQL_DB_PASSWORD=password \
-e MYSQL_DB_HOST=wp-db -p 8888:80 \
wordpress
```

- 생성확인(mysql 접속)
```
root@docker-ubuntu:~# docker exec -it wp_db bash
root@c9fcd439da92:/# mysql -u root -p 
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 22
Server version: 5.7.35 MySQL Community Server (GPL)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| wp                 |
+--------------------+
5 rows in set (0.01 sec)

mysql> 
```

## 예2) multi-tier 구성하기(문제풀이)
<!-- Image -->
||Description|
|--|--|
|Image|<img src="img/genid.png" width=400 height=200>
```
root@docker-ubuntu:~# cat genid.sh 
#!/bin/bash
mkdir -p /webdata
while true
do
        /usr/bin/rig | /usr/bin/boxes -d boy > /webdata/index.html
        sleep 5

done
```
```
root@docker-ubuntu:~# cat Dockerfile 
FROM ubuntu:18.04
RUN apt-get update ; apt-get -y install rig boxes
ADD genid.sh /bin/genid.sh
RUN chmod +x /bin/genid.sh
ENTRYPOINT ["/bin/genid.sh"]
```
```
# docker run -d --name=genid -v /webdata:/webdata genid
# docker run -d --name=nginx -v /webdata:/usr/share/nginx/html -p 8889:80 nginx
# curl 127.0.0.1:8889
root@docker-ubuntu:~# curl 127.0.0.1:8889
        .-"""-.
       / .===. \
       \/ 6 6 \/
       ( \___/ )
  _ooo__\_____/______
 /                   \
| Viola York          |
| 638 Kennel Ln       |
| Aurora, IL  60507   |
| (708) xxx-xxxx      |
 \_______________ooo_/
        |  |  |
        |_ | _|
        |  |  |
        |__|__|
        /-'Y'-\
       (__/ \__)
root@docker-ubuntu:~# 
root@docker-ubuntu:~# curl 127.0.0.1:8889
         .-"""-.
        / .===. \
        \/ 6 6 \/
        ( \___/ )
  __ooo__\_____/______
 /                    \
| Pasquale Workman     |
| 100 Freeland Ave     |
| Knoxville, TN  37901 |
| (615) xxx-xxxx       |
 \_______________ooo__/
        |  |  |
        |_ | _|
        |  |  |
        |__|__|
        /-'Y'-\
       (__/ \__)
root@docker-ubuntu:~# 
```



# docker-compose 로 컨테이너 실행
```
[Solved]ERROR: Version in "./docker-compose.yml" is unsupported

Try
$ docker-compose up -d

Problem
ERROR: Version in "./docker-compose.yml" is unsupported.

Cause
docker-compose v3 syntax is not supported by docker-compose until version 1.10.0.
You'll need to update docker-compose to a newer version to get rid of that error. Current version is 1.16.1

Solved
기존에 sudo apt로 설치하면 옛날버전이 설치되기 때문에 지운다.
$ sudo apt-get remove docker-compose
curl을 이용하여 최신버전으로 설치
$ curl -L https://github.com/docker/compose/releases/download/1.25.0-rc1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose 
권한주기
``$ chmod +x /usr/local/bin/docker-compose``
 

+) 관련 github (https://github.com/docker/compose/releases)
```

```
root@docker-ubuntu:/my_wordpress# cat docker-compose.yml 
version: "3.8"

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8890:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  wordpress_data: {}
```
```
# curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

# /usr/local/bin/docker-compose config

```

# Kubernetes(쿠버네티스)
- Kubernetes 계층구조
<!-- Table -->
|Layer|구분|종류|
|--|--|--|
|layer 6|Develoment Workflow|OpenShift, Cloud Foundary, Docker Cloud, Deis, Flynn....|
|layer 5|Orchestration/Scheduling Service Model|Kubernetes, Docker Swarm,Marathon/Mesos,Nomad,..|
|layer 4|Container Engine|Docker, Rocket, RunC(OCI), Osv, LXC, LXD|
|layer 3|Operating System|Ubuntu,RHEL,CoreOS, Unikernels|
|layer 2|virtual Infrastructure|vSphere, EC2, GCP, Azure, OpenStack|
|layer 1|Physical Infrastructure|Raw Computer, Network, Storage|



## * Kubectl command

- 리소스 리스트보기
```
$ kubectl api-resources
$ kubectl --help
$ kubectl logs --help
```
- node 정보보기
```
$ kubectl get nodes
$ kubectl get nodes -o wide
$ kubectl describe node mast.example.com
```
- pod 실행 및 보기
```
방법1 : kubectl run webserver --image=nginx:1.14 --port 80
방법2 : kubectl create -f webserver.yaml
```