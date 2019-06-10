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
| 数据卷管理               | `docker volume COMMAND`                                                                                  |
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

