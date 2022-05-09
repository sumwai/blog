---
title: Archlinux 安装输入法
date: 2022-05-09T21:50:30+08:00
draft: true
---

### 安装输入法

#### 搜狗输入法

```shell
yay -S fcitx-sogoupinyin
```

### 安装fcitx配置工具

```shell
yay -S fcitx-configtool
```

### 配置环境变量

```shell
echo export GTK_IM_MODULE=fcitx >> .xprofile 
echo export QT_IM_MODULE=fcitx >> .xprofile
echo export XMODIFIERS="@im=fcitx" >> .xprofile
```

### 设置输入法开机自启动

#### i3wm

```config
exec --no-startup-id "fcitx"
```

### 重启

```shell
systemctl reboot
```
