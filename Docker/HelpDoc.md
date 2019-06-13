# Docker

## 常用命令
>记录一些常用的命令

#### 查看版本信息
| 用途                       | 命令               |
| -------------------------- | ------------------ |
| 测试Docker版本以及安装信息 | `docker --version` |
| ^                          | `docker info`      |
| ^                          | `docker version`   |


#### 镜像相关
| 用途             | 命令                                                 |
| ---------------- | ---------------------------------------------------- |
| 从镜像库提取镜像 | `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`           |
| 列出镜像         | `docker images [OPTIONS] [REPOSITORY[:TAG]]`         |
| 管理镜像         | `docker image COMMAND`                               |
| 删除镜像         | `Usage:  docker image rm [OPTIONS] IMAGE [IMAGE...]` |



#### 容器相关
| 用途             | 命令                                                         |
| ---------------- | ------------------------------------------------------------ |
| 管理容器         | `docker container COMMAND`                                   |
| 列出容器         | `docker ps [OPTIONS]`                                        |
| ^                | `docker container ls [OPTIONS]`                              |
| 从镜像运行到容器 | `docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`    |
| 启动容器         | `docker container start [OPTIONS] CONTAINER [CONTAINER...]`  |
| 连接容器         | `docker container attach [OPTIONS] CONTAINER `               |
| ^                | `docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]` |
| 停止容器         | `docker container stop [OPTIONS] CONTAINER [CONTAINER...]`   |
| 终止容器         | `docker container kill [containIDs]`                         |
| 删除容器         | `docker container rm [OPTIONS] CONTAINER [CONTAINER...]`     |


### 数据管理相关           
| 用途                     | 命令                                                                                                       |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| 数据卷管理               | `docker volume COMMAND`                                                                                    |
| 创建数据卷               | `docker volume create [OPTIONS] [VOLUME]`                                                                  |
| 查看数据卷列表           | `docker volume ls [OPTIONS]`                                                                               |
| 查看数据卷信息           | `docker volume inspect [OPTIONS] VOLUME [VOLUME...]`                                                       |
| 启动一个挂载数据卷的容器 | `docker run --name 需要创建的容器名称 # -v 数据卷名称:容器目录 --mount source=数据卷名称,target=容器目录 ` |
| 删除数据卷               | `docker volume rm [OPTIONS] VOLUME [VOLUME...]`                                                            |
| 清理数据卷               | `docker volume prune [OPTIONS]`                                                                            |
* **挂载一个本地目录作为数据卷**
使用 `--mount` 标记可以指定挂载一个本地主机的目录到容器中去。

```bash
$ docker run -d -P \
    --name web \
    # liunx 使用
    # -v /src/webapp:/opt/webapp \
    # windows使用
    # -v //c/user/目录:/opt/webapp \
    --mount type=bind,source=/src/webapp,target=/opt/webapp \
    training/webapp \
    python app.py

```

上面的命令加载主机的 `/src/webapp` 目录到容器的 `/opt/webapp`目录。这个功能在进行测试的时候十分方便，比如用户可以放置一些程序到本地目录中，来查看容器是否正常工作。本地目录的路径必须是绝对路径，以前使用 `-v` 参数时如果本地目录不存在 Docker 会自动为你创建一个文件夹，现在使用 `--mount` 参数时如果本地目录不存在，Docker 会报错。

* **拷贝配置文件到镜像**
```
# liunx 使用
# -v /src/webapp:/opt/webapp:ro \
# windows使用
# -v //c/user/目录:/opt/webapp:ro \
```


###拷贝容器里的文件
| 用途                                    | 命令                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| 在容器和本地文件系统之间复制文件/文件夹 | `docker container cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH` |
| ^                                       | `docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH`         |

#### 使用 Dockerfile 定制镜像
Dockerfile 是一个文本文件，其内包含了一条条的 指令(Instruction)，每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建。

* **指令**

| 指令 | 用途                                                                                       | 命令以及参数                                                                                                           |
| ---- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| FROM | 导入依赖镜像                                                                               | `FROM 镜像名称`                                                                                                        |
| RUN  | 运行相关命令                                                                               | `shell` 格式 : `RUN <命令>` <br> `exec` 格式 : `RUN ["可执行文件/程序","参数1","参数2"]`                                                              |
| CMD  | CMD 指令的格式和 RUN 相似                                                                  | `shell` 格式 : `CMD <命令>` <br> `exec` 格式 : `CMD ["可执行文件/程序","参数1","参数2"]`                               |
|ENTRYPOINT |ENTRYPOINT 的目的和 CMD 一样，都是在指定容器启动程序及参数。ENTRYPOINT 在运行时也可以替代，不过比 CMD 要略显繁琐，需要通过 docker run 的参数 --entrypoint 来指定。|`shell` 格式 : `ENTRYPOINT <命令>` <br> `exec` 格式 : `ENTRYPOINT ["可执行文件/程序","参数1","参数2"]`|
| COPY | 复制文件                                                                                   | `COPY [--chown=<user>:<group>] <源路径>...<目标路径>` <br> `COPY [--chown=<user>:<group> ["<源路径1>,..."<目标路径>"]` |
| ADD  | ADD 指令和 COPY 的格式和性质基本一致。但是在 COPY 基础上增加了一些功能。可以解压内容到目录 | `ADD [--chown=<user>:<group>] <源路径>...<目标路径>` <br> `ADD [--chown=<user>:<group> ["<源路径1>,..."<目标路径>"]`   |
|ENV |设置环境变量|`ENV <key> <value>`<br>` ENV <key1>=<value1> <key2>=<value2>... `|
|ARG|构建参数|` ARG<参数名>[=<默认值>]`|
|VOLUME|定义匿名卷|`VOLUME ["<路径1>","<路径2>"...]`|
|EXPOSE |声明端口|` EXPOSE<端口1>[<端口2>...] `|