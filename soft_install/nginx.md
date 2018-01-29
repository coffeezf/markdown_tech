# Nginx 安装配置

Nginx("engine x")是一款是由俄罗斯的程序设计师Igor Sysoev所开发高性能的 Web和 反向代理 服务器，也是一个 IMAP/POP3/SMTP 代理服务器。
在高连接并发的情况下，Nginx是Apache服务器不错的替代品。

------


## Nginx 安装

> 系统平台：CentOS release 6.6 (Final) 64位。


### 一、安装编译工具及库文件

```
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
```

### 二、首先要安装 PCRE

> PCRE 作用是让 Nginx 支持 Rewrite 功能。


1. 下载 PCRE 安装包，下载地址： http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz 

```
cd ~
wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
```

2. 安装

```
# 解压
tar zxvf pcre-8.35.tar.gz

cd pcre-8.35

# 编译安装
./configure
make && make install

```

3. 查看pcre版本

```
pcre-config --version
```

### 三、安装Nginx

1. 下载 Nginx，下载地址：http://nginx.org/download/nginx-1.9.9.tar.gz

```
cd ~
wget http://nginx.org/download/nginx-1.9.9.tar.gz
```

2. 安装

```
# 解压
tar zxvf nginx-1.9.9.tar.gz

cd nginx-1.9.9

# 编译安装
./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=~/pcre-8.35
make && make install

```

3. 查看nginx版本

```
/usr/local/webserver/nginx/sbin/nginx -v
```


到此，nginx安装完成。
