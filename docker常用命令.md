## 镜像相关操作

### 获取docker镜像

`docker pull docker_image_name `

### 导入本地镜像

`docker load -i docker_image_path`

--input/-i：导入指定文件

--quiet/-q：精简输出信息

### 保存镜像为tar文件

`docker save -o new_image_name.tar target_image_name:tag`

-o：输出到文件

### 创建一个新镜像

`docker commit -a "author_name" -m "uodate_description" target_image_id new_image_name:tag`

-a：镜像作者

-c：使用Dockerfile指令创建镜像

-m：提交的文字说明

-p：commit时暂停容器

### 查看镜像

`docker images`

-a：列出本地所有镜像

--digests：显示镜像的摘要信息

-f：显示满足条件的镜像

--format：指定返回值的模板文件

--no-trunc：显示完整的镜像信息

-q：只显示镜像id

`docker images ubuntu`

列出本地镜像中REPOSITORY为ubuntu的镜像列表

## 容器相关操作

### 查看容器

`docker ps`

-a：显示所有的容器，包括未运行

-q :静默模式，只显示容器编号

-l :显示最近创建的容器

-n :列出最近创建的n个容器

-f :根据条件过滤显示的内容

--format :指定返回值的模板文件

--no-trunc :不截断输出

-s :显示总的文件大小

### 创建容器

`docker run --name docker_name -it bash image_name:tag` 

-i：以交互模式

-t：为容器分配一个伪输入终端

--name：为容器指定名称

--volume/-v：绑定一个卷，映射本机地址与容器目录（workspace）

-d: 后台运行容器，并返回容器ID；

NV_GPU：指定使用的GPU序号，NV_GPU=0,1,2,3

-a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；

-P: 随机端口映射，容器内部端口随机映射到主机的端口

-p: 指定端口映射，格式为：主机(宿主)端口:容器端口

--dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致

--dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致

-h "mars": 指定容器的hostname

-e username="ritchie": 设置环境变量

--env-file=[]: 从指定文件读入环境变量

--cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定CPU运行

-m :设置容器使用内存最大值

--net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型

--link=[]: 添加链接到另一个容器

--expose=[]: 开放一个端口或一组端口

### 容器启停

`docker start/stop/restart docker_id`

exit：退出容器，容器会停止

ctrl+q,p：退出容器，容器后台运行

### 连接容器

`docker attach docker_id`

### 在运行容器中执行命令

`docker exec -it docker_id bash`

-d：后台运行

-i：即使没有附加也保持STDIN打开

-t：分配一个伪终端

attach连接后exit命令退出后容器会停止，exec则不会

### 删除容器

`docker rm docker_id`

-f：强制删除一个正在运行中的容器

-l：移除容器间网络链接

-v：删除与容器关联的卷

`docker rm $(docker pa -a -q)`

删除所有已经停止的容器

### 导出容器

`docker export -o new_docker_name.tar target_docker_id`

-o：将输入内容写到文件

### 导入容器为镜像

`docker import docker_name.tar new_image_name:tag`

-c：应用docker 指令创建镜像

-m：提交时的说明文字