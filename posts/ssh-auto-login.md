---
title: SSH自动登录
date: 2022-04-20T14:43:10+08:00
draft: true
---

对于某些懒人（我），在ssh登录服务器时，懒得输入密码，可以使用公钥验证，只需要在服务器配置允许公钥认证，然后在本地生成公钥，再上传到服务器，就可以一劳永逸了。

### 允许密钥认证

```bash
vim /etc/ssh/sshd_config
```

只需要取消注释以下两个参数即可

```ini
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```
其中`PubkeyAuthentication`选项允许公钥认证，`AuthorizedKeysFile`选项指定公钥认证文件。

### 本地生成公钥

```bash
ssh-keygen
```
输入之后一路回车确认即可，此命令将在本地`~/.ssh/`目录下生成`id_rsa`, `id_rsa.pub`文件，而`id_rsa.pub`就是配置所需要的文件

### 配置服务器公钥

> 在首次配置公钥时，可以直接使用以下命令，同时输入服务器密码，等待文件上传完成，就可以使用`ssh`免密码登录了。

#### linux

```bash 
scp ~/.ssh/id_rsa.pub root@aaa.com:/root/.ssh/authorized_keys
```

#### windows

> Windows操作首先需要进入用户主目录，即`C:\Users\[用户名]`，再使用以下命令即可

```bash
scp .\.ssh\id_rsa.pub root@sumwai.cn:/root/.ssh/authorized_keys
```

### 配置完成

当公钥文件上传完成之后，即可使用`ssh root@aaa.com`登录服务器了，无需密码认证，简直懒人福音。