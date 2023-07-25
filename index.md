## Docker的历史 2010年，几个高it的年轻人，成立了一家公司
做一些 pass 的云计算服务！LXC 有关的容器技术 ！
他们将此技术（容器化技术） 命名就是 Docker


开源
2013年开源
2014,Docker1.0
```vm, linux 原生镜像（一个电脑！）隔离，需要开启多个虚拟机 几个G 几分钟 docker， 隔离 镜像（最核心的环境 4m + jdk +mysql）十分的小巧， 运行镜像就行 几个M KB 秒级启动```

> ## 聊聊Docker >Docker 是基于 GO 语言开发的一个开源项目 url: http://www.docker.com
doc: http://docs.docker.com 文档很全
hub :http://hub.docker.com


## docker能干嘛 ### 虚拟机缺点 1. 资源占用多 2. 冗余步骤多 3. 启动很慢

### 容器化技术 容器化技术不是模拟完整的操作系统
比较不同
+ 传统虚拟机，虚拟出一整个硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件 + 容器内的应用直接运行在宿主机的内容，容器是没有自己内核的，也没有虚拟硬件，所以就轻便了 + 每个容器时相互隔离，每个容器都有属于自己的文件系统，互不影响 ### DevOps（开发、运维） **应用更快速的交付和部署**
传统：一堆帮助文档，安装程序
Docker: 打包镜像发布测试，一键运行
**更便捷的升级和扩缩容**
使用了docker后，就像搭积木一样
项目打包为一个镜像，扩展 服务器A 服务器B
**更简单的系统运维**
在容器化之后，我们的开发，测试环境都是高度一致的
**更高效的计算资源利用**
Docker 是 内核级别的虚拟化，可以在一个物理机上运行很多的容器！服务器的性能可以被榨干到极致


# Docker的安装 ## Docker的基本组成 https://devopedia.org/images/article/101/8323.1565281088.png
### 镜像（image）：
docker镜像就好比是一个模板，可以通过这个模板老创建容器服务，tomcat镜像===> run ===> tomcat01容器（提供服务器），
通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）。
### 容器（container） Docker利用容器技术，独立运行一个或者一个组应用，通过镜像来创建的
启动，停止，删除，基本命令！
目前就可以把这个容器理解为一个简易的操作系统
### 仓库
仓库就是存放镜像的地方
仓库分为公用仓库和私有仓库
Docker Hub（默认是国外的）
阿里云……都有容器服务器（配置镜像加速！）
## 安装Docker > ### 环境准备 > 1.linux基础
> 2.centos 7
> 3.使用xshell远程对服务器进行操作

> ###环境查看
>系统是3.10以上的
> 5.15.90.1-microsoft-standard-WSL2 > > NAME="Rocky Linux" VERSION="8.7 (Green Obsidian)" ID="rocky" ID_LIKE="rhel centos fedora" VERSION_ID="8.7" PLATFORM_ID="platform:el8" PRETTY_NAME="Rocky Linux 8.7 (Green Obsidian)" ANSI_COLOR="0;32" LOGO="fedora-logo-icon" CPE_NAME="cpe:/o:rocky:rocky:8:GA" HOME_URL="https://rockylinux.org/" BUG_REPORT_URL="https://bugs.rockylinux.org/" ROCKY_SUPPORT_PRODUCT="Rocky-Linux-8" ROCKY_SUPPORT_PRODUCT_VERSION="8.7" REDHAT_SUPPORT_PRODUCT="Rocky Linux" REDHAT_SUPPORT_PRODUCT_VERSION="8.7" > ### 帮助文档 The Docker installation package available in the official Rocky Linux 8 repository may not be the latest version. To get the latest and greatest version, install Docker from the official Docker repository. This section shows you how to do just that. But first, let’s update the package database: sudo dnf check-update Next, add the official Docker repository: sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo While there is no Rocky Linux specific repository from Docker, Rocky Linux is based upon CentOS and can use the same repository. With the repository added, install Docker, which is composed of three packages: sudo dnf install docker-ce docker-ce-cli containerd.io After installation has completed, start the Docker daemon: sudo systemctl start docker Verify that it’s running: sudo systemctl status docker The output should be similar to the following, showing that the service is active and running: Output ● docker.service - Docker Application Container Engine Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled) Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago Docs: https://docs.docker.com Main PID: 749 (docker) Lastly, make sure it starts at every server reboot: sudo systemctl enable docker Installing Docker now gives you not just the Docker service (daemon) but also the docker command line utility, or the Docker client. We’ll explore how to use the docker command later in this tutorial. > ### 过程 # 1.卸载旧的版本 # 2.需要的安装包 # 3.设置镜像的仓库 # 更新软件包的索引 yum makecache # 4.安装docker相关的额外包 docker-ce 社区版 docker-ee 企业版 # 5.启动docker systemctl start docker # 6.查看docker状态 systemctl status docker # 7. Hello-World 检查不在本地后去拉取然后在运行 # 8.查看下载后的Hello-World镜像 [root@DESKTOP-BO85GLS ~]# docker images REPOSITORY TAG IMAGE ID CREATED SIZE hello-world latest 9c7a54a9a43c 7 weeks ago 13.3kB > ### 卸载docker(卸载依赖，删除资源) # 1.卸载依赖 yum remove docker-ce docker-ce-cli containerd.io # 2.删除资源 rm -rf /var/lib/docker # /var/lib/docker docker的默认工作路径 ## 阿里云镜像加速

## 回顾Hello World流程

## 底层原理 ### Docker是怎么工作的? Docker是一个 Client - Server结构的系统，Docker的守护进程运行在主机上。通过Socket从客户端访问！
DockerServer 接收到 Docker-Client 的指令，就会执行这个命令！
### Docker为什么比 vm 快 1. Docker有着比虚拟机更少的抽象层 2. Docker利用的是宿主机的内核，vm需要时Guest OS。
所有说，新建一个容器的时候，Docker不需要像vm一样重新加载一个操作系统内核，避免引导
虚拟机是加载Guest OS，分钟级别的，而docker是利用宿主机的OS ,省略了复杂的过程，秒级！
之后学习完所有的命令，再看理论，就会很清晰


# docker的常用命令 ## Help docker version docker info docker command --help
## 镜像命令 docker images [root@DESKTOP-BO85GLS ~]# docker images REPOSITORY TAG IMAGE ID CREATED SIZE hello-world latest 9c7a54a9a43c 7 weeks ago 13.3kB # 解释 REPOSITORY 镜像的仓库源 TAG 镜像的标签 IMAGE ID 镜像的id CREATED 镜像的创建时间 SIZE 镜像的大小 # 可选项 -a --all #列出所有的镜像 -q --quiet #只显示镜像的id docker search [root@DESKTOP-BO85GLS ~]# docker search mysql NAME DESCRIPTION STARS OFFICIAL AUTOMATED mysql MySQL is a widely used, open-source relation… 14262 [OK] mariadb MariaDB Server is a high performing open sou… 5453 [OK] percona Percona Server is a fork of the MySQL relati… 616 [OK] phpmyadmin phpMyAdmin - A web interface for MySQL and M… 828 [OK] # 可选项 [root@DESKTOP-BO85GLS ~]# docker search --help Usage: docker search [OPTIONS] TERM Search Docker Hub for images Options: -f, --filter filter Filter output based on conditions provided --format string Pretty-print search using a Go template --limit int Max number of search results --no-trunc Don't truncate output --filter=STAR=3000 只搜索star数大于3000
docker pull 下载镜像 [root@DESKTOP-BO85GLS ~]# docker pull mysql Using default tag: latest # 如果不写tag ，默认就是latest latest: Pulling from library/mysql 72a69066d2fe: Pull complete 93619dbc5b36: Pull complete 99da31dd6142: Pull complete 626033c43d70: Pull complete 37d5d7efb64e: Pull complete ac563158d721: Pull complete d2ba16033dad: Pull complete 688ba7d5c01a: Pull complete 00e060b6d11d: Pull complete 1c04857f594f: Pull complete 4d7cfa90e6ea: Pull complete e0431212d27d: Pull complete Digest: sha256:e9027fe4d91c0153429607251656806cc784e914937271037f7738bd5b8e7709 Status: Downloaded newer image for mysql:latest docker.io/library/mysql:latest 等价于它 docker pull mysql docker pull docker.io/library/mysql:latest #指定版本下载 [root@DESKTOP-BO85GLS ~]# docker pull mysql:5.7 5.7: Pulling from library/mysql 72a69066d2fe: Already exists 93619dbc5b36: Already exists 99da31dd6142: Already exists 626033c43d70: Already exists 37d5d7efb64e: Already exists ac563158d721: Already exists d2ba16033dad: Already exists 0ceb82207cd7: Pull complete 37f2405cae96: Pull complete e2482e017e53: Pull complete 70deed891d42: Pull complete Digest: sha256:f2ad209efe9c67104167fc609cca6973c8422939491c9345270175a300419f94 Status: Downloaded newer image for mysql:5.7
**docker rmi** 删除镜像
docker rmi -f 容器id #删除指定的容器 docker rmi -f 容器id 容器id 容器id #删除多个容器 docker rmi -f $(docker images -aq) #删除全部的容器 ## 容器命令
