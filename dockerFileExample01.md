1.
```

FROM Ubuntu

VOLUME ["Volume01","Volume02"]

CMD echo "-----end-----"

CMD /bin/bash

```

2.
```docker build -f [dockerfileName] -t [Image Repo Name] .```

3. Dockerfile 命令
```FROM```: 基础镜像

```MAINTAINER```：谁来维护， name + Email

```RUN```: 镜像构建的时候需要运行的命令

```ADD```: 将文件加入镜像

```WORKDIR```:镜像工作目录

```VOLUME```：设置挂在卷

```EXPOSE```:指定暴露端口

```CMD```：容器启动的时候需要运行的命令，只有最后一个会生效，可被替代. 一行只能有一个命令，但可以有多行

```ENTRYPOINT```:容器启动的时候需要运行的命令， 可以追加命令

```ONBUILD```:The ONBUILD instruction adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build. The trigger will be executed in the context of the downstream build, as if it had been inserted immediately after the FROM instruction in the downstream Dockerfile.

```COPY```:将文件拷贝到镜像，不会自动解压

```ENV```：镜像构建的时候设置环境变量

4. Dockerfile
```
FROM ubuntu:18.04

MAINTAINER ZAC<test@test.com>

ENV MYPATH /usr/local

WORKDIR $MYPATH

RUN apt-get update

RUN apt-get install -y vim

RUN apt-get install -y net-tools

EXPOSE 80

CMD echo $MYPATH

CMD /bin/bash

```

```docker build -f Dockerfile -t testubuntu2:0.1 .```

