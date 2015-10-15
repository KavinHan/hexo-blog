title: 阿里云(ECS) CentOS 上安装Nginx和Vsftpd
tags: 阿里云
---

## 阿里云环境
- OS: CentOS 7.0 64位
- Nginx: 1.6.3
- Vsftpd: 3.0.2

## 安装Nginx

```
$> yum install epel-release
$> yum install Nginx
$> systemctl start nginx
```
在浏览器访问你的ECS的公网IP能看见Nginx运行正常。

## 配置Nginx虚拟主机
这里有个坑。。。
### 创建虚拟主机目录

### 在虚拟主机目录创建index.html

### 创建配置文件

### 激活配置文件

## 安装与配置Vsftpd





## 参考
- https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7
- https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-on-centos-7
- http://segmentfault.com/q/1010000000510752
- http://www.cnblogs.com/dudu/archive/2012/12/15/linux-ftp-vsftpd.html
