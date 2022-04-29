---
title: Shell Sed
date: 2022-04-29T16:57:13+08:00
draft: true
---


### Replace

> sed 's/[Regex]/[Replace]/g' 

```shell
echo "aaa/bbb/ccc////" | sed 's/\/*$//g'
```

