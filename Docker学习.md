## 1	Docker的安装和介绍

### 1.1	介绍



适合人群

- 软件开发工程师
- 运维工程师
- DevOps 工程师



必备基础知识

- 最好熟悉一门编程语言
- 最好熟悉最基本的 Linux 命令



### 1.2	容器技术的介绍

注意：我们这里所说的容器 container 是指的一种技术，而 Docker 只是一个容器技术的实现，或者说让容器技术普及开来的最成功的实现。



#### 1.2.1	容器正在引领基础架构的一场新的革命

- 90年代的 PC
- 00年代的虚拟化
- 10年代的 cloud
- 11年代的 container



#### 1.2.2	什么是container(容器)？

容器是一种快速的打包技术

Package software into Standardized Units for Development, Shipment and Deployment

- 标准化
- 轻量级
- 易移植

Linux Container 容器技术的诞生（2008年）就解决了 IT 世界里“集装箱运输”的问题。Linux Container（简称LXC）它是一种内核轻量级的操作系统层虚拟化技术。Linux Container 主要由 Namespace 和 Cgroup 两大机制来保证实现：

- Namespace 命名空间主要用于资源的隔离。
- Cgroup 就负责资源管理控制作用，比如进程组使用 CPU/MEM 的限制，进程组的优先级控制，进程组的挂起和恢复等等。

![](D:\计算机\docker\全面的Docker系统性入门+进阶实践\container intro.PNG)



#### 1.2.3	容器的快速发展和普及

到2020年，全球超过50%的公司将在生产环境中使用container——Gartner



### 1.3	容器的标准化

`docker != container`

在2015年，由Google，Docker、红帽等厂商联合发起了OCI（Open Container Initiative）组织，致力于容器技术的标准化。



#### 1.3.1	容器运行时标准（runtime spec）

简单来讲就是规定了容器的基本操作规范，比如如何下载镜像，创建容器，启动容器等。



#### 1.3.2	容器镜像标准（image spec）

主要定义镜像的基本格式。



#### 1.3.3	容器是关乎“速度”

- 容器会加速你的软件开发
- 容器会加速你的程序编译和构建
- 容器会加速你的测试
- 容器会加速你的部署
- 容器会加速你的更新
- 容器会加速你的故障恢复



## 2	Docker 快速上手



### 2.1	Docker CLI 命令行介绍

#### 2.1.1	Docker Version

Windows (Intel芯片)

```shell
$ docker version
Client: Docker Engine - Community
Cloud integration: 1.0.12
Version:           20.10.5
API version:       1.41
Go version:        go1.13.15
Git commit:        55c4c88
Built:             Tue Mar  2 20:14:53 2021
OS/Arch:           windows/amd64
Context:           default
Experimental:      true

Server: Docker Engine - Community
Engine:
Version:          20.10.5
API version:      1.41 (minimum version 1.12)
Go version:       go1.13.15
Git commit:       363e9a8
Built:            Tue Mar  2 20:15:47 2021
OS/Arch:          linux/amd64
Experimental:     false
containerd:
Version:          1.4.4
GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
runc:
Version:          1.0.0-rc93
GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
docker-init:
Version:          0.19.0
GitCommit:        de40ad0
```

Linux（Intel芯片）

```shell
￥ docker version
Client: Docker Engine - Community
Version:           20.10.0
API version:       1.41
Go version:        go1.13.15
Git commit:        7287ab3
Built:             Tue Dec  8 18:59:40 2020
OS/Arch:           linux/amd64
Context:           default
Experimental:      true

Server: Docker Engine - Community
Engine:
Version:          20.10.0
API version:      1.41 (minimum version 1.12)
Go version:       go1.13.15
Git commit:       eeddea2
Built:            Tue Dec  8 18:57:45 2020
OS/Arch:          linux/amd64
Experimental:     false
containerd:
Version:          1.4.3
GitCommit:        269548fa27e0089a8b8278fc4fc781d7f65a939b
runc:
Version:          1.0.0-rc92
GitCommit:        ff819c7e9184c13b7c2607fe6c30ae19403a7aff
docker-init:
Version:          0.19.0
GitCommit:        de40ad0
```

Mac （Intel芯片）

```shell
$ docker version
Client: Docker Engine - Community
Cloud integration: 1.0.9
Version: 20.10.5
API version: 1.41
Go version: go1.13.15
Git commit: 55c4c88
Built: Tue Mar 2 20:13:00 2021
OS/Arch: darwin/amd64
Context: default
Experimental: true

Server: Docker Engine - Community
Engine:
Version: 20.10.5
API version: 1.41 (minimum version 1.12)
Go version: go1.13.15
Git commit: 363e9a8
Built: Tue Mar 2 20:15:47 2021
OS/Arch: linux/amd64
Experimental: false
containerd:
Version: 1.4.3
GitCommit: 269548fa27e0089a8b8278fc4fc781d7f65a939b
runc:
Version: 1.0.0-rc92
GitCommit: ff819c7e9184c13b7c2607fe6c30ae19403a7aff
docker-init:
Version: 0.19.0
GitCommit: de40ad0
```



#### 2.1.2	docker命令行的基本使用

docker + 管理的对象（比如容器，镜像） + 具体操作（比如创建，启动，停止，删除）

例如

- `docker image pull nginx` 拉取一个叫nginx的docker image镜像
- `docker container stop web` 停止一个叫web的docker container容器



### 2.2	认识一下docker命令行

```shell
$ docker version

Client: Docker Engine - Community
 Version:           20.10.8
 API version:       1.41
 Go version:        go1.16.6
 Git commit:        3967b7d
 Built:             Fri Jul 30 19:53:39 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.8
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.6
  Git commit:       75249d8
  Built:            Fri Jul 30 19:52:00 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.9
  GitCommit:        e25210fe30a0a703442421b0f60afac609f950a3
 runc:
  Version:          1.0.1
  GitCommit:        v1.0.1-0-g4144b63
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```



```shell
$ docker info

Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Build with BuildKit (Docker Inc., v0.6.1-docker)
  scan: Docker Scan (Docker Inc., v0.8.0)

Server:
 Containers: 4
  Running: 1
  Paused: 0
  Stopped: 3
 Images: 7
 Server Version: 20.10.8
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: false
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: e25210fe30a0a703442421b0f60afac609f950a3
 runc version: v1.0.1-0-g4144b63
 init version: de40ad0
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 5.10.23-5.al8.x86_64
 Operating System: Alibaba Cloud Linux 3 (Soaring Falcon)
 OSType: linux
 Architecture: x86_64
 CPUs: 1
 Total Memory: 1.927GiB
 Name: iZuf6fz2pl3xxj0hfnnc66Z
 ID: JVZJ:OI7D:EFZI:N2X4:KQHQ:FERL:NCCM:TNYT:4EYE:2NNT:HY4P:EP4C
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Registry Mirrors:
  https://iqxy9eov.mirror.aliyuncs.com/
 Live Restore Enabled: false
```



```shell
$ docker

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/root/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker
                           context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/root/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/root/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/root/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  app*        Docker App (Docker Inc., v0.9.1-beta3)
  builder     Manage builds
  buildx*     Build with BuildKit (Docker Inc., v0.6.1-docker)
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  scan*       Docker Scan (Docker Inc., v0.8.0)
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.

To get more help with docker, check out our guides at https://docs.docker.com/go/guides/
```



```shell
$ docker container --help

Usage:  docker container COMMAND

Manage containers

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Run a command in a new container
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker container COMMAND --help' for more information on a command.
```



### 2.3	镜像和容器（image vs container）

#### 2.3.1	image镜像

- Docker image 是一个 `read-only` 文件

- 这个文件包含文件系统，源码，库文件，依赖，工具等一些运行application所需要的文件
- 可以理解成一个模板
- docker image具有**分层**的概念



#### 2.3.2	container容器

- “一个运行中的docker image”
- 实质是复制image并在image最上层加上一层 `read-write` 的层（称之为 `container layer`，容器层）
- 基于同一个image可以创建多个 container



![container](D:\计算机\docker\全面的Docker系统性入门+进阶实践\container.PNG)



#### 2.3.3	docker image的获取

- 自己制作
- 从registry拉取（比如docker hub）



### 2.4	创建第一个容器

| 操作                 | 命令（全）                         | 命令（简）                           |
| -------------------- | ---------------------------------- | ------------------------------------ |
| 容器的创建           | docker container run <image name>  | docker run <image name>              |
| 容器的列出(up)       | docker container ls                | docker ps                            |
| 容器的列出(up和exit) | docker container ls -a             | docker ps ls -a                      |
| 容器的停止           | docker container stop <name or ID> | docker stop <contrainer name or  ID> |
| 容器的删除           | docker container rm <name or  ID>  | docker rm <container name or ID>     |



### 2.5	命令行小技巧之批量操作

#### 2.5.1	批量停止

```shell
$ docker container ps

CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
cd3a825fedeb   nginx     "/docker-entrypoint.…"   7 seconds ago    Up 6 seconds    80/tcp    mystifying_leakey
269494fe89fa   nginx     "/docker-entrypoint.…"   9 seconds ago    Up 8 seconds    80/tcp    funny_gauss
34b68af9deef   nginx     "/docker-entrypoint.…"   12 seconds ago   Up 10 seconds   80/tcp    interesting_mahavira
7513949674fc   nginx     "/docker-entrypoint.…"   13 seconds ago   Up 12 seconds   80/tcp    kind_nobel
```

##### 方法1

```shell
$ docker container stop cd3 269 34b 751
```

##### 方法2

```shell
$ docker container stop $(docker container ps -q)cd3a825fedeb269494fe89fa34b68af9deef7513949674fc$ docker container ps -aCONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                     PORTS     NAMEScd3a825fedeb   nginx     "/docker-entrypoint.…"   30 seconds ago   Exited (0) 2 seconds ago             mystifying_leakey269494fe89fa   nginx     "/docker-entrypoint.…"   32 seconds ago   Exited (0) 2 seconds ago             funny_gauss34b68af9deef   nginx     "/docker-entrypoint.…"   35 seconds ago   Exited (0) 2 seconds ago             interesting_mahavira7513949674fc   nginx     "/docker-entrypoint.…"   36 seconds ago   Exited (0) 2 seconds ago             kind_nobel
```



#### 2.5.2	批量删除

和批量停止类似，可以使用 `docker container rm $(docker container ps -aq)`



### 2.6	容器的attached和detached模式

#### 2.6.1	前台进入容器

```shell
$ docker run -p 80:80 nginx
```

在命令行中会打印出日志信息，ctrl+c 退出后，windows系统不会退出容器，但linux会。



#### 2.6.2	后台进入容器

```shell
$ docker run -d -p 80:80 nginx
```

在命令行中不会打印出日志信息。



#### 2.6.3	由后台进入前台

```shell
$ docker attach <container name or ID>
```



### 2.7	容器的交互式模式

#### 2.7.1	获取容器日志

```shell
$ docker container logs <container name or ID>
```



#### 2.7.2	动态获取容器日志

```shell
$ docker container logs -f <container name or ID>
```



#### 2.7.3	创建一个容器并进入交互式模式

```shell
$ docker container run -it
```



#### 2.7.4	在一个已经运行的容器里执行一个额外的command

```shell
$ docker container exec -it# 在此情况下退出容器交互模式后，容器并不会停止
```



### 2.8	容器和虚拟机（Container vs VM）

![](D:\计算机\docker\全面的Docker系统性入门+进阶实践\container and VM.PNG)



#### 2.8.1	容器不是Mini虚拟机

- 容器其实是进程Containers are just processes
- 容器中的进程被限制了对CPU内存等资源的访问
- 当进程停止后，容器就推出了



#### 2.8.2	容器的进程process

```shell
$ docker container run -d nginx57fe4033dd7e1e620a0b6a7b83b85d4f8f98772f0ce585624c384de254826fd0$ docker container lsCONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES57fe4033dd7e   nginx     "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   80/tcp	festive_proskuriakova$ docker container top 57fUID                 PID                 PPID                C                   STIME               TTY                 TIME                CMDroot                7646                7625                0                   12:14               ?                   00:00:00            nginx: master process nginx -g daemon off;systemd+            7718                7646                0                   12:14               ?                   00:00:00            nginx: worker process
```



### 2.9	docker container run背后发生了什么？

- 1. 在本地查找是否有nginx这个image镜像，但是没有发现
- 2. 去远程的image registry查找nginx镜像（默认的registry是Docker Hub)
- 3. 下载最新版本的nginx镜像 （nginx:latest 默认)
- 4. 基于nginx镜像来创建一个新的容器，并且准备运行
- 5. docker engine分配给这个容器一个虚拟IP地址
- 6. 在宿主机上打开80端口并把容器的80端口转发到宿主机上
- 7. 启动容器，运行指定的命令（这里是一个shell脚本去启动nginx）



## 3	镜像的创建管理和发布

### 3.1	镜像的获取

- pull from `registry` (online) 从 registry 拉取
  - public (公有)
  - private (私有)
- build from `Dockerfile` (online) 从 Dockerfile 构建
- load from `file` (offline) 文件导入 (离线)



![get image](D:\计算机\docker\全面的Docker系统性入门+进阶实践\get image.PNG)



### 3.2	镜像的基本操作

#### 3.2.1	镜像的拉取Pull Image

默认从Docker Hub拉取，如果不指定版本，会拉取最新版

```shell
$ docker pull nginx

Using default tag: latest
latest: Pulling from library/nginx
69692152171a: Pull complete
49f7d34d62c1: Pull complete
5f97dc5d71ab: Pull complete
cfcd0711b93a: Pull complete
be6172d7651b: Pull complete
de9813870342: Pull complete
Digest: sha256:df13abe416e37eb3db4722840dd479b00ba193ac6606e7902331dcea50f4f1f2
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```



指定版本

```shell
$ docker pull nginx:1.20.0

1.20.0: Pulling from library/nginx
69692152171a: Already exists
965615a5cec8: Pull complete
b141b026b9ce: Pull complete
8d70dc384fb3: Pull complete
525e372d6dee: Pull complete
Digest: sha256:ea4560b87ff03479670d15df426f7d02e30cb6340dcd3004cdfc048d6a1d54b4
Status: Downloaded newer image for nginx:1.20.0
docker.io/library/nginx:1.20.0
```



#### 3.2.2	镜像的查看

```shell
$ docker image ls

REPOSITORY              TAG       IMAGE ID       CREATED       SIZE
quay.io/bitnami/nginx   latest    0922eabe1625   6 hours ago   89.3MB
nginx                   1.20.0    7ab27dbbfbdf   10 days ago   133MB
nginx                   latest    f0b8a9a54136   10 days ago   133MB
```



#### 3.2.3	镜像的删除

只有运行在该镜像上的容器都删除了之后才可以删除镜像

```shell
$ docker image rm 0922eabe1625

Untagged: quay.io/bitnami/nginx:latest
Untagged: quay.io/bitnami/nginx@sha256:d143befa04e503472603190da62db157383797d281fb04e6a72c85b48e0b3239
Deleted: sha256:0922eabe16250e2f4711146e31b7aac0e547f52daa6cf01c9d00cf64d49c68c8
Deleted: sha256:5eee4ed0f6b242e2c6e4f4066c7aca26bf9b3b021b511b56a0dadd52610606bd
Deleted: sha256:472a75325eda417558f9100ff8b4a97f4a5e8586a14eb9c8fc12f944b26a21f8
Deleted: sha256:cdcb5872f8a64a0b5839711fcd2a87ba05795e5bf6a70ba9510b8066cdd25e76
Deleted: sha256:e0f1b7345a521469bbeb7ec53ef98227bd38c87efa19855c5ba0db0ac25c8e83
Deleted: sha256:11b9c2261cfc687fba8d300b83434854cc01e91a2f8b1c21dadd937e59290c99
Deleted: sha256:4819311ec2867ad82d017253500be1148fc335ad13b6c1eb6875154da582fcf2
Deleted: sha256:784480add553b8e8d5ee1bbd229ed8be92099e5fb61009ed7398b93d5705a560
Deleted: sha256:e0c520d1a43832d5d2b1028e3f57047f9d9f71078c0187f4bb05e6a6a572993d
Deleted: sha256:94d5b1d6c9e31de42ce58b8ce51eb6fb5292ec889a6d95763ad2905330b92762
Deleted: sha256:95deba55c490bbb8de44551d3e6a89704758c93ba8503a593cb7c07dfbae0058
Deleted: sha256:1ad1d903ef1def850cd44e2010b46542196e5f91e53317dbdb2c1eedfc2d770c
```



### 3.3	Dockerfile介绍

- Dockerfile是用于构建docker镜像的文件
- Dockerfile里包含了构建镜像所需的“指令”
- Dockerfile有其特定的语法规则



#### 举例：执行一个Python程序

容器及进程，所以镜像就是一个运行这个进程所需要的环境。

加入我们要在一台ubuntu21.04上运行下面这个hello.py的Python程序

hello.py的文件内容：

```python
print("hello docker")
```

第一步，准备Python环境

```shell
apt-get update && \
DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y python3.9 python3-pip python3.9-dev
```

第二步，运行hello.py

```shell
[root@user ~]# hello.py
hello docker
```



#### 一个Dockerfile的基本结构

Dockerfile

```dockerfile
FROM ubuntu:21.04
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y python3.9 python3-pip python3.9-dev
ADD hello.py /
CMD ["python3", "/hello.py"]
```



### 3.4	镜像的构建和分享

#### 3.4.1	构建

```shell
docker image build -t <DockerHub name>/<image name>:<tag> .
```



#### 3.4.2	分享

```shell
[root@user ~]# docker login[root@user ~]# docker image push <image name>:<tag>
```



### 3.5	通过commit创建镜像

```shell
[root@user ~]# docker container commit <container ID> <image name>
```



### 3.6	关于 scratch 镜像

Scratch 是一个空的Docker镜像。

通过 scratch 来构建一个基础镜像。

```c
#include <stdio.h>int main(){    printf("hello docker\n");}
```

编译成一个二进制文件

```shell
[root@user ~]# gcc --static -o hello hello.c[root@user ~]# ./hellohello docker
```



```dockerfile
FROM scratchADD hello /CMD ["/hello"]
```

构建

```shell
[root@user ~]# docker build -t hello .[root@user ~]# docker image lsREPOSITORY   TAG       IMAGE ID       CREATED          SIZEhello        latest    2936e77a9daa   40 minutes ago   872kB
```

运行

```shell
[root@user ~]# docker container run -it hellohello docker
```



## 4	Dockerfile完全指南

### 4.1	基础镜像的选择

#### 4.1.1	基本原则

- 官方镜像优于非官方的镜像，如果没有官方镜像，则尽量选择Dockerfile开源的
- 固定版本tag而不是每次都使用lastest
- 尽量选择体积小的镜像



#### 4.1.2	Build一个Nginx镜像

假设我们有一个 `index.html` 文件

```html
<h1>Hello Docker</h1>
```

准备一个Dockerfile

```dockerfile
FROM nginx:1.21.0-alpine
ADD index.html /usr/share/nginx/html/index.html
```



### 4.2	通过RUN执行指令

`run` 主要用于在Image里执行指令，比如安装软件，下载文件等。

```shell
$ apt-get update
$ apt-get install wget
$ wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz
$ tar zxf ipinfo_2.0.1_linux_amd64.tar.gz
$ mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo
$ rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```



#### 4.2.1	Dockerfile

```dockerfile
FROM ubuntu:21.04
RUN apt-get update
RUN apt-get install -y wget
RUN wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz
RUN tar zxf ipinfo_2.0.1_linux_amd64.tar.gz
RUN mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo
RUN rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```

每一行的RUN命令都会产生一层image layer，导致镜像的臃肿。



#### 4.2.2	改进版Dockerfile

```dockerfile
FROM ubuntu:21.04
RUN apt-get update && \
	apt-get install -y wget && \
	wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz && \
	tar zxf ipinfo_2.0.1_linux_amd64.tar.gz && \
	mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo && \
	rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```



### 4.3	文件复制和目录操作

往镜像里复制文件有两种方式，`copy` 和 `add` ，我们来看一下两者的不同。



#### 4.3.1	复制普通文件

`COPY` 和 `ADD` 都可以把 local 的一个文件复制到镜像里，如果目标目录不在，则会自动创建

```dockerfile
FROM python:3.9.5-alpine3.13
COPY hello.py /app/hello.py
```

比如把本地的 hello.py 复制到 /app 目录下。/app 这个 folder 不存在，则会自动创建



#### 4.3.2	复制压缩文件

`ADD` 比 COPY 高级一点的地方就是，如果复制的是一个 gzip 等压缩文件时，ADD 会帮助我们自动去解压缩文件。

```dockerfile
FROM python:3.9.5-alpine3.13
ADD hello.tar.gz /app/
```



### 4.4	构建参数和环境变量（ARG vs ENV）

`ARG` 和 `ENV` 是经常容易被混淆的两个 Dockerfile 的语法，都可以用来设置一个“变量”。但实际上两者有很多的不同。

```dockerfile
FROM ubuntu:21.04
RUN apt-get update && \
	apt-get install -y wget && \
	wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz && \
	tar zxf ipinfo_2.0.1_linux_amd64.tar.gz && \
	mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo && \
	rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```



#### 4.4.1	ENV

```dockerfile
FROM ubuntu:21.04ENV VERSION=2.0.1RUN apt-get update && \	apt-get install -y wget && \	wget https://github.com/ipinfo/cli/releases/download/ipinfo-${VERSION}/ipinfo_${VERSION}_linux_amd64.tar.gz && \	tar zxf ipinfo_2.0.1_linux_amd64.tar.gz && \	mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo && \	rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```



#### 4.4.2	ARG

```dockerfile
FROM ubuntu:21.04ARG VERSION=2.0.1RUN apt-get update && \	apt-get install -y wget && \	wget https://github.com/ipinfo/cli/releases/download/ipinfo-${VERSION}/ipinfo_${VERSION}_linux_amd64.tar.gz && \	tar zxf ipinfo_${VERSION}_linux_amd64.tar.gz && \	mv ipinfo_${VERSION}_linux_amd64 /usr/bin/ipinfo && \	rm -rf ipinfo_${VERSION}_linux_amd64.tar.gz
```



使用ARG创建变量时，变量仅存在于镜像的构建时候，在我们创建容器的时候无法使用变量。

使用ENV创建变量时，变量会作为环境变量永久地保存在镜像里面。



修改变量

```shell
docker image build -f .\Dockerfile-arg -t ipinfo-arg-2.0.0 --build-arg VERSION=2.0.0 .
```



### 4.5	CMD容器启动命令

CMD 可以用来设置容器启动时默认会执行的命令。

- 容器启动时默认执行的命令。
- 如果 docker container run 启动容器时指定了其它命令，则 CMD 命令会被忽略。

- 如果定义了多个 CMD，只有最后一个会被执行。

```dockerfile
FROM ubuntu:21.04ENV VERSION=2.0.1RUN apt-get update && \	apt-get install -y wget && \	wget https://github.com/ipinfo/cli/releases/download/ipinfo-${VERSION}/ipinfo_${VERSION}_linux_amd64.tar.gz && \	tar zxf ipinfo_${VERSION}_linux_amd64.tar.gz && \	mv ipinfo_${VERSION}_linux_amd64 /usr/bin/ipinfo && \	rm -rf ipinfo_${VERSION}_linux_amd64.tar.gz
```



删除已经退出的容器

```shell
docker system prune -f
```

容器执行完毕后，自动删除容器

```shell
docker container run --rm -it ipinfo ipinfo 8.8.8.8
```



### 4.6	容器启动命令ENTRYPOINT

ENTRYPOINT 也可以设置容器启动时要执行的命令，但是和 CMD 是有区别的。

- CMD 设置的命令，可以在 docker container run 时传入其它命令，覆盖掉 CMD 的命令，但是 ENTRYPOINT 所设置的命令是一定会被执行的。
- ENTRYPOINT 和 CMD 可以联合使用，ENTRYPOINT 设置执行的命令，CMD 传递参数。

```dockerfile
FROM ubuntu:21.04CMD ["echo", "hello docker"]
```

把上面的 Dockerfile build 成一个叫 `demo-cmd` 的镜像

```shell
$ docker image lsREPOSITORY        TAG       IMAGE ID       CREATED      SIZEdemo-cmd          latest    5bb63bb9b365   8 days ago   74.1MB
```

```dockerfile
FROM ubuntu:21.04ENTRYPOINT ["echo", "hello docker"]
```

build 成一个叫 `demo-entrypoint` 的镜像

```shell
$ docker image lsREPOSITORY        TAG       IMAGE ID       CREATED      SIZEdemo-entrypoint   latest    b1693a62d67a   8 days ago   74.1MB
```

CMD的镜像，如果执行创建容器，不指定运行时的命令，则会默认执行 CMD 所定义的命令，打印出 hello docker

```shell
$ docker container run -it --rm demo-cmdhello docker
```

但是如果我们 docker container run 的时候指定命令，则该命令会覆盖掉 CMD 的命令，如：

```shell
$ docker container run -it --rm demo-cmd echo "hello world"hello world
```

但是 ENTRYPOINT 的容器里 ENTRYPOINT 所定义的命令则无法覆盖，一定会执行

```shell
$ docker container run -it --rm demo-entrypointhello docker$ docker container run -it --rm demo-entrypoint echo "hello world"hello docker echo hello world
```





### 4.7	Shell格式和Exec格式

CMD 和 ENTRYPOINT 同时支持 shell 格式和 Exec 格式。

#### 4.7.1	Shell 格式

```shell
CMD echo "hello docker"
```

```shell
ENTRYPOINT echo "hello docker"
```



#### 4.7.2	Exec格式

可以执行命令的方式

```shell
ENTRYPOINT ["echo", "hello docker"]
```

```shell
CMD ["echo", "hello docker"]
```

注意 shell 脚本的问题

```dockerfile
FROM ubuntu:21.04ENV NAME=dockerCMD echo "hello $NAME"
```

假如我们要把上面的 CMD 改成 Exec 格式，下面这样改是不行的。

```dockerfile
FROM ubuntu:21.04ENV NAME=dockerCMD ["echo", "hello $NAME"]
```

它会打印出 `hello $NAME` ，而不是 `hello docker` ，那么需要怎么写呢？我们需要以 shell 脚本的方式去执行

```dockerfile
FROM ubuntu:21.04ENV NAME=dockerCMD ["sh", "-c", "echo hello $NAME"]
```



### 4.8	构建一个Flask镜像

```dockerfile
FROM python:3.9.5-slimCOPY app.py /src/app.pyRUN pip install flaskWORKDIR /srcENV FLASK=app.pyEXPOSE 5000CMD ["flask", "run", "-h", "0.0.0.0"]
```

```shell
docker container run -d -p 5000:5000 flask-demo
```



### 4.9	合理使用内存

```dockerfile
FROM python:3.9.5-slimRUN pip install flaskWORKDIR /srcENV FLASK=app.py# 以上操作均可以使用CACHE执行COPY app.py /src/app.py	# 这步操作放在后面执行EXPOSE 5000CMD ["flask", "run", "-h", "0.0.0.0"]
```

对比：

```dockerfile
FROM python:3.9.5-slim# 如果这步不使用CACHE，那么后面都不会使用CACHE，内存开销大COPY app.py /src/app.pyRUN pip install flaskWORKDIR /srcENV FLASK=app.pyEXPOSE 5000CMD ["flask", "run", "-h", "0.0.0.0"]
```



### 4.10	dockerignore

使用 `.dockerignore` 文件

```dockerfile
.vscode/env/
```



### 4.11	镜像的多阶段构建

```c
#include <stdio.h>void main(int argc, char *argv[]){    printf("hello %s\n", argv[argc - 1]);}
```

以下镜像大小：1.4 GB

```dockerfile
FROM gcc:9.4COPY hello.c /src/hello.cWORKDIR /srcRUN gcc --static -o hello hello.cENTRYPOINT ["/src/hello"]CMD []
```



多阶段构建：

```dockerfile
FROM gcc:9.4 AS builderCOPY hello.c /src/hello.cWORKDIR /srcRUN gcc --static -o hello hello.cFROM alphine:3.13.5#将builder中/src/hello文件拷贝到alphine:3.13.5的/src/hello文件COPY --from=builder /src/hello /src/helloENTRYPOINT ["/src/hello"]CMD []
```



### 4.12	尽量使用非ROOT用户

使用非 root 用户来构建这个镜像

- 通过 groupadd 和 useradd 创建一个 flask 的组和用户
- 通过 USER 指定后面的命令要以 flask 这个用户的身份运行

```dockerfile
FROM python:3.9.5-slimRUN pip install flask && \	groupadd -r flask && useradd -r -g flask flask && \	mkdir /src && \	chown -R flask:flask /srcUSER flaskCOPY app.py /src/app.pyWORKDIR /srcENV FLASK=app.pyEXPOSE 5000CMD ["flask", "run", "-h", "0.0.0.0"]
```



## 5	Docker的存储

### 5.1	本章介绍

默认情况下，在运行中的容器里创建的文件，被保存在一个可写的容器层：

- 如果容器被删除了，则数据也没有了
- 这个可写的容器层是和特定的容器绑定的，也就是这些数据无法方便的和其它容器共享

Docker 主要提供了两种方式做数据的持久化

- Data Volume，由 Docker 管理，（/var/lib/docker/volumes/），持久化数据的最好方式
- Bind Mount，由用户指定存储的数据具体 mount 在系统什么位置



### 5.2	数据持久化之 Bind Mount

```dockerfile
VOLUME ["\data"]	# 可指定容器内的一个文件夹
```



查看本地磁盘的挂载

```shell
$ docker volume ls
```

查看 volume 的详细信息，可以看到在本地挂载数据的路径

```shell
$ docker volume inspect <VOLUME NAME>
```



在创建容器时指定 volume 

```shell
$ docker container run -d -v <volume name:容器内需要挂载的目录> <image name>
```



#### 5.2.1	创建容器（不指定 -v 参数）

此时 Docker 会自动创建一个随机名字的 volume，去存储我们在 Dockerfile 定义的 volume `VOLUME ["/app"]`，

**在不使用 -v 参数的时候，Dockerfile中的 `VOLUME ["/APP"]` 才是有效的。**

在这个 Volume 的 mountpoint 可以发现容器创建的文件，VOLUME NAME 是一个随机的字符串。



#### 5.2.2	创建容器（指定 -v 参数）

在创建容器的时候通过 `-v` 参数，我们可以手动的指定需要创建 Volume 的名字，以及对应于容器内的路径，这个路径是可以任意的，不必需要在 Dockerfile 里通过 VOLUME 定义。



### 5.3	Bind Mount 练习之 Docker 开发环境

```c
void main(int argc, char *argv[])
{
    printf("hello %s\n", argv[argc-1]);
}
```

```shell
$ docker container run -it -v <本地文件>:<容器文件> <IMAGE NAME:IMAGE TAG>
```

```shell
$ gcc -o hello hello.c
$ ./hello docker
```



### 5.4	多个机器之间的容器共享数据

![](D:\计算机\docker\全面的Docker系统性入门+进阶实践\docker save.PNG)

Docker 的 volume 支持多种 driver。默认创建的 volume driver 都是 local

```shell
$ docker volume inspect vscode
[
    {
        "CreatedAt": "2021-06-23T21:33:57Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/vscode/_data",
        "Name": "vscode",
        "Options": null,
        "Scope": "local"
    }
]
```

这一节我们看看一个叫 sshfs 的 driver，如何让 docker 使用不在同一台机器上的文件系统做 volume



#### 5.4.1	环境准备

准备三台 Linux 机器，之间可以通过 SSH 相互通信。

| hostname     | ip             | ssh username | ssh password |
| ------------ | -------------- | ------------ | ------------ |
| docker-host1 | 192.168.200.10 | vagrant      | vagrant      |
| docker-host2 | 192.168.200.11 | vagrant      | vagrant      |
| docker-host3 | 192.168.200.12 | vagrant      | vagrant      |



#### 5.4.2	安装 plugin

在其中两台机器上安装一个plugin `vieux/sshfs`

```shell
[vagrant@docker-host1 ~]$ docker plugin install --grant-all-permissions vieux/sshfslatest: Pulling from vieux/sshfsDigest: sha256:1d3c3e42c12138da5ef7873b97f7f32cf99fb6edde75fa4f0bcf9ed27785581152d435ada6a4: CompleteInstalled plugin vieux/sshfs
```

```shell
[vagrant@docker-host2 ~]$ docker plugin install --grant-all-permissions vieux/sshfslatest: Pulling from vieux/sshfsDigest: sha256:1d3c3e42c12138da5ef7873b97f7f32cf99fb6edde75fa4f0bcf9ed27785581152d435ada6a4: CompleteInstalled plugin vieux/sshfs
```



#### 5.4.3	创建 volume

```shell
[vagrant@docker-host1 ~]$ docker volume create --driver vieux/sshfs \                          -o sshcmd=vagrant@192.168.200.12:/home/vagrant \                          -o password=vagrant \                          sshvolume
```

查看

```shell
[vagrant@docker-host1 ~]$ docker volume lsDRIVER               VOLUME NAMEvieux/sshfs:latest   sshvolume[vagrant@docker-host1 ~]$ docker volume inspect sshvolume[    {        "CreatedAt": "0001-01-01T00:00:00Z",        "Driver": "vieux/sshfs:latest",        "Labels": {},        "Mountpoint": "/mnt/volumes/f59e848643f73d73a21b881486d55b33",        "Name": "sshvolume",        "Options": {            "password": "vagrant",            "sshcmd": "vagrant@192.168.200.12:/home/vagrant"        },        "Scope": "local"    }]
```



#### 5.4.4	创建容器挂载 Volume

创建容器，挂载 sshvolume 到 /app 目录，然后进入容器的 shell，在 /app 目录创建一个 test.txt 文件

```shell
[vagrant@docker-host1 ~]$ docker run -it -v sshvolume:/app busybox shUnable to find image 'busybox:latest' locallylatest: Pulling from library/busyboxb71f96345d44: Pull completeDigest: sha256:930490f97e5b921535c153e0e7110d251134cc4b72bbb8133c6a5065cc68580dStatus: Downloaded newer image for busybox:latest/ #/ # lsapp   bin   dev   etc   home  proc  root  sys   tmp   usr   var/ # cd /app/app # ls/app # echo "this is ssh volume"> test.txt/app # lstest.txt/app # more test.txtthis is ssh volume
```

这个文件我们可以在 docker-host3 上看到

```shell
[vagrant@docker-host3 ~]$ pwd/home/vagrant[vagrant@docker-host3 ~]$ lstest.txt[vagrant@docker-host3 ~]$ more test.txtthis is ssh volume
```

















































































