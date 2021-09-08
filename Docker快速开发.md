拉取镜像：`docker image pull <IMAGE NAME>:<TAG>`

查看镜像：`docker image ls`

删除镜像：`docker image rm <IMAGE ID>`	只有删除所有该镜像上的容器才可以删除镜像

构建镜像：`docker image build -t <DOCKERHUB NAME>/<IMAGE NAME>:<TAG> .`





容器操作

创建：`docker container run <IMAGE NAME>`

列出启动的容器：`docker container ls`

列出所有的容器：`docker container ls -a`

列出启动的容器ID：`docker container ls -q`

容器的停止：`docker container stop <IMAGE NAME or IMAGE ID>`

容器的删除：`docker container rm <IMAGE NAME or IMAGE ID>`

批量删除/停止：`docker container stop/rm $(docker container ps -aq)`

