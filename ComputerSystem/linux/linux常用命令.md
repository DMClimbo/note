## source命令

- 用法：source FileName

- 作用：在当前bash环境下读取并执行文件中的命令，通常用于重新执行刚修改的初始化文档，如.bash_profile和.profile等等，**可以把一个文件的内容当做shell来执行**

- source filename 与 sh filename 及./filename执行脚本的区别

  1. 当shell脚本具有可执行权限时，用`sh filename`与`./filename`执行脚本是没有区别得。`./filename`是因为当前目录没有在PATH中，所有”.”是用来表示当前目录的。
  2. `sh filename` 重新建立一个子shell，在子shell中执行脚本里面的语句，该子shell继承父shell的环境变量，但子shell新建的、改变的变量不会被带回父shell，除非使用export。
  3. `source filename`：这个命令其实只是简单地读取脚本里面的语句依次在当前shell里面执行，没有建立新的子shell。那么脚本里面所有新建、改变变量的语句都会保存在当前shell里面。

  

  

  

## man命令

- 语法：man -参数  title

- 作用：man命令是linux下的帮助指令，通过man可以查看Linux中的指令帮助、配置文件帮助和编程帮助等信息。

- 参数：

  | -a      | 显示所有匹配项                                               |
  | ------- | ------------------------------------------------------------ |
  | -d      | 显示man查照手册文件时候，搜索路径信息,不显示手册页内容       |
  | -D      | 同-d,显示手册页内容                                          |
  | -f      | 同命令whatis ，将在whatis数据库查找以关键字开同的帮助索引信息 |
  | -h      | 显示帮助信息                                                 |
  | -k      | 同命令apropos 将搜索whatis数据库，模糊查找关键字             |
  | -S list | 指定搜索的领域及顺序 如：-S 1:1p httpd 将搜索man1然后 man1p目录 |
  | -t      | 使用troff 命令格式化输出手册页 默认：groff输出格式页         |
  | -w      | 不带搜索title 打印manpath变量 带title关键字 打印找到手册文件路径,默认搜索一个文件后停止 |
  | -W      | 同-w                                                         |
  | section | 搜索领域【限定手册类型】默认查找所有手册                     |



​	

## curl命令

curl 是常用的命令行工具，用来请求 Web 服务器。它的名字就是客户端（client）的 URL 工具的意思。

它的功能非常强大，命令行参数多达几十种。如果熟练的话，完全可以取代 Postman 这一类的图形界面工具。

​	

不带有任何参数时，curl 就是发出 GET 请求。

```bash
$ curl https://www.example.com
```

上面命令向`www.example.com`发出 GET 请求，服务器返回的内容会在命令行输出。



[常用参数](http://www.ruanyifeng.com/blog/2019/09/curl-reference.html)