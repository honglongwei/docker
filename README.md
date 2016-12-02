# docker学习笔记idoc(i-docker-book)

---

### docker的简介

  Docker是一个开源的引擎，可以轻松的为任何应用创建一个轻量级的、可移植的、自给自足的容器。简言之，docker就是用go开发的一种轻量级虚拟化容器。

  ![Image](https://github.com/honglongwei/docker/blob/master/images/zhu.jpg)
  
  Docker 使用客户端-服务器 (C/S) 架构模式。Docker 客户端会与 Docker 守护进程进行通信。Docker 守护进程会处理复杂繁重的任务，例如建立、运行、发布你的 Docker 容器。Docker 客户端和守护进程可以运行在同一个系统上，当然你也可以使用 Docker 客户端去连接一个远程的 Docker 守护进程。Docker 客户端和守护进程之间通过 socket 或者 RESTful API 进行通信。

  Docker 守护进程运行在一台主机上。用户并不直接和守护进程进行交互，而是通过 Docker 客户端间接和其通信。Docker 客户端，实际上是 docker 的二进制程序，是主要的用户与 Docker 交互方式。它接收用户指令并且与背后的 Docker 守护进程通信，如此来回往复。


### docker的三大组件

* #### 镜像(images)

  Docker 镜像是Docker容器运行时的只读模板，每一个镜像由一系列的层(layers)组成。Docker使用 UnionFS来将这些层联合到单独的镜像中。UnionFS 允许独立文件系统中的文件和文件夹(称之为分支)被透明覆盖，形成一个单独连贯的文件系统。正因为有了这些层的存在，Docker是如此的轻量。当你改变了一个Docker镜像，比如升级到某个程序到新的版本，一个新的层会被创建。因此，不用替换整个原先的镜像或者重新建立(在使用虚拟机的时候你可能会这么做)，只是一个新 的层被添加或升级了。现在你不用重新发布整个镜像，只需要升级，层使得分发 Docker 镜像变得简单和快速。
  
* #### 仓库(registeries)
  
  Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。同样的，Docker 仓库也有公有和私有的概念。公有的 Docker 仓库名字是 Docker Hub。Docker Hub 提供了庞大的镜像集合供使用。这些镜像可以是自己创建，或者在别人的镜像基础上创建。Docker 仓库是 Docker 的分发部分。
  
* #### 容器(containers)

  Docker 容器和文件夹很类似，一个Docker容器包含了所有的某个应用运行所需要的环境。每一个 Docker 容器都是从 Docker 镜像创建的。Docker 容器可以运行、开始、停止、移动和删除。每一个 Docker 容器都是独立和安全的应用平台，Docker 容器是 Docker 的运行部分。
  
  
### 为什么要学习docker

  我学习docker主要是因为Go，也是为了更好的实现devops的桥接，随着caas平台的推进，和打包即应用的快速部署等吸引所驱使。

### docker的优缺点

  1. 标准化应用发布，docker容器包含了运行环境和可执行程序，可以跨平台和主机使用；
  2. 快速部署和启动，VM启动一般是分钟级，docker容器启动是秒级，即启即用；
  3. 方便构建基于SOA架构或微服务架构的系统，通过服务编排，更好的松耦合；
  4. 轻量低成本，占有更少的磁盘空间，一台主机可以启动上千个容器；
  5. 方便持续集成，通过与代码进行关联使持续集成非常方便；
  6. 安全隔离的执行环境，每个运行的容器互不影响；
  7. 文件系统分离，每一个进程容器跑在完全分离的root权限的文件系统下
  资源分离，系统资源（像CPU、内存）能被指定的分配给每一个进程容器,使用cgroups
  网络分离，使用一个虚拟的接口和IP地址，每一个进程容器跑在它自己的网络命名空间
  丰富的镜像资源，用户可以方便的在此基础上构建自己的容器运行；

  #### Docker VS VM虚拟机: 优势那就是轻量和高性能和便捷性
  
  ![Image](https://github.com/honglongwei/docker/blob/master/images/2.jpg) 
  ![Image](https://github.com/honglongwei/docker/blob/master/images/3.jpg)
  
  * 快 <br>
　　运行时的性能可以获取极大提升(经典的案例是提升97%) <br>
　　管理操作(启动，停止，开始，重启等等) 都是以秒或毫秒为单位的。 <br>

  * 敏捷 <br>
　　像虚拟机一样敏捷，而且会更便宜，在bare metal(裸机)上布署像点个按钮一样简单。<br>

  * 灵活 <br>
　　将应用和系统“容器化”，不添加额外的操作系统 <br>

  * 轻量 <br>
　　你会拥有足够的“操作系统”，仅需添加或减小镜像即可。在一台服务器上可以布署100~1000个Containers容器。<br>

  * 便宜 <br>
　　开源的，免费的，低成本的。由现代Linux内核支持并驱动。注* 轻量的Container必定可以在一个物理机上开启更多“容器”，注定比VMs要便宜。<br>

  * 生态系统 <br>
　　正在越来越受欢迎，只需要看一看Google的趋势就知道了， docker or LXC.  <br>
　　还有不计其数的社区和第三方应用。<br>

  * 云支持 <br>
　　不计其数的云服务提供创建和管理Linux容器框架。 <br>
　　有关Docker性能方面的优势，还可参考此IBM工程师对性能提升的评测，从各个方面比VMs(OS系统级别虚拟化)都有非常大的提升。 <br>
　　Performance Characteristics of VMs vs Docker Containers by Boden Russel (IBM) <br>
　　Performance characteristics of traditional v ms vs docker containers  <br>

  * 有争论的部分 <br>
　　任何项目都会有争论，就像Go，像NodeJS, 同样Docker也有一些。 <br>

  * 能否彻底隔离<br>
　　在超复杂的业务系统中，单OS到底能不能实现彻底隔离，一个程序的崩溃/内存溢出/高CPU占用到底会不会影响到其他容器或者整个系统?很多人对Docker能否在实际的多主机的生产环境中支持关键任务系统还有所怀疑。 注* 就像有人质疑Node.JS单线程快而不稳，无法在复杂场景中应用一样。 <br>
　　不过可喜的是，目前Linux内核已经针对Container做了很多改进，以支持更好的隔离。<br>

  * GO语言还没有完全成熟 <br>
　　Docker由Go语言开发，但GO语言对大多数开发者来说比较陌生，而且还在不断改进，距离成熟还有一段时间。此半git、半包管理的方式让一些人产生不适。 <br>

  * 被私有公司控制  <br>
　　Docker是一家叫Dotcloud的私有公司设计的，公司都是以营利为目的，比如你没有办法使用源代码编绎Docker项目，只能使用黑匣子编出的Docker二进制发行包，未来可能不是完全免费的。 目前Docker已经推出面向公司的企业级服务(咨询、支持和培训)。 <br>
  

### docker的主要用途

  * 系统容器
  
  * 应用容器
  
  * 存储容器
  
### docker的应用场景

  1. 简化配置
  这是Docker公司宣传的Docker的主要使用场景。虚拟机的最大好处是能在你的硬件设施上运行各种配置不一样的平台（软件、系统），Docker在降低额外开销的情况下提供了同样的功能。它能让你将运行环境和配置放在代码中然后部署，同一个Docker的配置可以在不同的环境中使用，这样就降低了硬件要求和应用环境之间耦合度。

  2. 代码流水线（Code Pipeline）管理
  前一个场景对于管理代码的流水线起到了很大的帮助。代码从开发者的机器到最终在生产环境上的部署，需要经过很多的中间环境。而每一个中间环境都有自己微小的差别，Docker给应用提供了一个从开发到上线均一致的环境，让代码的流水线变得简单不少。

  3. 提高开发效率
  这就带来了一些额外的好处：Docker能提升开发者的开发效率。如果你想看一个详细一点的例子，可以参考Aater在DevOpsDays Austin 2014 大会或者是DockerCon上的演讲。
  不同的开发环境中，我们都想把两件事做好。一是我们想让开发环境尽量贴近生产环境，二是我们想快速搭建开发环境。
  理想状态中，要达到第一个目标，我们需要将每一个服务都跑在独立的虚拟机中以便监控生产环境中服务的运行状态。然而，我们却不想每次都需要网络连接，每次重新编译的时候远程连接上去特别麻烦。这就是Docker做的特别好的地方，开发环境的机器通常内存比较小，之前使用虚拟的时候，我们经常需要为开发环境的机器加内存，而现在Docker可以轻易的让几十个服务在Docker中跑起来。

  4. 隔离应用
  有很多种原因会让你选择在一个机器上运行不同的应用，比如之前提到的提高开发效率的场景等。
  我们经常需要考虑两点，一是因为要降低成本而进行服务器整合，二是将一个整体式的应用拆分成松耦合的单个服务（译者注：微服务架构）。如果你想了解为什么松耦合的应用这么重要，请参考Steve Yege的这篇论文，文中将Google和亚马逊做了比较。

  5. 整合服务器
  正如通过虚拟机来整合多个应用，Docker隔离应用的能力使得Docker可以整合多个服务器以降低成本。由于没有多个操作系统的内存占用，以及能在多个实例之间共享没有使用的内存，Docker可以比虚拟机提供更好的服务器整合解决方案。

  6. 调试能力Docker
  提供了很多的工具，这些工具不一定只是针对容器，但是却适用于容器。它们提供了很多的功能，包括可以为容器设置检查点、设置版本和查看两个容器之间的差别，这些特性可以帮助调试Bug。你可以在《Docker拯救世界》的文章中找到这一点的例证。

  7. 多租户环境
  另外一个Docker有意思的使用场景是在多租户的应用中，它可以避免关键应用的重写。我们一个特别的关于这个场景的例子是为IoT（译者注：物联网）的应用开发一个快速、易用的多租户环境。这种多租户的基本代码非常复杂，很难处理，重新规划这样一个应用不但消耗时间，也浪费金钱。
  使用Docker，可以为每一个租户的应用层的多个实例创建隔离的环境，这不仅简单而且成本低廉，当然这一切得益于Docker环境的启动速度和其高效的diff命令。

  8. 快速部署
  在虚拟机之前，引入新的硬件资源需要消耗几天的时间。Docker的虚拟化技术将这个时间降到了几分钟，Docker只是创建一个容器进程而无需启动操作系统，这个过程只需要秒级的时间。这正是Google和Facebook都看重的特性。
  你可以在数据中心创建销毁资源而无需担心重新启动带来的开销。通常数据中心的资源利用率只有30%，通过使用Docker并进行有效的资源分配可以提高资源的利用率。


### docker的安装与使用
  * 安装  <br>
    1. centos <br>
       a. 配置epel源 <br>
          yum install -y yum-priorities && rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6

       b. 安装 docker-io febootstrap(febootstrap用来制作centos镜像的工具) <br>
          yum install docker-io febootstrap -y   <br>
          
    2. redhat  <br>
       a. 配置epel源  <br>
          rpm -ivh http://dl.Fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
          
       b.修改epel.repo源把https改成http,安装 docker-io <br>
         yum -y install docker-io
    
  * 使用
    1. 主配置文件 <br>
       ![Image](https://github.com/honglongwei/docker/blob/master/images/1.jpg)  <br>

    2. 启动 <br>
       [root@docker_004 ~]# /etc/init.d/docker start   <br>
       Starting docker:                                           [  OK  ]   <br>
       [root@docker_004 ~]# ps -ef |grep docker              <br>
       root      2502     1  5 09:59 pts/1    00:00:00 /usr/bin/docker -d    <br>
       
    3. 命令介绍 <br>
    （先有镜像，再用镜像启动一个个容器）<br>
     
     * #### docker search +镜像名 //搜索镜像<br>
       -s 40 列出收藏数不小于40的镜像 <br>
       
     * #### docker info  //显示 Docker 系统信息，包括镜像和容器数。<br>
     
     * #### docker pull +镜像名 //下载镜像 <br>
     
     * #### docker images //列出本地所有镜像。 <br>
       -a 列出所有镜像（含过程镜像） <br> 
       -f 过滤镜像 <br> 
       -q 仅列出镜像ID <br> 
       --tree 以树状结构列出镜像的所有提交历史 <br>
       
     * #### docker run //启动一个容器 <br>
       -d 后台运行容器，并返回容器ID<br>
       -i 以交互模式运行容器，通常与 -t 同时使用<br>
       -t 为容器重新分配一个伪输入终端，通常与 -i 同时使用<br>
       --dns 8.8.8.8 指定容器使用的DNS服务器，默认和宿主一致<br>
       --dns-search example.com 指定容器DNS搜索域名，默认和宿主一致<br>
       -h "mars" 指定容器的hostname<br>
       --name 设置容器的名称，在对容器操作的时候就可以使用名称，如：--name mysqlwp <br>
       -e 设置容器的环境变量，如：-e MYSQL_ROOT_PASSWORD=wordpressdocker <br>
       -p 设置容器和host的端口映射，如：-p 80：80 <br>
       -P 大P暴露容器所有端口映射 <br>
       --link 将两个容器关联起来，如：--link [容器名]:[镜像名] <br>
       -v 设置容器文件映射,如：-v "$PWD":/cookbook:ro ([宿主目录]:[容器对应目录]:[权限:ro表示 read-only]) <br>
       
     * #### docker ps //列出所有运行中容器 <br>
       -a 列出所有容器（含沉睡镜像） <br>
       -l 仅列出最新创建的一个容器 <br>
       -n=4 列出最近创建的4个容器 <br>
       -q 仅列出容器ID <br>
       -s 显示容器大小 <br>
      
     * #### docker attach vs docker exec //tty进入容器 <br>
       docker attach可以attach到一个已经运行的容器的stdin，然后进行命令执行的动作。 
       但是需要注意的是，如果从这个stdin中exit，会导致容器的停止。<br>
       [root@docker_004 ~]# docker exec -it test /bin/sh  <br>
    
     * #### docker start|stop|restart  //启动、停止和重启一个或多个指定容器  <br>
      -a 待完成<br>
      -i 启动一个容器并进入交互模式<br>
      -t 10 停止或者重启容器的超时时间（秒），超时后系统将杀死进程<br>
    
     * #### docker kill  //杀死一个或多个指定容器进程
    
     * #### docker inspect //检查镜像或者容器的参数，默认返回 JSON 格式<br>
      -f 指定返回值的模板文件<br>
      
     * #### docker logs //获取容器运行时的输出日志 <br>
      -f 跟踪容器日志的最近更新 <br>
      -t 显示容器日志的时间戳 <br>
      --tail="10" 仅列出最新10条容器日志<br>
    
     * #### docker rm  //从本地移除一个或多个指定的镜像<br>
       -f 强行移除该容器，即使其正在运行<br>
       -l 移除容器间的网络连接，而非容器本身<br>
       -v 移除与容器关联的空间<br>
       
     * #### docker rmi //从本地移除一个或多个指定的镜像 <br>
      -f 强行移除该镜像，即使其正被使用 <br>
      --no-prune 不移除该镜像的过程镜像，默认移除<br>

### 基于CentOS 6.5创建私有仓库

* 修改Docker参数<br>
    vim /etc/sysconfig/docker:<br>
    other_args="--insecure-registry 10.0.0.1:5000" <br>

    启动服务:<br>
    service docker start

* 创建存放images的目录
    mkdir -pv /data/registry

* 启动私有仓库容器, 并映射本地目录
    # 下载registry<br>
     docker pull registry<br>
    
    # 启动仓库容器<br>
     docker run -d -p 5000:5000 -v /data/registry:/tmp/registry registry<br>

    # 可以拉取一个比较小的images做测试<br>
     docker pull centos<br>

    # 更改images的tag<br>
     sudo docker tag centos 10.0.0.1:5000/centos<br>

    # Push images<br>
     sudo docker push 10.0.0.1:5000/centos<br>

    # Pull images<br>
     sudo docker pull 10.0.0.1:5000/centos<br>

    # 通过API查看<br>
     curl http://10.0.0.1:5000/v1/search<br>

    # 在私有仓库搜索<br>
     docker search 10.0.0.1:5000/centos<br>
     
     
###  创建一个系统容器并远程连接

* 下载系统镜像 <br>
  docker pull rastasheep/ubuntu-sshd 
      
* 启动容器<br>
  docker run -itd -p 16888:22 -h docker_test --name="docker_001" rastasheep/ubuntu-sshd /bin/bash<br>
  // -p 映射对应端口 -P 映射所有端口 -h 指定hostname  --name 给容器指定一个别名

* 进行容器<br>
  docker exec -it docker_001 /bin/bash<br> 
  // 若用docker attach docker_001进入容器exit退出容器则容器停止<br> 
  /etc/init.d/ssh start
  
* 远程连接<br> 
  ssh -p 16888 root@10.0.0.1
 
* 对容器做了修改保存提前镜像<br> 
  // 容器做了一定的修改，以后想继续使用可以保存镜像并提交到自己的私有仓库<br> 
  docker ps // 不加参数列出正在运行的所有容器，-l显示最后一次创建的容器, -a显示所有容器包括非运行的<br> 
  docker stop docker_001<br> 
  docker commit docker_001 docker_v1 //保存修改<br> 
