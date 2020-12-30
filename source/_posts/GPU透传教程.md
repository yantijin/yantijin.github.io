---
title: GPU透传
date: 2020-12-29 21:05:01
tags: 安装教程
---
<!--more-->

> 参考[链接](https://medium.com/@MARatsimbazafy/journey-to-deep-learning-nvidia-gpu-passthrough-to-lxc-container-97d0bc474957)

### 创建容器

> 新建CT，内存32G，存储1024G，选ubuntu18.04的版本，需要注意将非高优先级选项去掉,假设名字为115

```
## 首先更换软件源，并更新
apt update
apt upgrade
apt install build-essential
```

### Host配置

> 首先查看host中是否已经安装好驱动了，`nvidia-smi`,如果有则下面host步骤到装驱动部分都不用再弄。

* apt update

* apt upgrade

* apt install vim

* apt install build-essential

* 装驱动:

  * 禁用nouveau：

    ```
    vim /etc/modprobe.d/blacklist-nouveau.conf
    ```

    添加如下内容

    ```
    blacklist nouveau
    options nouveau modeset=0
    ```

    重新生成内核initramfs:

    ```
    update-initramfs -u
    ```

  * 确认内核版本和headers版本一致，如果不一致则进行更新，并安装 kernel-devel

    * apt install kernel-devel

  * 装驱动

    ```
    wget -c https://cn.download.nvidia.com/XFree86/Linux-x86_64/450.80.02/NVIDIA-Linux-x86_64-450.80.02.run
    sudo sh ./NVIDIA-Linux-x86_64-450.80.02.run (一路默认选项即可)
    apt install nvidia-smi
    ```

* 配置驱动

  ```
  vim  /etc/modules-load.d/modules.conf
  ```

  添加如下内容

  ```
  # /etc/modules: kernel modules to load at boot time.
  
  # This file contains the names of kernel modules that should be loaded
  # at boot time, one per line. Lines beginning with “#” are ignored.
  nvidia
  nvidia_uvm
  ```

  保存退出并更新

  ```
  update-initramfs -u
  ```

* 查看`/dev/nvidia`中是否包含nvidia-ctl nvidia0和nvidia-uvm等文件，若没有

  ```
  usr/bin/nvidia-smi -L && /bin/chmod 666 /dev/nvidia*
  /usr/bin/nvidia-modprobe -c0 -u && /bin/chmod 0666 /dev/nvidia-uvm*
  ```

* 重启服务器

* 查看nvidia-smi看是否安装驱动成功，加上

  ```
  $ modprobe nvidia-uvm
  $ ls /dev/nvidia* -l
  crw-rw-rw- 1 root root 243, 0 Jan 16 02:20 /dev/nvidia-uvm
  crw-rw-rw- 1 root root 195, 0 Jan 16 02:16 /dev/nvidia0
  crw-rw-rw- 1 root root 195, 255 Jan 16 02:16 /dev/nvidiactl
  ```

* 配置container文件

  ```
  vim /etc/pve/lxc/115.conf
  ```

  加入如下内容

  ```
  lxc.cgroup.devices.allow: c 195:* rwm
  lxc.cgroup.devices.allow: c 243:* rwm
  lxc.mount.entry: /dev/nvidia0 dev/nvidia0 none bind,optional,create=file
  lxc.mount.entry: /dev/nvidiactl dev/nvidiactl none bind,optional,create=file
  lxc.mount.entry: /dev/nvidia-uvm dev/nvidia-uvm none bind,optional,create=file
  lxc.mount.entry: /dev/nvidia-modeset dev/nvidia-modeset none bind,optional,create=file
  lxc.mount.entry: /dev/nvidia-uvm-tools dev/nvidia-uvm-tools none bind,optional,create=file
  ```

  **注意**：其中195 243是根据上一步中`ls /dev/nvidia* -l`的输出中的数值确定的

* 重启前面创建的容器，并确认/dev/中包含了nvidia0, nvidia-ctl, nvidia-uvm这三项

  ```
  ls /dev/nvidia* -l
  ```

### 容器配置

* 安装cuda

  ```
  wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
  sudo sh cuda_10.2.89_440.33.01_linux.run
  ```

  **注意安装过程中不要选cuda中自带的驱动，切记切记**， 成功之后，添加cuda路径到系统

  ```
  vim ~/.bashrc
  ```

  添加如下内容

  ```
  export PATH=/usr/local/cuda-10.2/bin${PATH:+:${PATH}}
  export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
  ```

  保存，退出

  测试是否成功 `nvcc -V`

* 安装nvidia-utils

  ```
  apt install nvidia-utils-450
  ```

  测试透传是否成功

  ```
  nvidia-smi
  ```

### 安装jupyter-hub

> 参考 [链接](https://tljh.jupyter.org/en/latest/install/custom-server.html)

```
apt install python3 python3-dev git curl
```

```
curl -L https://tljh.jupyter.org/bootstrap.py | sudo -E python3 - --admin root
```

Press `Enter` to start the installation process. This will take 5-10 minutes, and will say ‘Done!’ when the installation process is complete.

## GPU集群安装教程

* 前提，几台CT容器均已配置GPU透传成功，只需要其中一个安装jupyter-hub即可,假设为A,其他两台为B1, B2

### 配置ssh免密登录

* B1, B2上操作：

  \#1. 修改sshd配置 
  vim /etc/ssh/sshd_config
  ​
  \#2. 改动如下
  Port 12345
  PermitRootLogin yes
  PubkeyAuthentication yes
  AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2
  ​
  \#3. 保存配置，启动sshd
  /usr/sbin/sshd
  ​
  \#4. 查看ssh是否启动
  ps -ef | grep ssh

* A上操作:

  \#1. 生成秘钥，一直回车即可，注意生成秘钥位置
  ssh-keygen -t rsa
  ​
  \#2. 在B上创建.ssh文件夹
  ssh -p 12345 B的ip （输入密码）

  mkdir -p .ssh
  ​退出B返回到A，输入`exit`

  #3. 将公钥添加到B的authorized_keys里，注意A的秘钥路径是否正确
  cat .ssh/id_rsa.pub | ssh -p 12345 B 'cat >> .ssh/authorized_keys'
  ​
  \#测试是否可以免密登录
  ssh -p 12345 B的ip

### 安装syncthing，让三台机器有共享文件目录

* apt install syncthing

* 更新到最新版本

* ```
  vim ~/.config/syncthing/config.xml
  ```

  将里面 `0.0.0.0:8384`改为`127.0.0.1:8384`

  将三台机器设置一个同步的目录

### 在各机器行安装horovod

> 参考[链接](https://zhuanlan.zhihu.com/p/63158504)

* apt install cmake
* 安装nccl
* 安装OpenMPI，并配置相关路径
* 安装horovod

