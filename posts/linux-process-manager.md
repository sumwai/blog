---
title: Linux进程管理
date: 2022-04-07T15:36:00+08:00
draft: true
---

#### 制造系统卡顿


> 计算圆周率，小数点后100位


```
echo \"scale=100; a(1)*4\" | bc -l
```


### 查看系统进程信息


```
top
```
>
> Tips: 按 `1` 显示所有CPU占用信息
>



>
> top - 15:22:41 up 5 days,  1:46,  2 users,  `load average`: `1.06`, 0.98, 0.61
>
> Tasks: 142 total,   3 running, 138 sleeping,   0 stopped,   1 zombie
>
> %Cpu(s): `52.4 us`,  1.0 sy,  0.0 ni, `46.6 id`,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
> 
> KiB Mem :  `3880128 total`,  2391088 free,   724104 used,   764936 buff/cache
> 
> KiB Swap:  4063228 total,  4057528 free,     5700 used.  `2909112 avail Mem`
>
>  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
>
> 11288 root      20   0   14900   2632    684 R 100.0  0.1   9:49.62 bc


```
CPU使用率: 100 - 46.6 (id) = 53.4%
内存使用率: [3880128 (total) - 2909112 (avail Mem)] / 3880128 (total) = 25%
系统负载: 1.06 / 2 (cpu number) = 53%
系统负载: 当前负载 / CPU总数
```


### 查看进程详情


```
ps aux | grep bc
```


> root     `11288` 99.9  0.0  14900  2632 pts/0    R+   15:10  20:31 bc -l
> root     `12582`  0.0  0.0 112812   944 pts/1    S+   15:31   0:00 grep --color=auto bc


> **酌情选择是否需要停止该进程**


### 查询进程与端口


- 查询进程端口

    > tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      965/sshd

    ```
    # netstat -anp | grep [进程]
    netstat -anp | grep sshd
    ```

- 查询端口进程

    > tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      965/sshd

    ```
    # netstat -anp | grep -w 端口号
    netstat -anp | grep -w 22
    ```

### 停止进程

- 停止所有

    ```
    # killall [进程命令]
    killall bc
    ```

- 停止指定进程

    ```
    # kill [进程ID]
    kill 11288
    ```

### 后台进程（任务）

- 启动任务

    ```
    nohup httpd -DFOREGROUND &
    ```

- 查看任务列表

    ```
    jobs
    ```
  
### 前后台任务切换

- 启动一个前台任务

  ```
  httpd -DFOREGROUND
  ```

- 挂起任务

    > 快捷键: <kbd>Ctrl</kbd> + <kbd>z</kbd>
    > **当任务挂起后，`jobs` 查看的任务状态为`已停止`**

- 后台运行任务

  ```
  # bg [任务id]
  bg 1
  ```
  ```
  [1]+ httpd -DFOREGROUND &
  ```
  
- 前台运行任务

  ```
  # fg [任务ID]
  fg 1
  ```
  ```
  httpd -DFOREGROUND
  ```