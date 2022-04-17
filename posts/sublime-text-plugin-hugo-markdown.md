---
title: Hugo markdown Sublime Text 插件
date: 2022-04-17T16:22:08+08:00
draft: true
---

#### 需求

由于博客是使用`caddy` + `hugo` 部署在服务器上的，但是写博客一般是在本地操作。

有个非常不方便的点就是：在服务器上可以使用`hugo new xxx.md`创建文章，文章会包含一个标题及时间，如下
```
---
title: Hugo markdown Sublime Text 插件
date: 2022-04-17T16:22:08+08:00
draft: true
---
```
在正常的本地编辑时，几乎不太可能随时去看时间，所以这是一个很麻烦的点。

因为我当前使用的SublimeText编辑器，所以写了一个小插件去解决这个问题。

不过因为是第一次开发，所以肯定需要上百度找找资料啦

#### 借鉴文章

- [Sublime Text 插件开发流程][https://www.jianshu.com/p/e2558ee1d503]
- [Python 日期和时间][https://www.runoob.com/python/python-date-time.html]
- [sublime text 插件 -- 获取文件名到剪贴板][https://www.likecs.com/show-204661998.html]
- [Python 字符串分割的方法][https://www.cnblogs.com/ShaunChen/p/6201129.html]


#### 插件代码

```
import sublime
import sublime_plugin
import time
from datetime import date

class BlogCommand(sublime_plugin.TextCommand):
	def run(self, edit):
		# 获取当前文件路径并且使用\\分割
		filepatharr = self.view.file_name().split("\\")
		# 获取当前时间戳，转为 2022-04-17T16:22:08+08:00 格式
		# Tips: 如果你的时区不是+08:00，需要自行修改。
		timeNow = time.strftime("%Y-%m-%dT%H:%M:%S+08:00", time.localtime())
		# 插入到页面开头
		self.view.insert(edit, 0, "---\ntitle: "+filepatharr[-1][:-3]+"\ndate: "+timeNow+"\ndraft: true\n---\n\n")
```

#### 快捷键绑定

```
[
	{
		"keys": ["ctrl+shift+b"],
		"command": "blog"
	}
]
```

#### 结束

以上就是为Hugo Markdown写的一个小插件，可以在文件开头插入`标题`、`时间`标记，可以快乐的写博客啦。