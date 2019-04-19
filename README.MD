# Docker

## 前言

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

## 1. 如何使用docker / How to use docker

下面内容都是在MAC OS环境下完成，Window用户可以 查看

### 1. 安装 / install

#### Mac OS

docker for Mac 支持 使用 brew 进行安装 你可以执行 

```shell
    brew cask install docker
```

在载入 Docker app 后，点击 Next，可能会询问你的 macOS 登陆密码，你输入即可。之后会弹出一个 Docker 运行的提示窗口，状态栏上也有有个小鲸鱼的图标。

#### Windows

Windows 环境可以 [点击这里](http://www.runoob.com/docker/windows-docker-install.html)

### 2. 如何使用docker / how to use docker

#### 1. 创建docker镜像 / create docker image

你可以创建自己的docker镜像，也可以通过 docker hub 找到自己需要的镜像， dockerHub 与 github 很相似，如果你使用github 那么你可以很容易的上手dockerhub

这里我们用创建docker镜像为例：

##### 1. 创建 Dockerfile / create Dockerfile

```shell
    touch Dockerfile
```

```docker
    # Base image to use, this nust be set as the first line
    FROM node

    # Maintainer: docker_user <docker_user at email.com> (@docker_user)
    MAINTAINER xxxxx@email.com

    # COPY 将本地项目文件拷贝到容器的某个目录下
    COPY . /app

    # WORKDIR 工作目录
    WORKDIR /app

    # VOLUME 文件映射 这里主要是通过宿主机（本地主机）与 容器内的某文件进行映射 达到在主机进行文件配置
    VOLUME /app/config

    # EXPOSE 映射端口
    EXPOSE 7101:7101/tcpP

    # ENTRYPOINT 执行某条命令 ENTRYPOINT 和 CMD 只能有一个 并执行最后一条  你也可以尝试使用 RUN
    ENTRYPOINT bash build.sh dev
```

更多 Dockerfile 配置可以到 [docker docs](https://docs.docker.com/v17.09/engine/reference/builder/) 查看

##### 2. create image

```shell
    # docker build -t <docker image name>
    docker build -t zmh6774517/aelf-block-api
```

##### 3. check image

你可以通过该命令查看你刚刚创建的docker镜像

```shell
    docker images
```

##### 4. docker run

```shell
    docker run -p 7101:7101 -v /Users/zhouminghui/WorkStudy/aelf-block-api/config/config.js:/app/config/config.js zmh6774517/aelf-block-api
```

##### 5. 将docker镜像推送到dockerHub上 / push docker image

请注意 这里的tag必须是你注册的docker账号名 否则会出现权限错误

```shell
    docker push zmh6774517/aelf-block-api
```

## 参考文献

[docker docs](https://docs.docker.com/)
[docker 菜鸟教程](http://www.runoob.com/docker/docker-tutorial.html)