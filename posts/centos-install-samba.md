---
title: Centos安装Samba服务
---

#### Samba端口号

- 139
- 445

#### 安装


```
shell
sudo yum -y install samba
```


#### 配置


```
shell
sudo vim /etc/samba/smb.conf
```


```
# See smb.conf.example for a more detailed config file or
# read the smb.conf manpage.
# Run \'testparm\' to verify the config is correct after
# you modified it.

[global]
	workgroup = SAMBA
	security = user
    interfaces = eth0
	passdb backend = tdbsam

	printing = cups
	printcap name = cups
	load printers = yes
	cups options = raw

[homes]
	comment = Home Directories
	valid users = %S, %D%w%S
	browseable = No
	read only = No
	inherit acls = Yes

[printers]
	comment = All Printers
	path = /var/tmp
	printable = Yes
	create mask = 0600
	browseable = No

[print$]
	comment = Printer Drivers
	path = /var/lib/samba/drivers
	write list = @printadmin root
	force group = @printadmin
	create mask = 0664
	directory mask = 0775
[wwwroot]
	valid users = www
    force user = www
    force group = www
    create mask = 0755
    directory mask = 0755
    available = yes
    comment = share all
    path = /www/wwwroot
    browseable = yes
    public = yes
    writable = yes
```


#### 配置登录密码

```
sudo smbpasswd -a www
```



#### 关闭SElinux


```
bash
sudo setenforce 0
```


#### 关闭防火墙

```
bash
sudo systemctl stop firewalld
```


#### 测试配置文件

```
bash
sudo testparm -s
```



```
Load smb config files from /etc/samba/smb.conf
Loaded services file OK.
Server role: ROLE_STANDALONE

# Global parameters
[global]
        interfaces = eth0
        printcap name = cups
        security = USER
        workgroup = SAMBA
        idmap config * : backend = tdb
        cups options = raw


[homes]
        browseable = No
        comment = Home Directories
        inherit acls = Yes
        read only = No
        valid users = %S %D%w%S


[printers]
        browseable = No
        comment = All Printers
        create mask = 0600
        path = /var/tmp
        printable = Yes


[print$]
        comment = Printer Drivers
        create mask = 0664
        directory mask = 0775
        force group = @printadmin
        path = /var/lib/samba/drivers
        write list = @printadmin root


[wwwroot]
        comment = share all
        create mask = 0755
        force group = www
        force user = www
        guest ok = Yes
        path = /www/wwwroot
        read only = No
        valid users = www
```



#### 启动Samba服务

```
bash
sudo systemctl start smb
```


#### 重启服务

```
bash
sudo systemctl restart smb
```


#### 设置开机自启


```
bash
sudo systemctl enable smb
```


#### Windows挂载

<kbd>文件管理器</kbd> -> 右键点击<kbd>网络</kbd> -> <kbd>映射网络驱动器</kbd> -> 输入<kbd>\\\\192.168.1.150\\wwwroot</kbd> -> 完成

> 当弹出账号密码时，输入账号：www，密码：**使用 `smbpasswd` 设置的密码**
