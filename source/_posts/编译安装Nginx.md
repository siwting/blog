---
title: 编译安装Nginx
date: 2019-10-22 14:36:36
tags: 
    - Nginx
    - 配置
    - 程序安装
categories: 运维
keywords: nginx
---


> 本文环境：centos 7    nginx 1.16.0

## 安装OpenSSL

```bash
yum -y install openssl openssl-devel
```

## 下载Nginx

```bash
wget http://nginx.org/download/nginx-1.16.0.tar.gz
```

## 解压Nginx

```bash
tar -xzf nginx-1.16.0.tar.gz
```

## 编译Nginx

```bash
cd nginx-1.16.0
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module  --with-http_realip_module --with-stream --with-stream_ssl_module --with-stream_realip_module --with-openssl=/usr/local/openssl

make
```

 - 出现错误 `./configure: error: C compiler cc is not found`

```bash
sudo yum  -y install gcc
```

- 出现错误：`./configure: error: the HTTP rewrite module requires the PCRE library.`

```bash
sudo yum install pcre-devel
```

- 出现错误：`./configure: error: the HTTP gzip module requires the zlib library.`

```bash
sudo yum install zlib-devel
```


## 安装Nginx

```bash
make install
```

## 配置Nginx服务

```bash
vi /usr/lib/systemd/system/nginx.service


[Unit]
Description=nginx
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s stop
ExecQuit=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true

[Install]
WantedBy=multi-user.target

```

## 启动Nginx

```bash
systemctl enable nginx.service
systemctl daemon-reload
systemctl start nginx
```

## 安装Certbot

```bash
yum install -y epel-release

yum install certbot python2-certbot-nginx
```

## 配置SSL

```bash
certbot --nginx --nginx-server-root /usr/local/nginx/conf --nginx-ctl /usr/local/nginx/sbin/nginx
```
