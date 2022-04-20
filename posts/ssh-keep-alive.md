---
title: SSH保持连接
date: 2022-04-20T13:37:44+08:00
draft: true
---

SSH连接长时间不操作的话会自动断开，此时终端会卡在之前的状态无法操作，可以使用配置文件来解决这个问题。有两种方式，分别是客户端配置和服务端配置。而对于开发人员来说，经常有多个服务器需要在一台机器上连接，所以推荐是配置在客户端，这样就不需要每次连接服务器都要配置。

### 客户端配置

配置文件: `~/.ssh/config`

```
Host *
	ServerAliveInterval 40
```

其中  `Host *` 这一项是配置所有主机，也可以使用`Host 主机名`对于不同主机配置不同的参数

```
Host aaa.com
	ServerAliveInterval 40
Host bbb.com
	ServerAliveInterval 10
```

`ServerAliveInterval`是指向服务器发送心跳包的间隔时间（秒），可以按自己的想法配置。