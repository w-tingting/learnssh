#  SSH远程连接工具

## 1. windows访问Linux虚拟机

[PuTTY](www.**putty**.org) 是一款免费的远程登录工具，使用==命令行==方式对服务器进行操作，支持SSH连接。

- 开启Linux端SSH服务

  1. 安装ssh服务器

  ```
  $ sudo apt-get install openssh-server
  ```

  2. 安装ssh服务器

  ```
  $ sudo apt-get install openssh-client
  ```

  3. 启动ssh服务

  启动：

  ```
  $ sudo /etc/init.d/ssh start
  ```

  确认：

  ```
  $ ps -e|grep ssh
  ```

- 设置虚拟机“网络适配器”

将“网络连接”方式设置为“桥接模式(B)”

- 获取Ubuntu的IP

命令行输入`ifconfig -a`

   ` inet addr`为网络IP地址：如192.168.1.8。

- windows使用PuTTY客户端登陆

  1. 在PuTTY配置界面输入主机IP地址
  2. 在弹出的窗口中输入Linux主机账户及密码

  ![1580955730887](D:\Typora project\1580955730887.png)


## 2.windows与Linux文件传输

username表示远程主机用户名，ip指远程主机ip地址 。

 [pscp](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)是putty安装包所带的远程文件传输工具 。pscp和scp功能相同，但pscp同时支持windows下使用，它有效解决了windows系统向linux服务器传输文件。

在Linux远程主机安装pscp：

```
sudo apt-get install putty-tools
```

1. windows向Linux传输文件/文件夹

在windows的DOS模式下，输入命令传输文件，具体如下：

- 传输文件

```
D:\Program Files\PuTTY>pscp 文件地址 username@ip:Linux地址
```

 例如：`pscp d:\1.txt tingting@192.168.1.8:/home/tingting `

- 传输文件夹

```
D:\Program Files\PuTTY>pscp -r 文件夹地址 username@ip:Linux地址
```

例如：`pscp -r d:\r tingting@192.168.1.8:/home/tingting`

2. 从服务器下载文件/文件夹

- 下载文件

```
D:\Program Files\PuTTY>pscp username@ip:文件地址（Linux） 本地目录（win）
```

例如： `pscp tingting@192.168.1.8:/home/tingting/timg.jpg d:\r`

- 下载文件夹

```
D:\Program Files\PuTTY>pscp -r username@ip:文件夹地址（Linux） 本地目录（win）
```

例如：`pscp -r tingting@192.168.1.8:/home/tingting/Downloads d:\r`

## 3. Linux登陆Linux远程主机与文件传输

命令：

```
ssh username@ip
```

或者：

```
ssh username@ip -p 端口号
```

- 文件传输

 在linux中，我们常用scp命令传输文件， username表示远程主机用户名，ip指远程主机ip地址 ： 

1. 从服务器下载文件

```
scp username@ip:/path/filename /var/www/local_dir（本地目录）
```

例如： scp tingting@192.168.1.8:/home/tingting/test.txt  /home/xxx

2. 上传本地文件到服务器

```
scp /path/filename username@ip:/path
```

3. 从服务器下载整个目录

```
scp -r username@ip:/var/www/remote_dir/（远程目录） /var/www/local_dir（本地目录）
```

4. 上传目录到服务器

``` 
scp -r local_dir username@ip:remote_dir
```

- 文件增量传输方式rsync
1. 从服务器下载到客户端
```
rsync -avzhP --process tingting@192.168.1.8:/home/tingting/1.txt /home/Ubuntu
```
其中，`-a`能正确处理软链接，`-v`显示同步过程的详细(verbose)信息，`-z`表示压缩传输，`-h`表示可读(human-readable)，`-P`表示断点续传；--process表示显示进度。

2. 上传到服务器:
```
rsync -avzhP --process /home/Ubuntu/1.txt tingting@192.168.1.8:/home/tingting
```
命令提示查询工具：cheat.sh
```
curl cheat.sh/<命令名称>
```
