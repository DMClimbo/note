# 安装docker、nvidia-docker 

- 安装docker：

  > curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

  ​	

  

- 安装Nvidia-docker:

  > *# If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers*
  >
  > docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f sudo apt-get purge -y nvidia-docker
  >
  > ​		
  >
  > *# Add the package repositories*
  >
  > curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  >
  > ​	 sudo apt-key add -
  >
  > distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
  >
  > curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  >
  > ​	sudo tee /etc/apt/sources.list.d/nvidia-docker.list
  >
  > sudo apt-get update
  >
  > ​	
  >
  > *# Install nvidia-docker2 and reload the Docker daemon configuration*
  >
  > sudo apt-get install -y nvidia-docker2
  >
  > sudo pkill -SIGHUP dockerd
  >
  > ​		
  >
  > *# Test nvidia-smi with the latest official CUDA image*
  >
  > docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi



# 常用命令

## 容器声明周期管理

- run :创建一个新的容器并运行一个命令

  语法：docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

  OPTIONS说明：

  - **-a stdin:** 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；

  - **-d:** 后台运行容器，并返回容器ID；

  - **-i:** 以交互模式运行容器，通常与 -t 同时使用；

  - **-P:** 随机端口映射，容器内部端口**随机**映射到主机的端口

  - **-p:** 指定端口映射，格式为：**主机(宿主)端口:容器端口**

  - **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用；

  - **--name="nginx-lb":** 为容器指定一个名称；

  - **--dns 8.8.8.8:** 指定容器使用的DNS服务器，默认和宿主一致；

  - **--dns-search example.com:** 指定容器DNS搜索域名，默认和宿主一致；

  - **-h "mars":** 指定容器的hostname；

  - **-e username="ritchie":** 设置环境变量；

  - **--env-file=[]:** 从指定文件读入环境变量；

  - **--cpuset="0-2" or --cpuset="0,1,2":** 绑定容器到指定CPU运行；

  - **-m :**设置容器使用内存最大值；

  - **--net="bridge":** 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；

  - **--link=[]:** 添加链接到另一个容器；

  - **--expose=[]:** 开放一个端口或一组端口；

  - **--volume , -v:** 绑定一个卷

  - **--runtime==nvidia ** 使用nvidia-docker

    ​	

  实例： docker run -it nginx:latest /bin/bash

  ​				使用镜像nginx:latest以交互模式启动一个容器,在容器内执行/bin/bash命令。

  ​		

- start/stop/restart：启动/停止/重启 容器

  ​	

- kill：杀死一个运行中的容器

  ​	

- rm：删除一个或多个容器

  ​		

- pause/unpause：暂停/恢复容器中所有的进程

  ​	

- create：创建一个新容器但不启动它(用法同docker run)

  ​		

- exec：在运行的容器中执行命令

  语法：docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

  OPTIONS说明：

  - **-d :**分离模式: 在后台运行
  - **-i :**即使没有附加也保持STDIN 打开
  - **-t :**分配一个伪终端



​	

## 容器操作

- ps：列出容器

  语法：**docker ps [OPTIONS]**

  OPTIONS说明：

  - **-a :**显示所有的容器，包括未运行的。

  - **-f :**根据条件过滤显示的内容。

  - **--format :**指定返回值的模板文件。

  - **-l :**显示最近创建的容器。

  - **-n :**列出最近创建的n个容器。

  - **--no-trunc :**不截断输出。

  - **-q :**静默模式，只显示容器编号。

  - **-s :**显示总的文件大小。

    ​		

- top：查看容器中运行的进程信息，支持ps命令参数

  语法：**docker top [OPTIONS] CONTAINER [ps OPTIONS]**

  容器运行时不一定有/bin/bash终端来交互执行top命令，而且容器还不一定有top命令，可以使用docker top来实现查看container中正在运行的进程。

  ​			

- attach：连接到正在运行中的容器

  ​	

- port：列出指定容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。

  ​			

## 镜像操作

- pull：从镜像仓库中拉去或者更新指定镜像

  ​	

- push：将本地的镜像上传到镜像仓库

  ​	

- search：从Docker Hub上查找镜像

  ​	

- images：列出本地镜像

  ​	

- rmi：删除本地一个或多个镜像

  ​	

- build：使用Dockerfile创建镜像

  语法：**docker build [OPTIONS] PATH | URL | -**

  OPTIONS说明：

  - **--build-arg=[] :**设置镜像创建时的变量；
  - **--cpu-shares :**设置 cpu 使用权重；
  - **--cpu-period :**限制 CPU CFS周期；
  - **--cpu-quota :**限制 CPU CFS配额；
  - **--cpuset-cpus :**指定使用的CPU id；
  - **--cpuset-mems :**指定使用的内存 id；
  - **--disable-content-trust :**忽略校验，默认开启；
  - **-f :**指定要使用的Dockerfile路径；
  - **--force-rm :**设置镜像过程中删除中间容器；
  - **--isolation :**使用容器隔离技术；
  - **--label=[] :**设置镜像使用的元数据；
  - **-m :**设置内存最大值；
  - **--memory-swap :**设置Swap的最大值为内存+swap，"-1"表示不限swap；
  - **--no-cache :**创建镜像的过程不使用缓存；
  - **--pull :**尝试去更新镜像的新版本；
  - **--quiet, -q :**安静模式，成功后只输出镜像 ID；
  - **--rm :**设置镜像成功后删除中间容器；
  - **--shm-size :**设置/dev/shm的大小，默认值是64M；
  - **--ulimit :**Ulimit配置。
  - **--tag, -t:** 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。
  - **--network:** 默认 default。在构建期间设置RUN指令的网络模式

  

## 定义容器生成镜像

> docker  commit   -a = "yang"   -m = "test"   83f6e827a1fc   ubuntu:1.0
>
> ​		
>
> 命令为commit
>
> -a为作者
>
> -m为描述信息
>
> 83f6e827a1fc      运行中容器的ID
>
> ubuntu                    镜像名
>
> ：1.0                          版本号



​	













# 踩过的坑

- cuda镜像runtime和devel的区别：

  CUDA images come in three flavors and are available through the [NVIDIA public hub repository](https://hub.docker.com/r/nvidia/cuda).

  - `base`: starting from CUDA 9.0, contains the bare minimum (libcudart) to deploy a pre-built CUDA application.
     Use this image if you want to manually select which CUDA packages you want to install.
  - `runtime`: extends the `base` image by adding all the shared libraries from the CUDA toolkit.
     Use this image if you have a pre-built application using multiple CUDA libraries.
  - `devel`: extends the `runtime` image by adding the compiler toolchain, the debugging tools, the headers and the static libraries.
     Use this image to compile a CUDA application from sources.

  **nvcc作为cuda的编译器，在runtime的镜像中是不提供的，需要拉取devel版本镜像**

  





​	

# docker容器配置

- 安装常用软件

  > #vim
  >
  > ​	apt install vim
  >
  > ​	
  >
  > #ifconfig
  >
  > ​	apt install net-tools
  >
  > ​	
  >
  > #ssh
  >
  > ​	apt install openssh-server
  >
  > ​	vim  /etc/ssh/sshd_config
  >
  > ​	在文件最后加入：
  >
  > ​	PermitRootLogin yes #允许root登录
  > ​	PermitEmptyPasswords no #不允许空密码登录	
  >
  > ​	保存后重启ssh服务：
  >
  > ​	service ssh restart



- 安装python3.6

  > #更新软件源并下载python3.6和pip
  >
  > ​	apt update 
  >
  > ​	apt install python3.6
  >
  > ​	apt install python3-pip
  >
  > ​		
  >
  > #为python和pip建立软链接
  >
  > ​	ln -s  /usr/bin/python3.6  /usr/bin/python
  >
  > ​	ln -s  /usr/bin/pip3    /usr/bin/pip
  >
  > ​	
  >
  > #更改pip源为阿里云
  >
  > ​	mkdir  ~/.pip
  >
  > ​	vim  ~/.pip/pip.conf
  >
  > ​	在文本中添加下面一段：
  >
  > ​	[global]
  > ​	index-url = http://mirrors.aliyun.com/pypi/simple/
  >
  > ​	[install]
  > ​	trusted-host=mirrors.aliyun.com

  ​		

- 安装所需的包

  > pip install torch == 1.4.0
  >
  > 

