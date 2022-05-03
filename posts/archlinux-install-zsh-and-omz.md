---
title: archlinux安装zsh及ohmyzsh
date: 2022-05-03T15:34:44+08:00
draft: true
---

### 准备

在安装之前，需要预先准备安装`git`, 如果是国内的用户（指访问不了github的用户），需要配置 ghproxy 镜像（用于安装ohmyzsh和ohmyzsh插件）

#### 安装 Git

```shell
pacman -Syy git
```

#### 配置ghproxy镜像

```shell
git config --global url."https://ghproxy.com/https://github.com/".insteadOf "https://github.com/"
```

### 安装 zsh 与 ohmyzsh

#### zsh

> 安装
```shell
pacman -Syy zsh
```

> 配置默认shell

```shell
chsh -s `which zsh`
```

#### ohmyzsh

> 官网: [ohmyz.sh](https://ohmyz.sh/)

> 官网指出的下载地址为`raw.github.com`， 对于可以访问github的用户，可以直接执行这个命令
```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
> 对于不能访问github的用户，将其更换为`ghproxy`镜像下载

```shell
sh -c "$(curl -fsSL https://ghproxy.com/https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### ohmyzsh 插件


#### 插件安装方式

将插件下载到`~/.oh-my-zsh/custom/plugins`目录下，并修改`~/.zshrc`中的`plugins`项，重载`zshrc`文件即可（`source ~/.zshrc`）

插件可以在github上查找, 推荐`zsh-users`的[仓库](https://github.com/zsh-users), 以下推荐两个比较好用的插件

#### zsh-autosuggestions

该插件的作用是自动补全，它会读取你的历史操作并在你下次输入命令时给与补全。
Github: [zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
安装: [INSTALL.md#oh-my-zsh](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

#### zsh-syntax-highlighting

顾名思义，这个就是zsh的语法高亮插件，其会高亮命令，可以一眼就看出来命令是否敲对。安装方式基本同上

Github: [zsh-users/zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
安装: [INSTALL.md#oh-my-zsh](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh)
