### 1 Docker简介

Docker是用golang开发的一个开源项目

> 作用：
>
> 1. docker能够运行在windows、linux、MacOS上面，因此用docker开发的项目可移植性高
> 2. 每个docker项目都是独立的虚拟环境，类似虚拟机，但是占用的资源比虚拟机少很多
> 3. 每开启一个docker都需要一个基础镜像



### 2 Docker安装

推荐使用官网提供的方法进行docker的安装：https://www.docker.com/

#### 2.1 linux安装docker

1. 进入官网：https://www.docker.com/
2. 选择”Developers"，再选择“Documentation"
3. 选择”Manuals“
4. 选择”Docker Engine“，再选择”install"，再选择对应的linux系统版本，
5. 安装说明书的步骤进行安装即可



### 3 Docker常见命令

先介绍一些docker的简单使用方法，以便能够快速入门docker，后续内容将会精进

#### 3.1 镜像操作

1. **搜索镜像**

**作用：**在Docker Hub上搜索与关键字匹配的镜像。

```bash
docker search <image_name>
```

示例：

```bash
# 示例
root@onlyubuntu:~# docker search nginx
NAME                               DESCRIPTION                                     STARS     OFFICIAL
nginx                              Official build of Nginx.                        19996     [OK]
unit                               Official build of NGINX Unit: Universal Web …   32        [OK]
nginx/nginx-ingress                NGINX and  NGINX Plus Ingress Controllers fo…   92        
nginxinc/nginx-unprivileged        Unprivileged NGINX Dockerfiles                  154       
nginx/nginx-prometheus-exporter    NGINX Prometheus Exporter for NGINX and NGIN…   42        
nginx/unit                         This repository is retired, use the Docker o…   63        
nginxinc/nginx-s3-gateway          Authenticating and caching gateway based on …   6         
nginx/nginx-ingress-operator       NGINX Ingress Operator for NGINX and NGINX P…   2         
nginx/nginx-quic-qns               NGINX QUIC interop                              1         
nginxinc/amplify-agent             NGINX Amplify Agent docker repository           1         
nginxinc/ingress-demo              Ingress Demo                                    4         
nginxproxy/nginx-proxy             Automated nginx proxy for Docker containers …   140       
nginx/unit-preview                 Unit preview features                           0         
bitnami/nginx                      Bitnami container image for NGINX               192       
nginxproxy/acme-companion          Automated ACME SSL certificate generation fo…   134       
ubuntu/nginx                       Nginx, a high-performance reverse proxy & we…   114       
kasmweb/nginx                      An Nginx image based off nginx:alpine and in…   8         
nginxproxy/docker-gen              Generate files from docker container meta-da…   17        
nginxinc/ngx-rust-tool                                                             0         
bitnami/nginx-ingress-controller   Bitnami container image for NGINX Ingress Co…   34        
nginxinc/mra_python_base                                                           0         
bitnami/nginx-exporter             Bitnami container image for NGINX Exporter      5         
nginxinc/mra-fakes3                                                                0         
rancher/nginx                                                                      2
```

> 注意：
>
> - NAME：镜像的名称，拉取镜像时用于指定要拉取的镜像，完整的名称是：`<用户名/组织名>/<镜像名>`，如果是官方镜像，则通常省略用户名/组织名，直接使用镜像名。
> - DESCRIPTION：镜像的简单描述
> - STARS：镜像的星级数，表示镜像的受欢迎程度
> - OFFICIAL：表示镜像是否为官方镜像，`[OK]` 表示这是一个官方镜像，空白表示非官方镜像



2. **拉取镜像**

**作用：**从Docker Hub或其他镜像仓库中下载指定的镜像。

```bash
docker pull <image_name>:<tag>
```

示例

```bash
# 示例
root@onlyubuntu:~# docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
f11c1adaa26e: Pull complete 
c6b156574604: Pull complete 
ea5d7144c337: Pull complete 
1bbcb9df2c93: Pull complete 
537a6cfe3404: Pull complete 
767bff2cc03e: Pull complete 
adc73cb74f25: Pull complete 
Digest: sha256:67682bda769fae1ccf5183192b8daf37b64cae99c6c3302650f6f8bf5f0f95df
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

> 注意：
>
> - 若再pull镜像时没有指定版本，则默认拉取该镜像最后的一个版本，即tag：latest



3. **列出本地镜像**

**作用：**显示当前系统上所有已下载的Docker镜像。

```bash
docker images
# 或者
docker image ls
```

示例：

```bash
root@onlyubuntu:~# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
nginx         latest    fffffc90d343   2 weeks ago     188MB
ubuntu        latest    35a88802559d   4 weeks ago     78.1MB
hello-world   latest    d2c94e258dcb   14 months ago   13.3kB
```

> 注意：
>
> - **PEROSITORY**：镜像所属的仓库名称，也是pull时的镜像名称
> - **TAG**：镜像的标签，也是镜像的版本，默认时lastet
> - **IMAGE ID**：镜像的id，这是一个SHA256哈希值
> - **CREATED**：镜像的构建时间
> - **SIZE**：镜像占用的磁盘空间大小



4. **删除镜像**

**作用：**从本地删除指定的镜像

```bash
docker rmi <image_name>:<tag>
# 或者通过镜像id进行删除
docker rmi <image_id>
```

示例：

```bash
root@onlyubuntu:~# docker rmi nginx:latest 
Untagged: nginx:latest
Untagged: nginx@sha256:67682bda769fae1ccf5183192b8daf37b64cae99c6c3302650f6f8bf5f0f95df
Deleted: sha256:fffffc90d343cbcb01a5032edac86db5998c536cd0a366514121a45c6723765c
Deleted: sha256:9f4b5d44149fd139616539e0ef5311a14338a970f25733ba95b4ae6d3becdf0d
Deleted: sha256:8e6e10fbcca1bb180c5cfc805a37240945a6ba703cb1f985d4d3b8a1c954fc5b
Deleted: sha256:dcec89b921d64a1d2f748c450832a4c5624219bbb1b696e1a606bff78b7afa60
Deleted: sha256:4994a8d5939af297abf594b7ab714dfb72e57217b94bf0a250a62903cbdb6d84
Deleted: sha256:8b2bc37f672b15bea06a204790da9f384ef7b06feccade3fd3b1945b63df5aef
Deleted: sha256:a4197512070a01764db77b424100c1f81f0ed696380b19bc26b6e72fafef0709
Deleted: sha256:32148f9f6c5aadfa167ee7b146b9703c59307049d68b090c19db019fd15c5406
```

> 注意：
>
> - 删除镜像时，必须指定镜像的版本



5. **打包镜像**

**作用：**命令用于将一个或多个Docker镜像保存到一个tar归档文件中，可以在不同的系统之间传输或备份这些镜像。

```bash
docker save [OPTIONS] IMAGE [IMAGE...]
```

> 常用选项
>
> - -o：指定输出文件的路径。如果未指定此选项，输出将发送到标准输出（stdout）

示例

```bash
# 保存一个名为my_image的镜像到一个名为my_image.tar的文件中
docker save -o my_image.tar my_image:latest

# 保存多个镜像到一个tar文件中
docker save -o multiple_images.tar my_image:latest another_image:latest
```



6. **加载镜像**

**作用：**从一个tar归档文件中加载一个或多个Docker镜像

```bash
docker load [OPTIONS]
```

> 常用选项
>
> - -i：指定要加载的tar文件路径（几乎是必须的）

示例

```bash
# 从一个名为my_image.tar的文件加载镜像
docker load -i my_image.tar
```





#### 3.2 容器操作

1. **运行容器**

**作用：**创建并启动一个新的容器。

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

> 说一些常用的选项：
>
> - -d：将容器放在后台运行
> - --name：指定容器的名称
> - -p：将主机的端口映射到容器的端口
> - -v：绑定挂载一个卷
> - -e：设置容器的环境变量
> - --rm：容器退出时，自动删除容器
> - --network：指定容器使用的网络模式或连接到的网络

示例：

```bash
docker run -d --name docker_ubuntu -p 8080:8080 ubuntu tail /dev/null
```



2. **列出容器**

**作用：**列出所有运行中的容器

```bash
docker ps [OPTIONS]
```

> 常用选项
>
> - -a：列出所有容器，不管是否在运行中
> - -q：只显示容器的id
> - -l：显示最近创建的一个容器
> - -n：显示最近创建的n个容器
> - -f：根据条件过滤容器
> - -s：显示容器所占磁盘空间大小

示例：

```bash
root@onlyubuntu:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                                                  NAMES
75e99af8f64d   ubuntu    "tail -f /dev/null"      About an hour ago   Up About an hour   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp              docker_ubuntu
ce8ba5cee91c   mysql     "docker-entrypoint.s…"   4 hours ago         Up 58 minutes      0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   docker_mysql
```



3. **停止容器**

**作用：**停止一个运行中的容器

```bash
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

> 常用选项
>
> - -t：指定在发送 SIGKILL 信号之前等待容器停止的秒数。如果未指定，默认值为 10 秒。SIGKILL信号用于强制停止容器
> - 可以指定多个容器，用空格隔开

示例

```bash
docker stop -t 5 mycontainer
```



4. **启动容器**

**作用：**启动一个已经停止的容器

```bash
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

> 常用选项
>
> - -a：将当前容器的标准输出、标准错误信息输出到当前终端控制台
> - -i：启动容器的同时，打开标准输入，能将当前终端的命令输入到容器中



5. **删除容器**

**作用：**删除一个已经停止的容器

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

> 常用选项
>
> - -f：强制删除容器，不管是否正在运行
> - -v：删除与容器关联的匿名卷



6. **执行命令**

**作用：**在运行的容器中执行命令。

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

> 常用选项
>
> - -i：保持标准输入打开。适用于需要在容器内进行交互的命令。
> - -t：分配一个伪终端。通常与 `-i` 一起使用，实现交互式会话。
> - -d：分离模式运行命令。即在容器后台运行指定的命令
> - -u：指定运行命令的身份

示例：

```bash
# 这条命令在 mycontainer 容器中启动一个交互式的 bash 终端。
docker exec -it mycontainer bash

# 这条命令会在 mycontainer 容器中后台运行 some_command。
docker exec -d mycontainer some_command

# 这条命令会以 username 用户的身份在 mycontainer 容器中运行 some_command。
docker exec -u username mycontainer some_command

```



7. **查看日志**

**作用：**显示容器的日志输出

```bash
docker logs [OPTIONS] CONTAINER
```

> 常用选项
>
> - -f：实时跟踪日志输出，类似tail -f
> - --tail && -n：只显示日志的最后n行
> - -t：在日志前面加上时间戳
> - --since：显示自指定时间以来的日志，可以使用 RFC3339 格式或相对时间（如 `1h`、`1m`）。
> - --until：显示直到指定时间的日志，可以使用 RFC3339 格式或相对时间。
> - --details：显示提供给日志的额外详细信息（如果可用）。

示例

```bash
# 显示 mycontainer 容器日志的最后 100 行。
docker logs --tail 100 mycontainer

# 显示 mycontainer 容器过去一小时的日志。
docker logs --since 1h mycontainer

# 显示 mycontainer 容器直到 10 分钟前的日志。
docker logs --until 10m mycontainer

```



8. **详细信息**

**作用：**查看容器的详细信息，如配置、网络设置、挂载点等。

```bash
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

> 常用选项
>
> - -f：指定输出的格式，使用 Go 模板语法。
> - -s：显示容器的大小（适用于容器）。
> - --type：指定要查看的对象类型，可以是 `container`、`image`、`volume` 或 `network`。

示例

```bash
# 查看容器详细信息
docker inspect --type container mycontainer

# 查看镜像详细信息
docker inspect --type image myimage

```



9. **重启容器**

**作用：**重启一个容器

```bash
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

> 常用选项
>
> - -t：在发送 SIGKILL 信号之前等待容器停止的秒数。如果未指定，默认值为 0 秒。



10. **容器和主机之间的复制**

**作用：**在容器和主机之间复制文件或目录。

```bash
# 将容器的文件复制到主机中
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-

# 将主机的文件复制到容器中
docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
```



11. **容器重命名**

**作用：**给一个容器重命名

```bash
docker rename CONTAINER NEW_NAME
```





### 4 创建镜像

创建自己的镜像，能够更好利用docker的可移植性

> 注意：
>
> - 创建的每个自定义镜像都必须有一个基础镜像



#### 4.1 使用commit

创建镜像最简单的方法就是使用`docker commit`方法

**作用：**将一个运行中的或者未运行中的容器打包为一个镜像

```bash
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

> 常用选项
>
> - -a：为新创建的镜像设置作者信息。
> - -m：为新创建的镜像设置提交消息，类似于git的提交消息。
> - -p：在创建镜像前暂停容器（默认行为），以确保文件系统的一致性。
> - -c：对Dockerfile的指令进行更改或添加。这可以用于在提交镜像时进行一些额外的配置。

示例

```bash
docker run -d --name my_container ubuntu:latest

# 修改容器状态，例如安装一些软件包
docker exec my_container apt-get update
docker exec my_container apt-get install -y nginx

# 提交容器为新的镜像，带有作者信息和提交消息
docker commit -a "John Doe <john.doe@example.com>" -m "Installed nginx" my_container my_image:nginx_installed

# 提交容器为新的镜像，并更改默认启动命令
docker commit --change='CMD ["nginx", "-g", "daemon off;"]' my_container my_image:nginx_custom_cmd

```



#### 4.2 使用Dockerfile

