# 如何用滴滴云在CentOS7.4上安装和使用ZStack企业版3.2.0（一）

## 前言

ZStack是下一代开源的云计算IaaS（基础架构即服务）软件。它主要面向未来的智能数据中心，通过提供灵活完善的APIs来管理包括计算、存储和网络在内的数据中心资源。用户可以利用ZStack快速构建自己的智能云数据中心，也可以在稳定的ZStack之上搭建灵活的云应用场景，例如VDI（虚拟桌面基础架构）、PaaS（平台即服务）、SaaS（软件即服务）等。

本系列文章将介绍，如何用滴滴云在CentOS7.4上安装ZStack企业版3.2.0，该版本对libvirt等虚拟化工具进行了重要升级。本篇作为该系列的第一篇，介绍的是安装管理节点。

## 准备

在开始之前，我们需要做以下准备工作：

* 一个滴滴云服务器，推荐配置为：CentOS 7.4，4核CPU 8G内存，250G SSD云盘存储，10Mbps带宽，并启用端口为5000的安全组规则。

## 第1步 - 下载ZStack3.2.0版本ISO进行升级

1. 切换到root权限:

```
$ sudo su
```

2. 下载最新的ISO，推荐下载ZStack官方的定制版ISO-c74版：ZStack-x86_64-DVD-3.2.0-c74.iso，您可以通过执行以下命令进行下载:

```
$ wget http://cdn.zstack.io/product_downloads/iso/ZStack/ZStack-x86_64-DVD-3.2.0-c74.iso
```

3. 需要下载最新的zstack-upgrade，您可以通过执行以下命令来进行下载:

```
$ wget http://cdn.zstack.io/product_downloads/scripts/zstack-upgrade
```

4. 需要到您的ISO路径下，执行以下命令升级iso:

```
$ sh zstack-upgrade -r ./ZStack-x86_64-DVD-3.2.0-c74.iso
```

## 第2步 - 更改ssh服务远程登录配置

1. 进入ssh目录

```
$ cd /etc/ssh
```

2. 更改sshd_config文件

```
$ vim sshd_config
把“PermitRootLogin no”的“no”改成“yes”后，保存退出
```

3. 重启sshd服务

```
$ service sshd restart
```

## 第3步 - 下载bin包完成安装

1. 创建/opt/zstack-dvd文件夹:

```
$ mkdir /opt/zstack-dvd
```

2. 下载ZStack-installer-3.2.0.bin包，您可以通过执行以下命令来下载bin包:

```
$ wget http://cdn.zstack.io/product_downloads/zstack-enterprise/enterprise3.2/ZStack-installer-3.2.0.bin
```

3. 需要到您的bin包路径下,通过执行以下命令来完成安装升级：

```
$ cd /home/dc2-user
$ bash ZStack-installer-3.2.0.bin -D
```
