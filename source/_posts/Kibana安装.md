# Kibana安装

> 本文环境
> centos 7
> kibana 7.4

## 安装

- 下载rpm包
```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.4.0-x86_64.rpm

```

- 安装
```bash
sudo rpm --install kibana-7.4.0-x86_64.rpm
```

- 设置开机自动启动
```bash
systemctl daemon-reload

systemctl enable kibana.service
```

- 启动/停止
```bash
systemctl start kibana

systemctl stop kibana
```

> home目录：/usr/share/kibana
> 配置目录：/etc/kibana
> data目录：/var/lib/kibana
> logs目录：/var/log/kibana

## 配置

- 配置监听IP地址，端口，ES地址

```bash

```

- 开发防火墙
```bash
firewall-cmd --zone=public --add-port=5601/tcp --permanent

firewall-cmd --complete-reload
```
