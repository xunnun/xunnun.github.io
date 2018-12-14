---
title: Linux安装zsh
date: 2018-12-14 11:41:17
categories: 环境配置
tags:
 - Centos
 - zsh
---

Linux 安装zsh

<!--more-->

# 添加第三方源
```
sudo yum install epel-release
sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
```
# 安装zsh

如果你用 Redhat Linux，执行:
```
sudo yum install -y zsh
```
如果你用 Ubuntu Linux，执行:
```
sudo apt-get install zsh
```
# 安装oh my zsh

自动安装:
```
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```
手动安装:
```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

# 更改默认shell

```
chsh -s /bin/zsh
```
# 安装插件
```
git clone git://github.com/joelthelion/autojump.git
cd autojump
./install.py
yum install autojump-zsh -y
vi  ~/.zshrc
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
plugins=(git autojump )
```

