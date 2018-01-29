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

### 四、Nginx配置

1. 创建 Nginx 运行使用的用户 www：
```
/usr/sbin/groupadd www
/usr/sbin/useradd -g www www
```

2. 配置nginx.conf,将Nginx配置/usr/local/webserver/nginx/conf/nginx.conf改为如下：
```
user www www;
worker_processes 4; #设置值和CPU核心数一致
error_log /usr/local/webserver/nginx/logs/nginx_error.log crit; #日志位置和日志级别
pid /usr/local/webserver/nginx/nginx.pid;
#Specifies the value for maximum file descriptors that can be opened by this process.
worker_rlimit_nofile 65535;
events
{
    use epoll;
    worker_connections 65535;
}
http
{
    include mime.types;
    default_type application/octet-stream;
    log_format main  '$remote_addr - $remote_user [$time_local] "$request" '
               '$status $body_bytes_sent "$http_referer" '
               '"$http_user_agent" $http_x_forwarded_for';

    #charset gb2312;

    server_names_hash_bucket_size 128;
    client_header_buffer_size 32k;
    large_client_header_buffers 4 32k;
    client_max_body_size 8m;

    sendfile on;
    tcp_nopush on;
    keepalive_timeout 60;
    tcp_nodelay on;
    fastcgi_connect_timeout 300;
    fastcgi_send_timeout 300;
    fastcgi_read_timeout 300;
    fastcgi_buffer_size 64k;
    fastcgi_buffers 4 64k;
    fastcgi_busy_buffers_size 128k;
    fastcgi_temp_file_write_size 128k;
    gzip on;
    gzip_min_length 1k;
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 2;
    gzip_types text/plain application/x-javascript text/css application/xml;
    gzip_vary on;

    #limit_zone crawler $binary_remote_addr 10m;
    #下面是server虚拟主机的配置
    server
    {
        listen 80;#监听端口
        server_name localhost;#域名
        index index.html index.htm index.php;
        root /usr/local/webserver/nginx/html;#站点目录
        location ~ .*\.(php|php5)?$
        {
            #fastcgi_pass unix:/tmp/php-cgi.sock;
            fastcgi_pass 127.0.0.1:9000;
            fastcgi_index index.php;
            include fastcgi.conf;
        }
        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|ico)$
        {
            expires 30d;
            #access_log off;
        }
        location ~ .*\.(js|css)?$
        {
            expires 15d;
            #access_log off;
        }
        access_log off;
    }
}
```

3. 检查配置文件ngnix.conf的正确性命令
```
/usr/local/webserver/nginx/sbin/nginx -t
```

### 五、启动Nginx

1. 启动Nginx命令
```
/usr/local/webserver/nginx/sbin/nginx
```
访问站点：http://192.168.0.1

2. Nginx其他命令
```
/usr/local/webserver/nginx/sbin/nginx -s reload            # 重新载入配置文件
/usr/local/webserver/nginx/sbin/nginx -s reopen            # 重启 Nginx
/usr/local/webserver/nginx/sbin/nginx -s stop              # 停止 Nginx
```
