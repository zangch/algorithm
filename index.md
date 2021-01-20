# Docker 初学介绍
## Linux 容器
　Linux 容器是一种虚拟化技术，不是模拟一个完整的操作系统，而是对进程进行隔。  
## Docker
　Docker 属于 Linux 容器的一种封装，提供简单易用的容器使用接口。  
### Docker 安装
　
### image 文件
　
### container 
　container 可运行的进程和 image 实例化的文件。  

### Dockerfile 文件
　Docker 根据 Dockerfile 文件生成二进制的 image 文件。  
 
　1. 编写 Dockerignore 文件    
```  
　写入要忽略的文件  
　若没有要忽略的文件可以不创建  
```
　2. 编写 Dockerfile文件  
```
　FROM [imageName]:[version] 继承官方的image
　MAINTAINER [name] 维护者信息
　
　ADD/CPPY [localDir] [containerDir] 将当前目录的所有文件（除了 .dockerignore ) ,都拷贝到 image 文件的 /app 目录，ADD 会自动解压和可以访问网络资源
　WORDIR /app 指定工作目录
　VOLUME [localDir] 指定持久化目录
　EXPOSE [port] 暴露容器端口
　RUN [command]
　CMD [command] RUN命令在 image 文件的构建阶段执行，执行结果都会打包进入 image 文件；CMD命令则是在容器启动后执行。另外一个 Dockerfile 可以包含多个RUN命令，但是只能有一个CMD命令。注意，指定了CMD命令以后，docker container run命令就不能附加命令了，否则它会覆盖CMD命令。
　ENTRYPOINT [command] 
```  

### Docker 指令  
```
　`docker version`  查看版本  
　`systemctl status docker` docker 服务  
　`docker image ls` image 列表  
　`docker image pull [imageName]` 拉取仓库中 image 到本地  
　`docker image rm [imageNmae]` 删除 image  
　`docker container ls` 正在运行 container 列表，`--all` container列表  
　`docker container run [imageName]` 从 image 生成容器实例,该指令会遍历本地 image，若没有会自动 pull  
　`docker container run --rm -p [localPort]:[containerPort] -it/-d [imageName]:[version] [command]` -it 容器的 shell 映射到当前, shell: /bin/bash, --rm: 运行后自动删除,-d 后台运行 
　`docker container start [containerID]` 启动已生成容器  
　`docker container stop [containerID]` 终止容器进程 SIGTERM 信号会进行收尾清理工作  
　`docker container kill [containerID]` 终止容器进程 SIGKILL 信号会立即终止  
　`docker container rm [containerID]` 删除容器文件  
　`docker image build -t [imageName]:[version] [dir]` 创建 image 文件，version 默认为 latest ，路径可以用 . 表示当前路径  
　`docker container logs [containerID]` 查看容器的输出  
　`docker container exec -it [containerID] /bin/bash` 进入正在运行的容器进程  
　`docker container cp [containID]:[/path/to/file]` 拷贝文件  
　`docker commit -a [myName] [containerID] [imageName]:[version]` 提交容器信息打包成镜像
```
