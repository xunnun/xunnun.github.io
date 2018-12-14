---
title: Centos7 配置shadowsocks
date: 2018-12-14 16:36:30
categories: 软件配置
tags:
  - Centos
  - 科学上网
  - shadowsocks
---
在 CentOS 7 下安装配置 shadowsocks
<!--more-->

# 服务端配置

## 安装 pip

```
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
```

## 安装shadowsocks

```
pip install --upgrade pip
pip install shadowsocks
```

## 编辑配置文件

创建配置文件 /etc/shadowsocks.json
```
{
  "server":"my_server_ip",
  "local_address": "127.0.0.1",
  "local_port":1080,
  "port_password":{
        "4433":"mypassword",
        "4434":"mypassword"
        },
  "timeout":300,
  "method":"aes-256-cfb",
  "fast_open": false
}
```
## 启动

```
ssserver -c /etc/shadowsocks.json

To run in the background:

ssserver -c /etc/shadowsocks.json -d start
ssserver -c /etc/shadowsocks.json -d stop
```

## 开机自启

/etc/systemd/system/shadowsocks.service
```
[Unit]
Description=Shadowsocks
After=network.target

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json
User=nobody
Group=nobody
LimitNOFILE=32768

[Install]
WantedBy=multi-user.target
```

启动服务
```
systemctl enable shadowsocks
systemctl start shadowsocks
```
## 日志查看

```
less /var/log/shadowsocks.log
journalctl -u shadowsocks.service -f |tee /var/log/shadowsocks.log
```

# 客户端配置

前面都一样，下载安装shadowsocks

## 创建配置文件

/etc/shadowsocks.json

```
{
  "server":"my_server_ip",
  "local_address": "127.0.0.1",
  "local_port":1080,
  "server_port":my_server_port,
  "password":"my_password",
  "timeout":300,
  "method":"aes-256-cfb"
}
```
## 启动

```
前端启动：sslocal -c /etc/shadowsocks.json；
后端启动：sslocal -c /etc/shadowsocks.json -d start；
后端停止：sslocal -c /etc/shadowsocks.json -d stop；
重启(修改配置要重启才生效)：sslocal -c /etc/shadowsocks.json -d restart
```

##开机自启

/etc/systemd/system/shadowsocks.service

```
[Unit]
Description=Shadowsocks Client Service
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/bin/sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json

[Install]
WantedBy=multi-user.target
```
启动服务

```
systemctl enable shadowsocks
systemctl start shadowsocks
```
