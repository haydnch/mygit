# 什么是docker

> **Docker** 是一个[开放源代码](https://zh.wikipedia.org/wiki/開放原始碼)[软件](https://zh.wikipedia.org/wiki/軟體)，是一个[开放平台](https://zh.wikipedia.org/wiki/開放平臺)，用于开发应用、交付（shipping）应用、运行应用。 Docker允许用户将基础设施（Infrastructure）中的应用单独分割出来，形成更小的颗粒（容器），从而提高交付软件的速度。
>
> **Docker容器**与虚拟机类似，但二者在原理上不同。容器是将[操作系统层虚拟化](https://zh.wikipedia.org/wiki/作業系統層虛擬化)，虚拟机则是虚拟化硬件，因此容器更具有便携性、高效地利用服务器。 容器更多的用于表示 软件的一个标准化单元。由于容器的标准化，因此它可以无视基础设施（Infrastructure）的差异，部署到任何一个地方。另外，Docker也为容器提供更强的业界的隔离兼容。
>
> **Docker** 利用[Linux核心](https://zh.wikipedia.org/wiki/Linux核心)中的资源分离机制，例如[cgroups](https://zh.wikipedia.org/wiki/Cgroups)，以及Linux核心[名字空间](https://zh.wikipedia.org/w/index.php?title=Linux命名空間&action=edit&redlink=1)（namespaces），来创建独立的[容器](https://zh.wikipedia.org/wiki/作業系統層虛擬化)（containers）。这可以在单一Linux实体下运作，避免引导一个[虚拟机](https://zh.wikipedia.org/wiki/虛擬機器)造成的额外负担。Linux核心对名字空间的支持完全隔离了工作环境中应用程序的视野，包括行程树、[网络](https://zh.wikipedia.org/wiki/计算机网络)、用户ID与挂载文件系统，而核心的cgroup提供资源隔离，包括[CPU](https://zh.wikipedia.org/wiki/CPU)、[存储器](https://zh.wikipedia.org/wiki/電腦記憶體)、block I/O与网络。从0.9版本起，Dockers在使用抽象虚拟是经由[libvirt](https://zh.wikipedia.org/wiki/Libvirt)的[LXC](https://zh.wikipedia.org/wiki/LXC)与systemd - nspawn提供界面的基础上，开始包括libcontainer库做为以自己的方式开始直接使用由Linux核心提供的虚拟化的设施，

# docker应用场景

1. 加速本地开发
2. 自动打包和部署应用
3. 创建轻量、私有的PaaS环境
4. 自动化测试和持续集成/部署
5. 部署并扩展Web应用、数据库和后端服务器
6. 创建安全沙盒
7. 轻量级的桌面虚拟化

# docker核心组件

docker中有三大核心组件：

- **镜像**

   镜像是一个只读的静态模版，它保存了容器需要的环境和应用的执行代码，可以将镜像看成是容器的代码，当代码运行起来之后，就成了容器。镜像和容器的关系也类似于程序和进程的关系。

- **容器**

  容器是一个运行时环境，是镜像的一个运行状态。它是镜像执行的动态表现。

- **库**

  库是一个特定的用户存储镜像的目录，一个用户可以建立多个库来保存自己的镜像。

# docker命令

## 查看容器

启动docker后，使用`docker ps`命令可以查看当前正在运行的容器：

![image-20200819095745723](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200819095745723.png)

上面这条命令是查看运行着的容器，若想查看所有容器，可使用`docker ps -a `命令。

## 创建并启动容器

- nginx容器

  `docker run --name nginx -d -p 8080:80 nginx`

- redis容器

  `docker run -itd --name redis -p 6379:6379 redis`

  -d参数表示容器后台运行；-it参数：i表示开发容器的标准输入（STDIN），t表示告诉dcker为容器创建一个命令行终端。

## 容器内执行命令

如果容器在后台启动，可以使用`docker exec`在容器内执行命令。

`docker exec -it redis /bin/bash`

![image-20200819101823721](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200819101823721.png)

## 查看容器进程

使用`docker top`命令可以查看容器中正在运行的进程，首先确保容器已经启动。

![image-20200819102409989](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200819102409989.png)



