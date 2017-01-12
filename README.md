### Linux/macOS下为git协议设置代理

* 创建并编辑 ~/.socks5proxyssh文件 ，添加如下代码

```
#!/bin/sh  
ssh -o ProxyCommand="[用户目录的绝对路径].socks5proxywrapper %h %p" "$@"
```

* 创建并编辑~/.socks5proxyssh文件，添加如下代码，注意端口与自己使用的一致

```
#!/bin/sh  
connect -S 127.0.0.1:1080 "$@"
```

* 给这两个文件添加执行权限

```
chmod a+x ~/.socks5proxyssh  
chmod a+x ~/.socks5proxywrapper
```

* 编辑~/.gitconfig文件，添加代理配置

```
[http]  
    proxy = socks5://127.0.0.1:1080    
[https]
    proxy = socks5://127.0.0.1:1080  
# http协议直接走socks5代理      
[core]  
    gitproxy =[用户目录的绝对路径].socks5proxywrapper  
# git协议通过wrapper走代理
```

* 编译connect.c文件，并拷贝或链接到/usr/local/bin

```
gcc connect.c -o connect  
cp connect /usr/local/bin
```

版权说明： connect文件来自于[gotoh](https://bitbucket.org/gotoh/connect/src/ee1fbc21da4ba0c733ed9b8bb7e1eeece57fc75a/connect.c?at=default&fileviewer=file-view-default) 项目



