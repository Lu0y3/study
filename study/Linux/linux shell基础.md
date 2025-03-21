[TOC]

# Linux 常用命令

Linux的命令有几百个，对程序员来说，常用的并不多，并不需要全部掌握。如果在学习和工作中遇到了陌生的Linux命令，不要轻易放过，多查资料，掌握它，日积月累，知识面就会宽广。  
本文介绍的是Linux的常用命令，对初学者来说，建议系统化的学习Linux基础知识。

## 推荐视频
[视频链接](https://www.bilibili.com/video/av18156598)  

## 1. 开机
- 物理机服务器：按下电源开关，就像Windows开机一样。
- 本地虚拟机：在VMware中点击“开启此虚拟机”。

## 2. 登录
启动完成后，输入用户名和密码，一般情况下，不要用root用户登录，root用户的权限太大，如果产生了误操作，后果相当严重。

## 3. 切换用户
在命令提示符下输入：  
`su - root`  
然后按提示输入root的密码后将切换到root用户。  
从root用户切换到其它普通用户不需要输入密码，从普通用户切换到任何用户都需要输入密码。

## 4. 重启和关机
重启和关机需要系统管理员用户权限。

### 1）重启
- `init 6` 或 `reboot`

### 2）关机
- `init 0` 或 `halt`

如果没有执行关机命令，强制断电或关闭本地虚拟机的窗口，会导致Linux操作系统文件的损坏，严重的可能导致系统无法正常启动。

## 5. 清屏
- `clear`  
清除当前屏幕上显示的内容。

## 6. 查看服务器的IP地址
- `ifconfig`

上图中，框中显示的就是IP地址。

## 7. 时间操作
普通用户可以查看时间，但设置时区和时间要系统管理员用户登录。

### 1）查看时间
- `date`

### 2）设置时区为中国上海时间
- `cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`

### 3）设置时间
- `date -s "yyyy-mm-dd hh:mi:ss"`

例如：
- `date -s "2020-01-02 12:35:28"`

### 4）把操作系统的时间写入CMOS
- `clock -w`

## 8. 目录和文件
文件系统是像一棵树，树干是`/`（根）目录，树枝是子目录，树枝后面还有树枝（子目录中还有子目录），树枝最后是树叶，目录的最后是文件。

严谨的说，文件名是由目录+文件名组成的。

对于目录和文件，有一些约定的表述，我们以`/usr/etc/readme.txt`为例：

1）全路径文件名包含了完整的目录名和文件名，即`/usr/etc/readme.txt`，还有一个称呼是“绝对路径文件名”。

2）`readme.txt`是文件名，它在`/usr/etc`目录中。

3）目录和文件的绝对路径是从根（`/`）算起，在任何时候都不会有歧义。

4）登录Linux后，一定处在目录树的某个目录中，这个目录称之为当前工作目录，简称当前目录。

5）目录和文件的相对路径是从当前目录算起，如果当前目录是`/usr`，`etc/readme.txt`等同于`/usr/etc/readme.txt`；如果当前目录是`/usr/etc`，`readme.txt`等同于`/usr/etc/readme.txt`。

6）用Linux的命令操作目录和文件的时候，采用绝对路径和相对路径都可以。

7）一个圆点`.`表示当前目录。

8）两个圆点`..`表示当前目录的上一级目录。

理解绝对路径和相对路径的概念非常重要，在日常操作中，绝对路径和相对路径会同时使用，但是程序员在编写的程序中极少使用相对路径。

## 9. 正则表达式
正则表达式又称规则表达式、通配符，目录和文件名都支持正则表达式，正则表达式的规则比较多，在这里我只介绍最常用的两种：星号“*”和问号“?”。

- 星号`*`：匹配任意数量的字符。
- 问号`?`：匹配一个字符。

示例：

当前目录下有以下几个文件：
- `book15`
- `book15.c`
- `book1.c`
- `book5.c`
- `makefile`

1）列出全部的文件：
- `ls`

2）列出文件名以`book`打头，`.c`结尾，中间可以是任意数量的字符的文件：
- `ls book*.c`

3）列出文件名以`book`打头，`.c`结尾，中间只能有一个字符的文件：
- `ls book?.c`

## 10. 查看当前目录
- `pwd`

## 11. 改变当前目录
- `cd 目录名`

示例：

1）进入`/tmp`目录：
   - `cd /tmp`

2）进入上一级目录：
   - `cd ..`

3）进入用户的主目录：
   - `cd`

## 12. 列出目录和文件信息
- `ls [-lt] 目录或文件名`

`ls`是list的缩写，通过`ls`命令不仅可以查看目录和文件信息，还可以查看目录和文件的权限、大小、主人和组等信息。

选项：
- `-l`列出目录和文件的详细信息。
- `-lt`列出目录和文件的详细信息，按时间降序显示。

示例：

1）列出当前目录下全部的目录和文件信息：
   - `ls`

2）列出当前目录下全部的目录和文件的详细信息：
   - `ls -l`

3）列出`/tmp`目录下全部的目录和文件：
   - `ls /tmp`

4）列出`/tmp`目录下以匹配`exp*.dmp`的目录和文件：
   - `ls /tmp/exp*.dmp`

5）列出`/tmp`目录下匹配`*.log`的目录和文件，按时间降序显示：
   - `ls /tmp/*.log`

## 13. 创建目录
- `mkdir 目录名`

示例：

1）在当前目录下创建`aaa`目录：
   - `mkdir aaa`

2）在当前目录的`aaa`目录下创建`bbb`目录：
   - `mkdir aaa/bbb`

3）创建`/tmp/aaa`目录：
   - `mkdir /tmp/aaa`

## 14. 删除目录和文件
- `rm [-rf] 目录或文件列表`

选项：
- `-r`可以删除目录，如果没有`-r`只能删除文件。
- `-f`表示强制删除，不需要确认。

目录和文件列表中间用空格分隔。

示例：

1）删除当前目录下匹配`*.log`的文件：
   - `rm *.log`

2）强制删除当前目录下匹配`*.log`的文件：
   - `rm -f *.log`

3）删除`/tmp/aaa`目录和文件：
   - `rm -r /tmp/aaa`

4）强制删除`/tmp`目录下匹配`exp*`的全部目录和文件：
   - `rm -rf /tmp/exp*`

5）强制删除当前目录下的`book`和`book.c`文件：
   - `rm -rf book book.c`

## 15. 移动目录和文件
- `mv 旧目录或文件名 新目录或文件名`

如果第二个参数是已经存在的目录，则把第一个参数（旧目录或文件名）移动到该目录中。

示例：

1）把当前目录中的`book.c`文件重命名为`book1.c`：
   - `mv book.c book1.c`

2）如果`/tmp/test3`是一个已经存在的目录，以下命令将把当前目录下的`book.c`文件移动到`/tmp/test3`目录中：
   - `mv book.c /tmp/test3`

3）如果`/tmp/test3`目录不存在，以下命令将把当前目录下的`book.c`文件改名为`/tmp/test3`：
   - `mv book.c /tmp/test3`

## 16. 复制目录和文件
- `cp [-r] 旧目录或文件名 新目录或文件名`

选项：
- `-r`可以复制目录，如果没有选项`-r`只能复制文件。

示例：

1）把当前目录下的`book1.c`文件复制为`book2.c`：
   - `cp book1.c book2.c`

2）把当前目录下的`aaa`目录复制为`bbb`：
   - `cp -r aaa bbb`

3）把当前目录下的`book1.c`文件复制为`/tmp/book1.c`：
   - `cp book1.c /tmp/book1.c`

4）把当前目录下的`aaa`目录复制为`/tmp/aaa`：
   - `cp -r aaa /tmp/aaa`

## 17. 修改用户的密码
- `passwd [用户名]`

普通用户只能修改自己的密码，只输入`passwd`就可以了，不能指定用户名。  
系统管理员可以修改任何用户的密码，`passwd`后需要指定用户名。

## 18. 打包压缩和解包解压
`tar`命令用来打包压缩和解包解压文件，类似Windows的WinRAR工具。

### 打包压缩
- `tar zcvf 压缩包文件名 目录或文件名列表`

示例：
- `tar zcvf 123.tgz aaa bbb ccc`

### 解包解压
- `tar zxvf 压缩包文件名`

示例：
- `tar zxvf /tmp/123.tgz`
![解包](/images/Linux/解包.png)

## 19. 判断网络是否连通
- `ping -c 包的个数 ip地址或域名`

示例：
1）向本地主机（127.0.0.1）ping五个包：
   - `ping -c 5 127.0.0.1`

2）向新浪的服务器（www.sina.com.cn）ping五个包：
   - `ping -c 5 www.sina.com.cn`

## 20. 显示文本文件的内容
- `cat 文件名`
- `more 文件名`
- `tail -f 文件名`

## 21. 统计文本文件的行数、单词数和字节数
- `wc 文件名`

示例：
- `wc book2*.c`

## 22. 搜索文件中的内容
- `grep "内容" 文件名`

示例：
- `grep max *.c`

## 23. 搜索文件
- `find 目录名 -name 文件名 -print`

示例：
1）从`/tmp`目录开始搜索，把全部的`*.c`文件显示出来：
   - `find /tmp -name *.c -print`

## 24. 增加/删除用户组
- `groupadd 组名`
- `groupdel 组名`

示例：
- `groupadd dba`
- `groupdel dba`

## 25. 增加/删除用户
- `useradd -n 用户名 -g 组名 -d 用户的主目录`
- `userdel 用户名`

示例：
- `useradd -n wucz -g dba -d /home/wucz`
- `userdel wucz`

## 26. 修改目录和文件的主人和组
- `chown [-R] 用户名:组名 目录或文件名列表`

示例：
- `chown -R oracle:dba /oracle/home /oracle/base`

## 27. 查看系统磁盘空间
- `df [-h] [-T]`

选项：
- `-h` 以方便阅读的方式显示信息。
- `-T` 列出文件系统类型。

示例：
- `df -h`
