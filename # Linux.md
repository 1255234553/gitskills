# Linux

bandit.labs.overthewire.org，端口为 2220



连接服务器：ssh '用户名'@'服务器名地址' -p '端口号'
- 指定端口添加-p 端口号
- 输入密码
- 登出：logout；exit

连接时就把参数带进去：ssh bandit18@localhost cat readme

#### 命令

- ls:列出当前目录中的所有文件和文件夹。
- ls-l:将列出目录的内容以及其他信息，例如大小、权限和日期。
- ls-a :列出所有内容，包括隐藏文件和文件夹。

---

- cd..:移动到上一个目录
- cd<directoryname> :会将您移动到指定的子目录。
- cd /home/directory/path/ :会将您从根目录（主目录）移至指定目录。
- cd ~: 将使您返回到您的 HOME 目录。

---

- mkdir<directoryname>:创建目录
- cat <filename>:知道内容
- pwd:显示当前的目录位置
- who:谁登陆到系统
- vi a.txt:创建一个新文件并打开文件编辑器

---

**通过shell复制文件**
- cp example1.txt example2.txt 将在同一位置创建一个名为 example2.txt 的 example1.txt 副本。
- cp example1.txt <directory>/ 将在 <directory> 指定的位置创建 example1.txt 的副本。

---

**移动和重命名文件**
- mv a.txt b.txt 将a.txt重命名为b.txt
- mv directory1 directory2 将目录重命名
- mv a.txt directory1/ 将a.txt移动到目录中
- mv a.txt dirrectory1/b.txt 将a.txt移动到目录中移动到目录中并把它重命名为b.txt

---

**删除文件和目录**
- rm a.txt
- rm directory1/

---

**更改文件权限**
- chmod u+w example1.txt将为用户 (u) 添加对文件的写（修改）权限。您还可以将g修饰符用于组权限或o用于世界权限。
- chmod g+r example1.txt 将为该组的文件添加读取（访问）权限。
- 您可以使用大量权限来保护或打开系统的各个方面。

---

**获取有关任何命令的详细信息**
- man <command>显示有关该命令的信息
- man -k <keyword>将在所有册页中搜索您指定的关键字

---

**将文件从您的位置复制到远程计算机。**如果需要将文件从本地计算机复制到远程访问的计算机，可以使用以下scp命令：
- scp /localdirectory/example1.txt <username>@<remote>:<path>将 example1.txt 复制到远程计算机上的指定 <path>。您可以将 <path> 留空以复制到远程计算机的根文件夹。
- scp <username>@<remote>:/home/example1.txt ./ 将 example1.txt 从远程计算机上的主目录移动到本地计算机上的当前目录。

---

**打开"-"虚线文件名**:cat < -

**读取文件名为空格的文件内容**：cat spaces之后用tab补全即可。

**file 命令用于确定文件的类型。**
- .file类型可以是人类可读的（例如'ASCII 文本'）或MIME 类型（例如'text/plain; charset=us-ascii'）
- file 文件名.扩展名
- file dircetoryname/*:显示特定目录中的所有文件文件类型

**find命令**

- find命令"find . -type f -size 1033c"，其中"." 查找当前目录以及子目录，-type f 指定文件类型为普通文件，-size 1033c 指定文件大小为 1033 bytes

  

---



**string**命令查看文件中的字符串

**grep **用于查找文件里符合条件的字符串

grep 指令用于查找内容包含指定的范本样式的文件，如果发现某文件的内容符合所指定的范本样式，预设 grep 指令会把含有范本样式的那一列显示出来。若不指定任何文件名称，或是所给予的文件名为 **-**，则 grep 指令会从标准输入设备读取数据。



- grep xxx [-abcEFGhHilLnqrsvVwxy]（https://www.runoob.com/linux/linux-comm-grep.html）、 [-A<显示行数>]、[-B<显示列数>]、[-C<显示列数>]、[-d<进行动作>]、[-e<范本样式>]、[-f<范本文件>]、[--help]、[范本样式]、[文件或目录...] **(xxx为查找的字符串)**

- 如：在当前目录中，查找后缀有 file 字样的文件中包含 test 字符串的文件，并打印出该字符串的行。此时，可以使用如下命令：

  ```
  grep test *file 
  ```

  结果如下所示：

  ```
  $ grep test test* #查找前缀有“test”的文件包含“test”字符串的文件  
  testfile1:This a Linux testfile! #列出testfile1 文件中包含test字符的行  
  testfile_2:This is a linux testfile! #列出testfile_2 文件中包含test字符的行  
  testfile_2:Linux test #列出testfile_2 文件中包含test字符的行 
  ```

---

#### Piping and Redirection

重定向到文件将其保存到文件中以作为记录保存、输入到另一个系统或发送给其他人。大于运算符 ( > ) 向命令行表明我们希望程序输出（或它发送到 STDOUT 的任何内容）保存在文件中而不是打印到屏幕上。

- ls > xxx:把ls的执行结果输出到文件abc.txt
- 在管道和重定向时，实际数据将始终相同，但该数据的格式可能与通常打印到屏幕上的格式略有不同。



#### 管道：一种将数据从一个程序发送到另一个程序的机制

* 我们使用的运算符是 (|)（在大多数键盘上的反斜杠 (\) 键上方找到）。这个操作符的作用是将左边程序的输出作为输入提供给右边的程序。
* cat a.txt | (   )



#### sort命令 ：对文件进行排序

按特定顺序排列记录。默认情况下，sort 命令假定内容为 ASCII 对文件进行排序。在 sort 命令中使用选项也可用于按数字排序。

* 以数字开头的行将出现在以字母开头的行之前。

* 以字母表中较早出现的字母开头的行将出现在以字母表中较晚出现的字母开头的行之前。

* 以小写字母开头的行将出现在以大写相同字母开头的行之前。



sort -u:在输出行去除重复行

sort -r:升序输出

sort -n:按数值排序

---

### Base64

- base64 -d 文件名：解码

- base64 -i 文件名：解码时忽略非字母字符



### tr

从标准输入中通过替换或删除操作进行字符转换。tr主要用于删除文件中控制字符或进行字符转换

使用tr时要转换两个字符串：字符串1用于查询，字符串2用于处理各种转换。tr刚执行时，字符串1中的字符被映射到字符串2中的字符，然后转换操作开始。

* cat testfile | tr a-z A-Z:将testfile中的小写字母全部转换成大写字母。
* tr -d:删除指定字符



### gzip压缩文件（可同时压缩多个文件）

gzip filename1 filename2：`gzip`将创建一个文件`filename.gz`并删除原始文件。

默认情况下，`gzip`在压缩文件中保留原始文件的时间戳、模式、所有权和名称。

gzip -k filename：保留原始文件



---

### 在客户端创建公共和私人SSH密钥

- mkdir ~/ .ssh
- chmod 700 ~/ .ssh
- ssh-keygen -t rsa

输入保存密钥的位置以及密钥的密码

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/b/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/b/.ssh/id_rsa.
Your public key has been saved in /home/b/.ssh/id_rsa.pub.
```



### telnet

- ```
  telnet [-8acdEfFKLrx][-b<主机别名>][-e<脱离字符>][-k<域名>][-l<用户名称>][-n<记录文件>][-S<服务类型>][-X<认证形态>][主机名称或IP地址<通信端口>]
  ```

  (https://www.runoob.com/linux/linux-comm-telnet.html)

### openssl

- openssl s_client [-connect host:port](连接主机：端口)



### nmap

- nmap [hostname/ipaddress](使用主机名和 IP 地址扫描系统。) 可同时扫描多个主机、整个子网
- nmap -v:用于获取有关远程机器的更多详细信息
- sudo nmap -sA [ipadd]:扫描以检测防火墙设置
- sudo nmap -sL [ipadd]:识别主机名
- nmap -iL a.txt:从文件扫描



### diff

diff 代表**差异**。该命令用于通过逐行比较文件来显示文件中的差异，告诉我们要更改一个文件中的哪些行以使两个文件相同。

**diff**使用某些**特殊符号**和**指令**，这些**符号**和**指令**使两个文件相同。

**特殊符号有：** 

```
a：添加
c： 更改
d： 删除
```

diff a .txt b.txt:

```
$ ls
a.txt  b.txt

$ cat a.txt
Gujarat
Uttar Pradesh
Kolkata
Bihar
Jammu and Kashmir

$ cat b.txt
Tamil Nadu
Gujarat
Andhra Pradesh
Bihar
Uttar pradesh
```

使用diff命令后

```
$ diff a.txt b.txt
0a1
> Tamil Nadu
2,3c3
< Uttar Pradesh
 Andhra Pradesh
5c5
 Uttar pradesh
```

diff输出的第一行包括：

- 第一个文件对应的行号
- 一个特殊的符号和
- 对应于第二个文件的行号。

**0a1**意味着**在**第 0 行**之后**（在文件的最开头）你必须添加**Tamil Nadu**以匹配第二个文件的第 1 行。然后它告诉我们每个文件中这些行是什么，前面有符号： 

- 以**<**开头的行是来自第一个文件的行。
- **>**前面的行是来自第二个文件的行。
- 下一行包含**2,3c3**这意味着需要更改第一个文件中的第 2 行到第 3 行以匹配第二个文件中的第 3 行。然后它告诉我们带有上述符号的那些行。
- 三个破折号**（“—”）**只是将文件 1 和文件 2 的行分开。



当**diff**告诉我们需要删除一行时

```
$ cat a.txt 
Gujarat 
Andhra Pradesh 
Telangana 
Bihar 
Uttar pradesh $ cat b.txt 
Gujarat 
Andhra Pradesh 
Bihar 
Uttar pradesh $ diff a.txt b.txt 
3d2 
< Telangana
```

输出**3d2**表示删除第一个文件的第 3 行，即*Telangana，*以便两个文件在第 2 行**同步**

---

“.”是指当前目录，“./"可以用来执行当前目录下的可执行文件

### nc

用于设置路由器[https://www.runoob.com/linux/linux-comm-nc.html]

### crontab

定期执行程序的命令
