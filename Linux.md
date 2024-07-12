## 9-Linux实操篇-实用指令

### 9.1 指定运行级别

* **基本介绍**：
    * 0：关机                     
    * 1.单用户[找回丢失密码]
    * 2.多用户状态没有网络服务
    * 3.多用户状态有网络服务
    * 4.系统未使用保留给用户
    * 5.图形界面
    * 6.系统重启

**常用的运行级别是3和5，也可以指定默认运行级别**

* 应用实例

    > 命令：init [0,1,2,3,4,5,6]	例如：`init 6`，系统将会重启

### 9.2 找回root密码

### 9.3 帮助指令

#### 9.3.1 man指令

**基本语法**：man [命令或配置文件]（功能描述：获得帮助信息）

* 案例：查看ls命令的帮助信息

    ```shell
    man ls
    ```

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231229100603317.png" alt="image-20231229100603317" style="zoom:67%;" />



#### 9.3.2 help指令

**基本语法**：help 命令（功能描述：获得shell内置命令的帮助信息）

* 案例：查看cd命令的帮助信息

    ```shell
    help cd
    ```

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231229100719083.png" alt="image-20231229100719083" style="zoom:67%;" />

### 9.4 文件目录类指令

#### 9.4.1 pwd指令

**基本语法**：pwd	**功能描述**：显示当前工作目录的绝对路径

* 案例：查看a.txt绝对路径

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231229101950837.png" alt="image-20231229101950837" style="zoom:80%;" />

#### 9.4.2 ls指令

**作用**：ls命令用于列出指定工作目录下之内容（包括文件和目录）。

**基本语法**：ls 参数 路径　　--参数可选

##### 1.不带参数

> **显示指定目录的文件和目录（不包含隐藏属性的文件和目录）。**

* 案例：`ls /home`

    ![image-20231229102541316](D:\Software\Typora\复制的图片\typora-user-images\image-20231229102541316.png)

##### 2.参数a

> **显示指定目录的所有文件和目录（包含隐藏属性的文件和目录，凡是以“.”开头都属于隐藏的文件或目录）。**

* 案例：`ls -a /`

    ![image-20231229103019966](D:\Software\Typora\复制的图片\typora-user-images\image-20231229103019966.png)

##### 3.参数l

> **列出指定目录的文件和目录（不包含隐藏属性的文件和目录），同时也列出文件和目录的形态、权限、属主、属主、文件大小等。**

* 案例：`ls -l /`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231229103254779.png" alt="image-20231229103254779" style="zoom:80%;" />

##### 4.参数al

> **列出指定目录的文件和目录（包含隐藏属性的文件和目录），同时也列出文件和目录的形态、权限、属主、属主、文件大小等。**

* 案例：`ls -al /`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231230090542327.png" alt="image-20231230090542327" style="zoom:80%;" />

##### 5.参数r

> **列出指定目录的文件和目录（不包含隐藏属性的文件和目录），以字母倒序的方式。**

* 案例：`ls -r /`

    ![image-20231229111148985](D:\Software\Typora\复制的图片\typora-user-images\image-20231229111148985.png)



#### 9.4.3 cd指令

**作用**：切换到指定目录

**基本语法**：cd [参数]	

> cd ~或者cd : 回到自己的家目录
> cd ..回到当前目录的上一级目录

* 案例1：使用绝对路径切换到root目录	`cd /root`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231230092048130.png" alt="image-20231230092048130" style="zoom:80%;" />

* 案例2：使用相对路径到/root目录，假设当前在/home/jack    `cd ../../root`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231230092347285.png" alt="image-20231230092347285" style="zoom:80%;" />

* 案例3：回到当前目录的上一级目录    `cd ..`
* 案例4：回到家目录    `cd ~`



#### 9.4.4 mkdir指令

**作用**：用于创建目录

**基本语法**：mkdir [选项] 要创建的目录

> 常用选项：-p，创建多级目录

* 案例1：创建一个目录/home/dog

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231230111508764.png" alt="image-20231230111508764" style="zoom:80%;" />

* 案例2：创建多级目录/home/animal/tiger

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231230111848056.png" alt="image-20231230111848056" style="zoom:80%;" />



#### 9.4.5 rmdir指令

**作用**：删除***空目录***

**基本语法**：rmdir [选项] 要删除的空目录

> **使用细节**
>
> * rmdir删除的是空目录，如果目录下有内容无法删除
> * 若想删除非空目录，需要使用`rm -rf 目录`

* 案例：删除一个目录/home/dog	`rmdir /home/dog`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231230112514564.png" alt="image-20231230112514564" style="zoom:80%;" />

* 案例：删除目录/home/animal，其中animal目录非空    `rm -rf /home/animal`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231122113367.png" alt="image-20231231122113367" style="zoom: 80%;" />



#### 9.4.5 touch指令

**作用**：创建空文件

**基本语法**：`touch 文件名`

* 案例：在/home目录下，创建一个空文件hello.txt	`touch hello.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231122554212.png" alt="image-20231231122554212" style="zoom:80%;" />



#### 9.4.6 touch指令

作用：拷贝文件到指定目录

基本语法：`cp [选项] source dest`

> 常用选项：**-r**	递归复制整个文件夹

* 案例1：将/home/hello.txt拷贝到/home/bbb下	`cp hello.txt bbb`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231123831458.png" alt="image-20231231123831458" style="zoom:80%;" />

* 案例2：将/home/bbb整个目录复制到/opt    `cp -r /home/bbb /opt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231124720059.png" alt="image-20231231124720059" style="zoom:80%;" />

> 使用细节：拷贝过程对于相同文件全部覆盖`\cp`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231125114358.png" alt="image-20231231125114358" style="zoom:80%;" />



#### 9.4.7 rm指令

**作用**：删除文件或目录

**基本语法**：**`rm [选项] 文件或目录`**

> 常用选项：
>
> -r：递归删除整个文件夹
> -f：强制删除不提示

* 案例1：将/home/hello.txt删除	**`rm /home/hello.txt`** 或 **`rm -f /home/hello.txt`**

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231155238464.png" alt="image-20231231155238464" style="zoom:80%;" />

* 案例2：递归删除整个文件夹/home/bbb    `rm -rf /home/bbb`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231155552864.png" alt="image-20231231155552864" style="zoom:80%;" />

#### 9.4.8 mv指令

**作用**：移动文件与目录或重命名

**基本语法**：

`mv oldNameFile newNameFile`	**重命名文件**

`mv /temp/movefile /targetFolder`	**移动文件**

* 案例1：将/home/cat.txt文件重命名为pig.txt	`mv /home/cat.txt pig.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231160412709.png" alt="image-20231231160412709" style="zoom:80%;" />

* 案例2：将/home/pig.txt文件移动到/root目录下    `mv /home/pig.txt /root`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231160826794.png" alt="image-20231231160826794" style="zoom:80%;" />

* 案例3：移动整个目录，将/opt/bbb移动到/home下    `mv /opt/bbb/ /home/`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231161811570.png" alt="image-20231231161811570" style="zoom:67%;" />

#### 9.4.9 cat指令

**作用**：查看文件内容

**基本语法**：`cat [选项] 要和查看的文件`

> **常用选项**：
>
> ​	`-n` 显示行号

* 案例：/etc/profile文件内容，并显示行号	`cat -n /etc/profile`

> 使用细节：cat只能浏览文件，不能修改文件，为了浏览方便，一般会带上**管道命令|more**

#### 9.4.10 more指令

**作用**：more指令是基于VI编辑器的文本过滤器，它以全屏的方式按页显示文本文件的内容。more指令中内置了若干快捷键

> **操作**：
>
> ​	空格：向下翻一页
> ​	回车键：向下翻一行
> ​	q：立刻离开more，不再显示该文件内容
> ​	Ctrl+F：向上翻滚一屏
> ​	Ctrl+B：返回上一屏
> ​	=：显示当前的行号
> ​	:f：输出文件名和当前行的行号

* 案例：使用more查看文件/etc/profile	`more /etc/profile`

#### 9.4.11 less指令

**作用**：less指令用来分屏查看文件内容，它的功能与more指令类似，但比more更加强大，支持各种显示终端，less指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容，对于显示大型文件具有较高的效率

**基本语法**：`less [要查看的文件]`

> **操作**：
> 	空格：向下翻一页
> 	[pagedown]：向下翻动一页
> 	[pageup]：向上翻动一页
> 	/字符串：向下搜索[字符串]的功能；n：向下查找；N：向上查找
> 	?字符串：向下搜索[字符串]的功能；n：向上查找；N：向下查找
> 	q：退出less程序

* 案例：使用less查看一个大文本文件/opt/杂文.txt	`less /opt/杂文.txt`

#### 9.4.12 echo指令

**作用**：输出内容到控制台

**基本语法**：`echo [选项] [输出内容]`

* 案例：使用echo指令输出环境变量，比如输出$PATH、$HOSTNAME	`echo $PATH` `echo $HOSTNAME`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231211843576.png" alt="image-20231231211843576" style="zoom:80%;" />

* 案例：使用echo指令输出hello world    `echo "hello world"`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231211954870.png" alt="image-20231231211954870" style="zoom:80%;" />

#### 9.4.13 head指令

**作用**：head用于显示文件的开头部分内容，默认情况下head指令显示文件的前10行内容

**基本语法**：`head 文件`（查看文件前10行内容）或 `head -n 数字 文件`（查看文件前n行内容）

* 案例：查看/etc/profile的前面5行内容	`head -n 5 /etc/profile`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231212811430.png" alt="image-20231231212811430" style="zoom:80%;" />

#### 9.4.13 tail指令

**作用**：用于输出文件中尾部的内容，默认情况下tail指令显示文件的后10行内容

**基本语法**：

> `head 文件`（查看文件后10行内容）
> `head -n 数字 文件`（查看文件后n行内容）
> `head -f 文件`（实时追踪该文档的所有更新）

* 案例1：查看/etc/profile的最后5行内容	`tail -n 5 /etc/profile`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231214020972.png" alt="image-20231231214020972" style="zoom:80%;" />

* 案例2：实时监控mydata.txt，看看当文件有变化时是否看到，实时的追加日期    `tail -f /home/mydata.txt`

#### 9.4.13 >指令和>>指令

**作用**：>输出重定向  >> 追加

基本语法：

> ls -l > 文件					列表的内容写入文件a.txt中（覆盖写）
> ls -al >> 文件				列表的内容追加到文件a.txt的末尾
> cat 文件1 > 文件2		将文件1的内容覆盖到文件2
> echo "内容" >> 文件	追加

* 案例1：将/home目录下的文件列表写入/home/info.txt中	`ls -l /home > /home/info.txt`
    **注意**：如果文件不存在则自动创建

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231220447697.png" alt="image-20231231220447697" style="zoom:80%;" />

* 案例2：将当前日历信息追加到/home/mycal文件中    `cal >> /home/mycal`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20231231220841854.png" alt="image-20231231220841854" style="zoom:80%;" />

#### 9.4.14 ln指令

**作用**：软链接也称为符号链接，类似于windows里的快捷方式，主要存放了链接其他文件的路径

**基本语法**：`ln -s [源文件或目录] [软连接名]`    给原文件创建一个软连接

* 案例1：在/home目录下创建一个软连接myroot，连接到/root目录	`ln -s /root /home/myroot`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101122147118.png" alt="image-20240101122147118" style="zoom: 80%;" />

* 案例2：删除软连接myroot    `rm -f /home/myroot`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101122343073.png" alt="image-20240101122343073" style="zoom:80%;" />

#### 9.4.15 history指令

**作用**：查看已经执行过的历史命令，也可以执行历史指令

**基本语法**：`history`

* 案例1：显示所有的历史命令	`history`

* 案例2：显示最近使用过的10个命令    `history 10`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101122945046.png" alt="image-20240101122945046" style="zoom:80%;" />

* 案例3：执行历史编号为5的指令    `!5`



### 9.5 时间日期类

#### 9.5.1 date指令-显示时间

**作用**：显示日期

**基本语法**：

> `date`：显示当前时间
> `date + %Y`：显示当前年份
> `date + %d`：显示当前月份
> `date "+%Y-%m-%d %H:%M:%S"`：显示年月日时分秒

* 案例1：显示当前时间信息    `date`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101124042497.png" alt="image-20240101124042497" style="zoom:80%;" />

* 案例2：显示当前年月日    `date "+%Y-%m-%d"`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101124230610.png" alt="image-20240101124230610" style="zoom:80%;" />

* 案例3：显示当前年月日时分秒    `date "+%Y-%m-%d %H:%M:%S"`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101124705869.png" alt="image-20240101124705869" style="zoom:80%;" />

#### 9.5.1 date指令-设置时间

**基本语法：**`date -s 字符串时间`

* 案例：设置系统当前时间，比如2024-1-1 12:50:34    `date -s "2024-1-1 12:5:30"`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101125202799.png" alt="image-20240101125202799" style="zoom:80%;" />

#### 9.5.2 cal指令

**作用**：查看日历

**基本语法**：`cal [选项]`    不加选项，显示本月日历

* 案例1：显示当前日历    `cal`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101125711715.png" alt="image-20240101125711715" style="zoom:80%;" />

* 案例2：显示2020年日历    `cal 2020`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101125810988.png" alt="image-20240101125810988" style="zoom:80%;" />



### 9.6 搜索查找类指令

#### 9.6.1 find指令

**作用**：从指定目录向下递归地遍历其各个子目录，将满足条件的文件或目录显示在终端

**基本语法**：`find [搜索范围] [选项]`

> **选项说明**：
> 	-name<查询方式>：按照指定的文件名查询方式查找文件
> 	-user<用户名>：查找属于指定用户的所有文件
> 	-size<文件大小>：按照指定的文件大小查找文件 

* 案例1：按文件名，根据名称查找/home目录下的hello.txt文件    `find /home -name hello.txt `

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101132702298.png" alt="image-20240101132702298" style="zoom:80%;" />

* 案例2：按拥有者，查找/opt目录下，用户名为nobody的文件    `find /opt -user nobody`

* 案例3：查找整个linux系统下大于200MB的文件（+n大于 -n小于 n等于，单位有k,M,G）   `find / -size +200M`

#### 9.6.2 locate指令

**作用**：快速定位文件路径。locate利用事先建立好的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件，无需遍历整个文件系统，查询速度较快。为了保证locate查询结果的准确性，必须定期更新locate

**基本语法**：`locate 搜索文件`

> **特别说明**：由于locate指令基于数据库查询，所有第一次运行前，必须使用updatedb指令创建locate数据库

* 案例：使用locate指令快速定位hello.txt位置    `locate hello.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101134619508.png" alt="image-20240101134619508" style="zoom:80%;" />

#### 9.6.3 which指令

**作用**：查看某个指令在哪个目录下

* 案例：查看ls在哪个目录下    `which ls`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240101135014814.png" alt="image-20240101135014814" style="zoom:80%;" />

#### 9.6.4 grep指令

**作用**：过滤查找   管道符"|"表示将前一个命令的处理结果传输给后面的命令处理

**基本语法**：`grep [选项] 查找内容 源文件`

> **常用选项**：
> -n：显示匹配行及行号
> -i：忽略字母大小写

* 案例：请在hello.txt中，查找"yes"所在行，并且显示行号

    * **写法1**：`cat /home/hello.txt | grep -n "yes"`

        <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106184510234.png" alt="image-20240106184510234" style="zoom:80%;" />

    * **写法2**：`grep -n "yes" /home/hello.txt`

        <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106184754788.png" alt="image-20240106184754788" style="zoom:80%;" />



### 9.7 压缩和解压

#### 9.7.1 gzip/gunzip指令

**作用**：gzip用于压缩文件，gunzip用于解压文件

**基本语法**：

`gzip 文件`    将文件压缩为*.gz文件
`gunzip 文件.gz`	解压缩文件

* 案例1：gzip压缩，将/home下的hello.txt文件进行压缩	`gzip /home/hello.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106190206140.png" alt="image-20240106190206140" style="zoom:80%;" />

* 案例2：gunzip，将/home下的hello.txt.gz文件进行解压缩    `gunzip /home/hello.txt.gz`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106190240950.png" alt="image-20240106190240950" style="zoom:80%;" />

#### 9.7.2 zip/unzip指令

**作用**：zip用于压缩文件或目录，unzip用于解压

**基本语法**：
`zip [选项] xxx.zip`
`unzip [选项] xxx.zip`

> **zip常用选项**：
> -r：递归压缩，即压缩目录
> **unzip常用选项**：
> -d<目录>：指定解压后文件的存放目录

* 案例1：将/home下的所有文件和文件夹压缩成myhome.zip    `zip -r myhome.zip /home/`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106192134938.png" alt="image-20240106192134938" style="zoom:80%;" />

* 案例2：将myhome.zip解压到/opt/tmp目录下    `unzip -d /opt/tmp/ /home/myhome.zip `

#### 9.7.3 tar指令

**作用**：打包指令，最终得到的文件是.tar.gz的文件

**基本语法：**`tar [选项] xxx.tar.gz 打包的内容`

> **选项说明**：
> -c：产生.tar打包文件
> -v：显示详细信息
> -f：指定压缩后的文件名
> -z：打包同时压缩
> -x：解压.tar文件

* 案例1：压缩多个文件，将/home/pig.txt和/home/cat.txt压缩成pc.tar.gz    `tar -vczf pc.tar.gz /home/pig.txt /home/cat.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106195756565.png" alt="image-20240106195756565" style="zoom:80%;" />

* 案例2：将/home的文件夹压缩成myhome.tar.gz    `tar -vczf myhonme.tar.gz /home/`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106201926413.png" alt="image-20240106201926413" style="zoom:80%;" />

* 案例3：将pc.tar.gz解压到当前目录，切换到/opt    `tar -zxvf pc.tar.gz ` 

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106202233753.png" alt="image-20240106202233753" style="zoom:80%;" />

* 案例4：将myhome.tar.gz解压到/opt/tmp2目录下    `tar -zxvf /home/myhonme.tar.gz -C /opt/tmp2`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240106202911655.png" alt="image-20240106202911655" style="zoom:80%;" />

 

## 10-组管理和权限管理

### 10.1 文件的所有者

一般为文件的创建者，谁创建了该文件，自然而然成为该文件的所有者

#### 10.1.1 查看文件的所有者

**指令**：`ls -ahl`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108143041747.png" alt="image-20240108143041747" style="zoom:80%;" />

#### 10.1.2 修改文件所有者

**指令**：`chown 用户名 文件名`

* 案例：使用root创建一个文件apple.txt，然后将其所有者改为tom

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108143226677.png" alt="image-20240108143226677" style="zoom:80%;" />

### 10.2 用户组的创建

**基本指令**：`groupadd 组名`

* 案例：创建一个组monster，创建一个用户fox，并将fox加入monster组中    `groupadd monster` `useradd -g monster fox`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108144224827.png" alt="image-20240108144224827" style="zoom:80%;" />

### 10.3 文件所在组

当某个用户创建了一个文件后，这个文件的所在组就是该用户所在的组

#### 10.3.1 查看文件所在组

**基本指令**：`ls -ahl`

* 案例：使用fox创建一个文件，查看文件属于哪个组？

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108145530652.png" alt="image-20240108145530652" style="zoom:80%;" />

#### 10.3.2 修改文件所在的组

**基本指令**：`chgrp 组名 文件名`

* 案例：使用root创建文件orange.txt，查看当前文件属于哪个组，然后将该文件所在组修改为fruit组

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108150700921.png" alt="image-20240108150700921" style="zoom:80%;" />

### 10.3 修改用户所在组

在添加用户时可以指定添加到哪个组中，同样的，用root权限也可以改变某个用户所在组

#### 10.3.1 改变用户所在组

> 1.usermod -g 新组名 用户名
> 2.usermod -d 目录名 用户名	改变该用户登录的初始目录    注意：用户需要有进入新目录的权限

* 案例：将zwj用户从原来所在组，修改到wudang组    `usermod -g wudang zwj`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108152504831.png" alt="image-20240108152504831" style="zoom:80%;" />

### 10.4 权限的基本介绍

ls -l 中显示的内容如下：
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240108160309079.png" alt="image-20240108160309079" style="zoom:80%;" />

> **0-9位说**明：
> 1.第0位确定文件类型
> 	l是 链接，相当于windows的快捷方式
> 	d是目录，相当于windows的文件夹
> 	c是字符设备文件，如鼠标、键盘
> 	b是块设备，比如硬盘
> 2.第1-3位确定所有者（该文件的所有者）用户该文件的权限
> 3.第4-6位确定所属组（同用户组的）拥有该文件的权限
> 4.第7-9位确定其他用户拥有该文件的权限

可用数字表示为：r=4，w=2，x=1，因此**rwx**=4+2+1=**7**

> **其他说明**：
> **5** ：文件：硬连接数  目录：子目录数
> **root**：用户
> **root**：组
> **141**：文件大小（字节）
> **12 月** 28 18:19：最后修改日期
> **jack**：目录名或文件名

#### 10.4.1 文件/目录的rwx权限详解

##### rwx作用到文件

> **[r]代表可读**：可以读取查看
> **[w]代表可写**：可以修改，但是不代表可以删除该文件，删除一个文件的前提是对该文件所在的目录有写权限
> **[x]代表可执行**：可以被执行

##### rwx作用到目录

> **[r]代表可读**：可以读取，ls查看目录内容
> **[w]代表可写**：可以修改，对目录内创建+删除+重命名目录
> **[x]代表可执行**：可以进入该目录

### 10.5 修改权限

通过chmod指令，可以修改文件或目录的权限

##### 第一种方式：+、-、=变更权限

> u：所有者 g：所有组 o：其他人 a：所有人(u、g、o的总和)
> `chmod u=rwx,g=rw,o=x 文件/目录名`
> `chmod o+w 文件/目录名`
> `chmod a-x 文件/目录名`

* 案例1：给abc文件的所有者读写执行的权限，给所在组读执行权限，给其他组读执行权限`chmod u=rwx,g=rw,o=rw abc` 
* 案例2：给abc文件的所有者除去执行的权限，增加组写的权限`chmod u-x,g+w abc `
* 案例3：给abc文件的所有用户添加读的权限`chmod a+r abc`

##### 第二种方式：通过数字变更权限

> **r=4，w=2，x=1	rwx=4+2+1=7**

`chmod u=rwx,g=rw,o=x 文件/目录名 `相当于 `chmod 751 文件/目录名`

* 案例：将/home/abc.txt文件的权限修改为rwxr-xr-x，使用数字的方式实现`chmod 755 /home/abc.txt`

### 10.6修改文件/目录的所有者

> `chown newowner 文件/目录`	改变所有者
> `chown newowner:newgroup` 文件/目录	改变所有者和所在组
> -R	如果是目录，则使其下所有子文件或目录递归生效

* 案例1：将/home/abc.txt文件的所有者修改为tom	`chown tom /home/abc.txt`
* 案例2：将/home/kkk目录下所有文件和目录的所有者都修改为tom    `chown -R tom /home/kkk`

### 10.7 修改文件/目录所在组

> `chgrp newgroup 文件/目录`	改变所在组

* 案例1：将/home/abc.txt文件的所在组修改成shaolin	`chgrp shaolin /home/abc.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240109122033030.png" alt="image-20240109122033030" style="zoom:80%;" />

* 将/home/kkk目录下的所有文件和目录的所在组都修改成shaolin    `chgrp -R shaolin /home/kkk`

### 最佳实践1—警察土匪

> jack，jerry 警察 police
> xh，xq 土匪 bandit
> 1.创建组
> 2.创建用户
> 3.jack创建一个文件，自己可以读写，本组人可以读，其他组没有任何权限
> 4.jack修改文件，让其他人可以读，本组人可以读写
> 5.xh投靠警察，看看是否可以读写

```shell
1.创建组
groupadd police
groupadd bandit
2.创建用户
useradd -g police jack
useradd -g police jerry
useradd -g bandit xh
useradd -g bandit xq
passwd jack
passwd jerry
passwd xh
passwd xq
3.jack创建一个文件，自己可以读写，本组人可以读，其他组没有任何权限
su jack
vim jack.txt
chmod 640 jack.txt
4.jack修改文件，让其他人可以读，本组人可以读写
chmod 664 jack.txt
5.xh投靠警察，看看是否可以读写
su root
usermod -g police xh
# id xh查看组是否修改成功
不能进行读写，因为对目录jack没有权限，需要先使用jack用户登录放开权限
su root
chmod 770 /home/jack
```

### 最佳实践2

```
1.建立两个组sx（神仙），yg（妖怪）
groupadd sx
groupadd yg
2.建立四个用户：唐僧、悟空、八戒、沙僧
useradd ts
useradd wk
useradd bj
useradd ss
3.设置密码
passwd ts
passwd wk
passwd bj
passwd ss
4.把悟空、八戒放入妖怪，唐僧、沙僧在神仙
usermod -g yg wk
usermod -g yg bj
usermod -g sx ts
usermod -g sx ss
5.用悟空建立一个文件monkey.java，该文件输出I am a monkey
su wk
vim monkey.txt
6.给八戒一个可以rw的权限
chmod g+r+w+x wk
chmod g+w monkey.txt
7.八戒修改monkey.java，加一句话I am a pig
vim monkey.txt
8.唐僧、沙僧对该文件没有权限

9.把沙僧放入妖怪组
usermod -g yg ss（root用户）
10.让沙僧修改文件monkey，加一句话：我是沙僧
vim monkey.txt
11.对文件夹rwx的细节讨论和测试
```



## 11-定时任务调度

### 11.1 crond任务调度

#### 11.1.1 概述

任务调度是指系统在某个时间执行的特定的命令或程序。

#### 11.1.2 任务调度分类

1.系统工作：有些重要的工作必须周而复始地执行，如病毒扫描等

2.个别用户工作：个别用户可能希望执行某些程序，比如对mysql数据库的备份

**基本语法**：`crontab [选项]`

> **常用选项：**
> -e：编辑crontab定时任务
> -l：查询crontab任务
> -r：删除当前用户所有的crontab任务

* 快速入门

    设置任务调度文件：/etc/crontab

    设置个人任务调度，执行crontab -e指令

    接着输入任务到调度文件

    如：*/1 * * * * ls -l /etc/ > /tmp/to.txt，代表每小时的每分钟执行ls -l /etc/ > /tmp/to.txt命令

    > **参数细节说明**
    > 									含义				范围
    >
    > 第一个*	一小时当中的第几分钟	0-59
    > 第二个*	一天当中的第几个小时	0-23
    > 第三个*	一个月当中的第几天		1-31
    > 第四个*	一年当中的地几个月		1-12
    > 第无个*	一周当中的星期几			0-7（0和7都代表星期日）

**特殊符号说明**

| 特殊符号 |                             含义                             |
| :------: | :----------------------------------------------------------: |
|    *     |   代表任何时间。比如第一个*就代表一小时中每分钟都执行一次    |
|    ,     | 代表不连续的时间。比如"0 8,12,16 * * *"命令，就代表在每天的8点0分，12点0分，16点0分都执行一次指令 |
|    -     | 代表连续的时间范围。比如"0 5 * * 1-6"命令，代表在周一到周六的凌晨5点0分执行命令 |
|   */n    | 代表每隔多久执行一次。比如"*/10 * * * *"命令，代表每隔10分钟执行一次命令 |

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240109145309519.png" alt="image-20240109145309519" style="zoom:80%;" />



* 案例1：每隔一分钟，将当前日期信息追加到/tmp/mydate文件中`*/1 * * * * date >> /tmp/mydate`

* 案例2：每隔一分钟，将当前日期和日历都追加到/home/mycal文件中

    * 1.`vim /home/my.sh` 写入内容 date >> /home/mycal和cal >> /home/mycal

        <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240109145801049.png" alt="image-20240109145801049" style="zoom:80%;" />

    * 2.给my.sh执行权限`chmod u+x my.sh`

    * 3.crontab -e，增加*/1 * * * * /home/my.sh

* 案例3：每天凌晨2点将mysql数据库testdb，备份到文件中。提示：指令为mysqldump -u root -p 密码 数据库 >> /home/db.bak

    * `1.crontab -e`
    * `0 2 * * * mysqldump -u root -p 密码 数据库 > /home/db.bak`

#### 11.1.3 crond相关指令

crontab -r：中止任务调度

crontab -l：列出当前有哪些任务调度

service crond restart：重启任务调度



### 11.2 at定时任务

#### 11.2.1 基本介绍

* at命令是一次性定时计划任务，at的守护进程atd会以后台模式运行，检查作业队列来运行
* 默认情况下，atd守护进程每60秒检查作业队列，有作业时，会检查作业运行时间，如果时间与当前时间匹配，则运行次作业
* at命令是一次性定时计划任务，执行完一个任务后不再执行此任务了
* 在使用at命令的时候，一定要保证atd进程的启动，可以使用相关指令来查看`ps -ef | grep atd`

#### 11.2.2 at命令格式

`at [选项] [时间]`

Ctrl + D 结束at命令的输入

**at命令选项**

| 选项          | 含义                                                     |
| ------------- | -------------------------------------------------------- |
| -m            | 当指定的任务被完成后，将给用户发送邮件，即使没有标准输出 |
| -I(大写i)     | atq的别名                                                |
| -d            | atrm的别名                                               |
| -v            | 显任务将被执行的时间                                     |
| -c            | 打印任务的内容到标准输出                                 |
| -V            | 显示版本信息                                             |
| -q <队列>     | 使用指定的队列                                           |
| -f <文件>     | 从指定文件读入任务而不是从标准输入读入                   |
| -t <时间参数> | 以时间参数的形式提交要运行的任务                         |

#### 11.2.3 at时间定义

1.接受在当天的hh:mm（小时:分钟）式的时间指定。假如该时间已过去，那么在第二天执行。例如：04:00

2.使用midnight（深夜）、noon（中午）、teatime（饮茶时间，一般是下午4点）等比较模糊的词语来指定时间

3.采用12小时制，即在时间后面加上AM、PM来说明是上午还是下午。例如：12pm

4.指定命令执行的具体日期，指定格式为**month day（月 日）**或**mm/dd/yy（月/日/年）**或**dd.mm.yy（日.月.年）**，指定的日期必须跟在指定时间的后面。例如：04:00 2021-03-1

5.使用相对计时法。指定格式为：now + count time-units，now是当前时间，time-units是时间单位，可以是minutes（分钟）、hours（小时）、days（天）、weeks（周）。count是时间的数量，几天、几小时。例如：now + 5minutes

6.直接使用today（今天）、tomorrow（明天）来指定完成命令的时间。

#### 11.2.4 案例

* 案例1：2天后的下午5点执行 /bin/ls home    `at 5pm + 2 days`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240110134503143.png" alt="image-20240110134503143" style="zoom:80%;" />

* 案例2：atq命令来查看系统中有没有执行的工作任务    `atq`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240110134524016.png" alt="image-20240110134524016" style="zoom:80%;" />

* 案例3：明天17点钟，输出时间到指定文件内，比如/root/date100.log    `at 5pm tomorrow`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240110134759844.png" alt="image-20240110134759844" style="zoom:80%;" />

* 案例4：2分钟后，输出时间到指定文件内，比如/root/date200.log    `at now + 2 minutes`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240110135407341.png" alt="image-20240110135407341" style="zoom:80%;" />

* 案例5：删除已经设置的任务，atrm编号    `atrm 5`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240110140023533.png" alt="image-20240110140023533" style="zoom:80%;" />



## 12-Linux磁盘分区、挂载

### 12.1 原理介绍

1.Linux无论有几个分区，分给哪一个目录使用，它归根结底就只有一个根目录，一个独立且唯一的文件结构，Linux中每个分区都是用来组成整个文件系统的一部分

2.Linux采用了一种叫“载入”的处理方法，它的整个文件系统包含了一整套的文件和目录，且将一个分区和一个目录联系起来。这时要载入的一个分区将使它的存储空间在一个目录下获得

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111133905769.png" alt="image-20240111133905769" style="zoom:67%;" />

### 12.2 查看所有设备挂载情况

**命令**：`lsblk` 或 `lsblk -f`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111133253958.png" alt="image-20240111133253958" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111133320708.png" alt="image-20240111133320708" style="zoom:80%;" />

### 12.3 硬盘说明

1.Linux硬盘分IDE硬盘和SCSI硬盘，目前基本上是SCSI硬盘。

2.对于IDE硬盘，驱动器标识符为"hdx~"，其中"hd"表明分区所在设备的类型，这里是指IDE硬盘。"x"为盘号（a为基本盘，b为基本从属盘，c为辅助主盘，d为辅助从属盘），"~"代表分区，前四个分区用数字1-4表示，它们是主分区或扩展分区，从5开始就是逻辑分区。例：hda3表示为第一个IDE硬盘上的第三个主分区或扩展分区，hdb2表示为第二个IDE硬盘上的第二个主分区或扩展区。

3.对于SCSI硬盘则标识为"sdx~"，SCSI硬盘是用"sd"来表示分区所在设备的类型的，其余则和IDE硬盘的表示方法一样。

### 12.4 挂载的经典案例

#### 虚拟机增加硬盘步骤2

分区命令：`fdisk /dev/sdb`

开始对/sdb分区

> m：命令显示列表
> p：显示磁盘分区
> n：新增分区
> d：删除分区
> w：写入并退出
> 说明：开始分区后输入n，新增分区，然后选择p，分区类型为主分区。两次回车默认剩余全部空间。最后输入w写入分区并退出，若不保存退出输入q

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111152731863.png" alt="image-20240111152731863" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111152754988.png" alt="image-20240111152754988" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111152854194.png" alt="image-20240111152854194" style="zoom:80%;" />

#### 虚拟机增加硬盘步骤3

格式化磁盘

分区命令：`mkfs -t ext4 /dev/sdb1`

其中ext4是分区类型

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111153012667.png" alt="image-20240111153012667" style="zoom:80%;" />

#### 虚拟机增加硬盘步骤4

挂载：将一个分区与一个目录联系起来

`mount 设备名称 挂载目录`

例如：`mount /dev/sdb1 /newdisk``

``umount 设备名称 或者 挂载目录`

例如：`umount /dev/sdb1` 或 `umount /newdisk`

注意：用命令行挂载重启后会失效

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111153238273.png" alt="image-20240111153238273" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111153301250.png" alt="image-20240111153301250" style="zoom:80%;" />

#### 虚拟机增加硬盘步骤5

永久挂载：通过修改/etc/fstab实现挂载

添加完成后执行mount -a即刻生效

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111154335525.png" alt="image-20240111154335525" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111154421100.png" alt="image-20240111154421100" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111154352367.png" alt="image-20240111154352367" style="zoom:80%;" />

### 12.5 磁盘情况查询

#### 12.5.1 查询系统整体磁盘使用情况

**基本语法**：`df -h`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111154708291.png" alt="image-20240111154708291" style="zoom:80%;" />

#### 12.5.2 查询指定目录的磁盘占用情况

**基本语法**：`du -h`

查询指定目录的磁盘占用情况，默认为当前目录

> -s：指定目录占用大小汇总
> -h：带计量单位
> -a：含文件
> --max-depth=1：子目录深度
> -c：列出明细的同时，增加汇总值

* 案例：查询/opt目录的磁盘占用情况，深度为1

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111155757063.png" alt="image-20240111155757063" style="zoom:80%;" />

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111155821326.png" alt="image-20240111155821326" style="zoom:80%;" />

### 12.6 磁盘情况-工作实用命令

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111161615763.png" alt="image-20240111161615763" style="zoom:80%;" />

#### 1.统计/opt文件夹下文件的个数

`ls -l /opt | grep "^-" | wc -l`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111161636768.png" alt="image-20240111161636768" style="zoom:80%;" />

#### 2.统计/opt文件夹下目录的个数

`ls -l /opt | grep "^d" | wc -l`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111161759294.png" alt="image-20240111161759294" style="zoom:80%;" />

#### 3.统计/opt文件夹下文件的个数，包括子文件夹里的

`ls -lR /opt | grep "^-" | wc -l`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111161830331.png" alt="image-20240111161830331" style="zoom:80%;" />

#### 4.统计/opt文件夹下目录的个数，包括子文件加里的

`ls -lR /opt | grep "^d" | wc -l`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111161904218.png" alt="image-20240111161904218" style="zoom:80%;" />

#### 5.以树状显示目录结构

`tree 目录`

> 若提示未找到命令，则先执行 **yum install tree**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240111162101229.png" alt="image-20240111162101229" style="zoom:80%;" />



## 13-Linux网络配置

### 13.1 ifconfig查看Linux网络配置

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240112135007752.png" alt="image-20240112135007752" style="zoom:80%;" />

### 13.2 ping测试主机之间网络连通性

**基本语法**：`ping 目的主机`

* 案例：测试当前服务器是否可以连接百度	`ping www.baidu.com`

### 13.3 指定ip

直接修改配置文件来指定IP，并可以连接到外网

编辑 `vim /etc/sysconfig/network-scripts/ifcfg-ens33`

要求：将ip地址配置的静态的，比如：ip地址为192.168.200.130

**ifcfg-ens33文件说明**

```
修改以下位置
BOOTPROTO="static"
# IP地址
IPADDR=192.168.200.130
# 网关
GATEWAY=192.168.200.2
# 域名解析器
DNS1=192.168.200.2
```

**重启网络服务或重启系统生效**

`service network restart` 或 `reboot`

### 13.4 设置主机名和hosts映射

#### 13.4.1 设置主机名

* 为了方便记忆，可以给Linux系统设置主机名，也可以根据需要修改主机名
* 指令`hostname`，查看主机名
* 修改文件在/etc/hostname中指定    `vim /etc/hostname`
* 修改后重启生效

#### 13.4.2  设置host映射

思考：如何通过主机名找到（ping）某个Linux系统

* windows

    > 在C:\Windows\System32\drivers\hosts文件指定即可，然后ping liang

    * 案例：192.168.200.130 liang

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240112145133974.png" alt="image-20240112145133974" style="zoom:80%;" />

* Linux

    > 在/etc/hosts文件指定    `vim /etc/hosts`

    * 案例：192.168.200.1 LAPTOP

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240112145606797.png" alt="image-20240112145606797" style="zoom:80%;" />

    

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240112151100064.png" alt="image-20240112151100064" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240112151123250.png" alt="image-20240112151123250" style="zoom:80%;" />



## 14-进程管理

### 14.1 基本介绍

1.在Linux中，每个执行的程序都称为一个进程，每一个进程都分配一个ID号（PID，进程号）

2.每个进程都可能以两种方式存在，前台与后台。所谓前台进程就是用户目前的屏幕上可以进行操作的；后台进程则是实际在操作，但是屏幕上无法看到的进程，通常使用后台方式执行。

3.一般系统的服务都是以后台进程的方式存在，而且都会常驻在系统中，知道关机才结束。

### 14.2 显示系统执行的进程

#### 14.2.1 基本介绍

`ps`命令是用来查看目前系统中，有哪些正在执行，以及它们执行的情况，可以不加任何参数

**ps显示的信息项**

| 字段     | PID            | TTY          | TIME                | CMD                        |
| -------- | -------------- | ------------ | ------------------- | -------------------------- |
| **说明** | **进程识别号** | **终端机号** | **进程占用CPU时间** | **正在执行的命令或进程名** |

> 可选参数：
> ps -a：显示当前终端的所有进程信息
> ps -u：以用户的格式显示进程信息
> ps -x：显示后台进程运行的参数

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240113151625309.png" alt="image-20240113151625309" style="zoom:80%;" />

#### 14.2.2 ps详解

##### 1.指令：ps -aux | grep xxx，比如查看sshd服务

##### 2.指令说明

> System V：展示风格
> USER：用户名称
> PID：进程号
> %CPU：进程占用CPU百分比
> %MEM：进程占用物理内存百分比
> VSZ：进程占用的虚拟内存大小（单位：KB）
> RSS：进程占用的物理内存大小（单位：KB）
> TT：终端名称。缩写
> STAT：进程状态，其中S-睡眠，s-表示该进程是会话的先导进程，N-表示进程拥有比普通优先级更低的优先级，R-正在运行，D-短期等待，Z-僵死进程，T-被跟踪或者被停止进程
> STARTED：进程的启动时间
> TIME：CPU时间，即进程使用CPU的总时间
> COMMAND：启动进程所用的命令和参数，如果过长会被截断显示

#### 14.2.3 应用实例

要求：以全格式显示当前所有的进程，查看进程的父进程

`ps -ef`以全格式显示当前所有的进程，-e 显示所有进程，-f 全格式

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240113153546717.png" alt="image-20240113153546717" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240113155625451.png" alt="image-20240113155625451" style="zoom:80%;" />

### 14.3 终止进程kill和killall

#### 14.3.1 介绍

若某个进程执行一半需要停止时，或者已消耗很大的系统资源时，此时可以考虑停止该进程。

#### 14.3.2 基本语法

`kill [选项] 进程号`	通过进程号杀死进程
`killall 进程名`=		通过进程名杀死进程，也支持通配符，这在系统因负载过大而变得很慢时很有用

> 常用选项：
> -9：表示强迫进程立即停止

#### 14.3.3 最佳实践

* 案例1：踢掉某个非法登录用户

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240113174650009.png" alt="image-20240113174650009" style="zoom:80%;" />

    `kill 5508`

* 案例2：终止远程    `kill 1102`

    * 重启sshd服务`/bin/systemctl start sshd.service`

* 案例3：终止多个gedit    `killall gedit`

* 案例4：强制杀掉一个终端    `kill -9 3097`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240113175520819.png" alt="image-20240113175520819" style="zoom:80%;" />

    

#### 14.3.4 查看进程树

**基本语法**：`pstree [选项]`

> 常用选项：
> -p：显示进程的PID
> -u：显示进程的所属用户

* 案例1：树状显示进程pid    `pstree -p`
* 案例2：树状显示进程的用户    `pstree -u`



## 15-服务管理

### 15.1 介绍

服务（service）本质就是进程，但是是运行在后台的，通常会监听某个端口，等待其他程序的请求，比如mysql、sshd、防火墙等，因此又称为守护进程。

### 15.2 service管理指令

`service 服务名 [start | stop | reload | status]`

> 在CentOS7.0以后很多服务不再使用service，而是systemctl

* service指令管理的服务在/etc/init.d查看

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114144632781.png" alt="image-20240114144632781" style="zoom:80%;" />

#### 15.2.1 service管理指令案例

* 请使用service指令，查看、关闭、启动network

    > 查看	 `service network status`
    > 关闭	`service network stop`
    > 启动    `service network start`

### 15.3 服务的运行级别

Linux有7种运行级别

> 运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动
> 运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登录
> 运行级别2：多用户状态（没有NFS），不支持网络
> 运行级别**3**：完全的多用户状态（有NFS），无界面，登录后进入控制台命令模式
> 运行级别4：系统未使用，保留
> 运行级别**5**：X11控制台，登陆后进入图形GUI界面
> 运行级别6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动

#### 15 .4.1 CentOS7后运行级别说明

在/etc/inittab，进行了简化，如下

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114150923561.png" alt="image-20240114150923561" style="zoom:80%;" />

* 查看当前运行级别`systemctl get-default`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114151058820.png" alt="image-20240114151058820" style="zoom:80%;" />

* 设置运行级别    `systemctl set-default multi-user.target`

### 15.4 chkconfig指令

#### 15.4.1 介绍

* 通过chkconfig命令可以给服务的各个运行级别设置自启动/自关闭
* chkconfig指令管理的服务在/etc/init.d查看
* CenOS7以后，很多服务使用systemctl管理

#### 15.4.2 chkconfig基本语法

查看服务 `chkconfig --list [| grep xxx]`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114160603115.png" alt="image-20240114160603115" style="zoom:80%;" />

`chkconfig 服务名 --list`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114160703867.png" alt="image-20240114160703867" style="zoom:80%;" />

`chkconfig --level 5 服务名 on/off`

#### 15.4.3 案例

* 对network服务进行各种操作`chkconfig --level 3 network off`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114160918917.png" alt="image-20240114160918917" style="zoom:80%;" />

> 使用细节：chkconfig重新设置服务后会自启动或关闭，需要重启（reboot）生效

### 15.5 systemctl管理指令

#### 15.5.1 基本语法

`systemctl [start | stop | restart | status] 服务名`

> systemctl 指令管理的服务在/usr/lib/systemd/system查看

#### 15.5.2 systemctl设置服务的自启动状态

1.`systemctl list-unit-files [| grep 服务名]`	查看服务开机启动状态，grep进行过滤

2.`systemctl enable 服务名`	设置服务开机自启动

3.`systemctl disable 服务名`	关闭服务开机启动

4.`systemctl is-enabled 服务名`	查看某个服务是否是自启动的

#### 15.5.3 案例

查看当前防火墙状况，关闭防火墙和重启防火墙

`systemctl status firewalld`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114162506859.png" alt="image-20240114162506859" style="zoom:80%;" />

`systemctl stop firewalld`

`systemctl restartfirewalld`

* 细节讨论

    > 关闭或者启用防火墙后，立即生效|
    > 这种方式只是临时生效，当重启系统后，还是回归以前对服务的设置
    > 如果希望设置某个服务自启动或关闭永久生效，要使用**`systemctl [enable|disable] 服务`**

### 15.6 打开/关闭指定端口

在生产环境中，往往需要将防火墙打开，但如果把防火墙打开，那么外部请求数据包就不能跟服务器监听端口通讯，这时，需要打开指定端口，比如80、8080等。

#### 15.6.1 firewall指令

打开端口：`firewall-cmd --permanent --add-port=端口号/协议`

关闭端口：`firewall-cmd --permanent --remove-port=端口号/协议`

**重新载入才能生效  `firewall-cmd --reload`**

查询端口是否开放：`firewall-cmd --query-port=端口号/协议`

#### 15.6.2 应用案例

* 案例1：启用防火墙。测试111端口是否能telnet

* 开放111端口    `firewall-cmd --permanent --add-port=111/tcp`   `firewall-cmd --reload`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114164731714.png" alt="image-20240114164731714" style="zoom:80%;" />

* 关闭111端口  `firewall-cmd --permanent --remove-port=111/tcp`   `firewall-cmd --reload`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240114165036594.png" alt="image-20240114165036594" style="zoom:80%;" />

### 15.7 动态监控进程

#### 15.7.1 介绍

top与ps命令很相似，它们都用来显示正在执行的进程。top与ps最大的不同。在于top在执行一段时间可以更新正在运行的进程

#### 15.7.2 基本语法

`top [选项]`

> 选项说明：
> 	-d：指定top命令每隔几秒更新，默认3秒
> 	-i：使top不显示任何闲置或者僵死进程
> 	-p：通过指定监控进程ID来仅仅监控某个进程的状态

> 交互操作说明
>
> P：以CPU使用率排序，默认此项
> M：以内存使用率排序
> N：以PID排序
> q：退出top

#### 15.7.3 应用实例

* 案例1：监视特定用户。`top`：输入此命令，按回车键，查看执行的进程；`u`：然后输入u回车，再输入用户名，即可
* 案例2：终止指定的进程。`top`：输入此命令，按回车键，查看执行的进程；`k`：然后输入k回车，再输入要结束的进程ID号
* 案例3：指定系统状态更新的时间(每隔10s自动更新)    `top -d 10`

### 15.8 监控网络状态

#### 15.8.1 基本语法

`netstat [选项]`

> 选项说明：
> 	-an：按一定顺序排列输出
> 	-p：显示哪个进程在调用

#### 15.8.2 应用案例

* 查看服务名为sshd的信息

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240115135912846.png" alt="image-20240115135912846" style="zoom:80%;" />

**检测主机连接命令ping**

是一种网络检测工具，主要用于检测远程主机是否正常，或是两部主机间的网线或网卡故障。



## 16-RPM与YUM

### 16.1 rpm包的管理

#### 16.1.1 介绍

rpm用于互联网下载包的打包及安装工具，它包含在某些Linux分发版中。它生产具有.RPM扩展名的文件，RPM是RedHat Package Manager(RedHat软件包管理工具)的缩写，类似windows的setup.exe。

#### 16.1.2 rpm包的简单查询指令

查询已安装的rpm列表	`rpm -qa | grep xx`

举例：查看当前系统是否安装firefox

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240115141904368.png" alt="image-20240115141904368" style="zoom:80%;" />

#### 16.1.3 rpm包名基本格式

firefox-102.15.0-1.el7.centos.x86_64

> 名称：firefox
> 版本号：102.15.0-1
> 适用操作系统：el7.centos.x86_64，表示CentOS7.x的64位系统
> 如果是i686、i386表示32位系统，noarch表示通用

#### 16.1.4 rpm其他查询指令

* 查询安装的所有rpm软件包`rpm -qa`

* 查询软件包是否安装`rpm -q 软件包名`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240115143701219.png" alt="image-20240115143701219" style="zoom:80%;" />

* 查询软件包信息`rpm -qi 软件包名`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240115143802132.png" alt="image-20240115143802132" style="zoom:80%;" />

* 查询软件包中的文件`rpm -ql 软件包名`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240115143926162.png" alt="image-20240115143926162" style="zoom:80%;" />

* 查询文件所属的软件包`rpm -qf 文件全路径名`  `rpm -qf /etc/passwd`    `rpm -qf /root/install.log`

#### 16.1.5 卸载rpm包

**基本语法**：`rpm -e RPM包的名称`  // erase

* 案例：删除firefox安装包	`rpm -e firefox`

> 细节讨论：
> 若其他包依赖于要卸载的软件包，卸载时会产生错误信息。若想强制删除，可以增加参数 --nodeps，但不推荐，可能造成程序无法运行。`rpm -e --nodeps foo`

#### 16.1.6 安装rpm包

**基本语法**：`rpm -ivh RPM包全路径名称`

> **参数说明：**
> 	i：install安装
> 	v：verbose提示
> 	h：hash进度条

### 16.2 yum

#### 16.2.1 介绍

yum是一个Shell前端软件包管理器，基于rpm包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖关系，并且一次性安装所有依赖的软件包。

#### 16.2.2 yum的基本指令

查询yum服务器是否有需要安装的软件`yum list | grep xxx`
安装指定的yum包`yum install xxx`

#### 16.2.3 yum应用实例

案例：使用yum安装firefox    `yum list | grep firefox` --> `yum install firefox`



## 17-搭建JavaEE环境

如果需要在Linux进行JavaE的开发，需要安装以下工具：

IDEA、JDK、MySQL

### 17.1 安装JDK

* 安装步骤

    > mkdir /opt/jdk
    > 通过Xftp上传到/opt/jdk下
    > cd /opt/jdk
    > 解压 tar -zxvf jdk-8u261-linux-x64.tar.gz
    > mkdir /usr/local/java
    > mv /opt/jdk/jdk1.8.0_261 /usr/local/java
    > 配置环境变量 vim /etc/profile
    > export JAVA_HOME=/usr/local/java/jdk1.8.0_261
    > export PATH=$JAVA_HOME/bin:$PATH
    > source /etc/profile

### 17.2 安装Tomcat

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240115152840295.png" alt="image-20240115152840295" style="zoom:80%;" />

## 18-Shell编程

* 脚本格式要求

    > 1.以#!/bin/bash开头
    > 2.脚本需要有可执行权限

* **脚本的执行方式**

    > 方式1：输入脚本的绝对路径或相对路径，**脚本需要有执行权限**。
    > 方式2：`sh 脚本`不用赋予脚本执行权限，直接执行即可。

* 编写一个脚本，输出hello world

    在目录/root/shcode下新建shell脚本hello.sh，写入如下内容

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116134751387.png" alt="image-20240116134751387" style="zoom:80%;" />

    给脚本加执行权限，执行**`./hello.sh`**或**`/root/shcode/hello.sh`**或**`sh hello.sh`**

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116135029938.png" alt="image-20240116135029938" style="zoom:80%;" />

### 18.1 Shell变量

#### 18.1.1 Shell变量介绍

Linux Shell中的变量分为**系统变量**和**用户变量**。系统变量：**$PATH**、**$HOME**、**$SHELL**、**$USER**等。显示当前shell所有变量：set

#### 18.1.2 shell变量的定义

**基本语法**：

> 定义变量：变量=值
> 撤销变量：unset 变量
> 声明静态变量：readonly变量，不可unset

* 案例1：定义变量A    `A=200`

* 案例2：撤销变量A    `unset A`

* 案例3：声明静态变量B=2，不能unset   `readonly B=2`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116144253127.png" alt="image-20240116144253127" style="zoom:80%;" />

    在/root/shcode目录下执行`./var.sh`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116144514750.png" alt="image-20240116144514750" style="zoom:80%;" />

**定义变量的规则**

> 1.变量名可以由字母、数字、下划线组成，但不能以数字开头
> 2.等号两侧不能有空格
> 3.变量名一般大写

**将命令的返回值赋值给变量**

> 1.A=`</date>`，将结果返回给变量A
> 2.A=$(date)等价于反引号
>
> <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116151431447.png" alt="image-20240116151431447" style="zoom:80%;" />
>
> <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116151456724.png" alt="image-20240116151456724" style="zoom:80%;" />

#### 18.1.3 设置环境变量

##### 基本语法

> **export 变量名=变量值		将shell变量输出为环境变量/全局变量**
> **source 配置文件				 让修改后的配置信息立即生效**
> **echo $变量名					  查询环境变量的值**

##### 快速入门

* 在/etc/profile文件定义TOMCAT_HOME环境变量

    1.编辑`vim /etc/profile`，添加如下内容

    ```shell
    export TOMCAT_HONE=/opt/tomcat
    ```

    2.`source /etc/profile`，使配置文件生效

* 查看环境变量TOMCAT_HOME的值

    3.`echo TOMCAT_HOME`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116152821759.png" alt="image-20240116152821759" style="zoom:80%;" />

* 在另外一个shell程序中使用TOMCAT_HOME

    4.`vim var.sh`，添加如下内容

    ```shell
    # 使用环境变量TOMCAT_HOME
    echo "tomcat_home=$TOMCAT_HOME"
    ```

    在/root/shcode下运行脚本`./var.sh`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116153403641.png" alt="image-20240116153403641" style="zoom:80%;" />

##### **shell脚本的多行注释**

```shell
# 将命令的返回值赋值给变量
:<<!
C=`date`
D=$(date)
echo "C=$C"
echo "D=$D"
!
```

### 18.2 位置参数变量

#### 18.2.1 介绍

当我们执行一个shell脚本时，如果希望获取命令行的参数信息，就可以使用位置参数变量。比如：`./myshell.sh 100 200`，这就是一个执行shell的命令行，可以在myshell脚本中获取到参数信息。

#### 18.2.2 基本语法

`$n`	n为数字，$0代表命令本身，$1-9代表第一到第九个参数，十以上的参数需要用大括号包含，如${10}
`$*`	代表命**令行中的所有参数**，$*把所有的参数看成一个整体
`$@`	也代表**命令行中的所有参数**，不过$@把每个参数区分对待
`$#`	代表**命令行中的所有参数的个数**

#### 18.2.3 案例

编写一个shell脚本position.sh，在脚本获取到命令行的各个参数信息

1.进入/root/shcode目录	`cd /root/shcode`
2.`vim myshell.sh`

   ```shell
   #!/bin/bash
   echo "0=$0 1=$1 2=$2"
   echo "所有的参数=$*"
   echo "$@"
   echo "参数的个数=$#"
   ```

3.增加执行权限	`chmod 744 myshell.sh`
4.`./myshell.sh 100 200`
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116155518069.png" alt="image-20240116155518069" style="zoom:80%;" />

### 18.3 预定义变量

#### 18.3.1 基本介绍

即shell设计者事先定义好的变量，可以直接在shell脚本中使用

#### 18.3.2 基本语法

`$$`	当前进程的进程号
`$!`	后台运行的最后一个进程的进程号
`$?`	最后一次执行的目录的返回状态。如果这个变量的值为0，证明上一个目录正确执行；如果这个变量的值非0（具体哪个数，由命令自己决定），则证明上一个命令没有正确执行。

#### 18.3.3 案例

* 在一个shell脚本中简单使用预定义变量

1.进入/root/shcode目录	`cd /root/shcode`
2.`vim preVar.sh`

   ```shell
#!/bin/bash
echo "当前执行的进程id=$$"
# 以后台的方式运行一个脚本，并获取它的进程号
/root/shcode/myshell.sh &
echo "最后一个后台方式运行的进程id=$!"
echo "执行的结果=#?"
   ```

3.增加执行权限	`chmod 744 preVar.sh `
4.`./preVar.sh`
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116160739961.png" alt="image-20240116160739961" style="zoom:80%;" />

### 18.4 运算符

#### 18.4.1 基本语法

**`$((运算式))`** 或 **`$[运算式]`** 或 **`expr m + n`** **`expr m - n`** **`expr m \* n`** **`expr m / n`** **`expr m % n`**

> 注意expr运算符间要有空格，如果希望将expr的结果赋给某个变量，使用反引号``

#### 18.4.2 案例

* **案例1：计算(2+3)*4**

    1.进入/root/shcode目录	`cd /root/shcode`
    2.`vim oper.sh`

       ```shell
    #!/bin/bash
    # 案例1：计算(2+3)*4
    # 第一种方式
    RES1=$(((2+3)*4))
    echo "res1=$RES1"
    # 第二种方式
    RES2=$[(2+3)*4]
    echo "res2=$RES2"
    # 第三种方式
    TMP = `expr 2 + 3`
    RES3=`expr $TMP \* 4`
    echo "res3=$RES3"
       ```

    3.增加执行权限	`chmod 744 oper.sh `
    4.`./oper.sh`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116163009798.png" alt="image-20240116163009798" style="zoom:80%;" />

* **案例2：求出命令行的两个参数的和**

    1.`vim oper.sh`

       ```shell
    # 求出命令行的两个参数的和
    SUM=$[$1+$2]
    echo "sum=$SUM"
       ```

    2.`./oper.sh 20 50`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240116163351374.png" alt="image-20240116163351374" style="zoom:80%;" />

### 18.5 条件判断

#### 18.5.1 基本语法

`[ condition ]`注意condition前后要有空格
非空返回true，可使用$?验证（0为true，>1为false）

* 案例

> [ jntm ]	返回true
> [ ]			 返回false
> [ condition ] && echo OK || echo notok	条件满足执行后面的语句

#### 18.5.2 判断语句

字符串比较 =

* 两个整数的比较

    > **-lt 小于**	**-le 小于等于**	**-eq 等于**	**-gt 大于**	**-ge 大于等于**	**-ne 不等于**

* 按照文件权限进行判断

    > **-r 读权限**    **-w 写权限**    **-x 执行权限**

* 按照文件类型进行判断

    > **-f 文件存在并且是常规文件**    **-e 文件存在**    **-d 文件存在并且是目录**

#### 18.5.3 案例

* 案例1："ok"是否等于"ok"

    ```shell
    #!/bin/bash
    # 案例1："ok"是否等于"ok"
    if [ "ok" = "ok" ]
    then
            echo "equal"
    fi
    ```

* 案例2：23是否大于等于22

    ```shell
    # 案例2：23是否大于等于22
    if [ 23 -ge 22 ]
    then
            echo ">"
    fi
    ```

* 案例3：/root/shcode/aaa.txt目录中的文件是否存在

    ```shell
    # 案例3：/root/shcode/aaa.txt目录中的文件是否存在
    if [ -f /root/shcode/aaa.txt ]
    then
            echo "文件存在"
    fi
    ```

### 18.6 流程控制 

#### 18.6.1 单分支和多分支

##### **基本语法**：

```shell
if [ 条件判断式 ]
then
	代码
fi
# 多分支
if [ 条件判断式 ]
then
	代码
elif [ 条件判断式 ]
then
	代码
fi
```

注意：[ 条件判断式 ]，中括号和条件判断式之间必须有空格

* 案例：编写一个shell程序，如果输入的参数大于等于60，输出及格了；否则输出不及格

    ```shell
    #!/bin/bash
    if [ $1 -ge 60 ]
    then
            echo "及格了"
    elif [ $1 -lt 60 ]
    then
            echo "不鸡格"
    fi
    ```

    

#### 18.6.2 case语句

##### 基本语法

```shell
case $变量名 in
"值1")
如果变量的值等于值1，则执行程序1
;;
"值1")
如果变量的值等于值1，则执行程序1
;;
···其他分支
*)
如果变量的值都不是以上的值，则执行此程序
;;
esac
```

* 案例：当命令行参数是1时，输出周一，是2时，输出周二，其他情况输出other

    ```shell
    #!/bin/bash
    case $1 in
    "1")
            echo "周一"
    ;;
    "2")
            echo "周二"
    ;;
    *)
            echo "other"
    ;;
    esac
    ```

#### 18.6.3 for循环

##### **基本语法**

```shell
for 变量 in 值1 值2 值3
do
程序
done
```

* 案例1：打印命令行输入的参数(这里可以看出$*和$@的区别)

    ```shell
    #!/bin/bash
    # $*把输入的参数当成一个整体，所以只会输出一句话
    for i in "$*"
    do
            echo "num is $i"
    done
    # 使用$@来获取输入的参数，注意，这时是分别对待，所以有几个参数就输出几句
    for j in "$@"
    do
            echo "num is $j"
    done
    ```

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240117184404263.png" alt="image-20240117184404263" style="zoom:80%;" />

```shell
for (( 初始值;循环控制条件;变量变化))
do
程序
done
```

* 案例2：从1加到100的值输出显示

    ```shell
    #!/bin/bash
    SUM=0
    for(( i=1; i<=100; i++))
    do
            SUM=$[$SUM + $i]
    done
    echo "总和SUM=$SUM"
    ```

#### 18.6.4 while循环

##### 基本语法

```shell
while [ 条件判断式 ]
do
程序
done
# 注意while和[有空格，条件判断式和]也有空格
```

* 案例：从命令行输入一个数n，统计从1加到n值为多少

    ```shell
    #!/bin/bash
    SUM=0
    i=0
    while [ $i -le $1 ]
    do
            SUM=$[$SUM + $i]
            i=$[$i + 1]
    done
    echo "SUM=$SUM"
    ```

#### 18.6.5 read读取控制台输入

##### 基本语法

`read (选项)(参数)`

> 选项：
> 	-p：指定读取值时的提示符
> 	-t：指定读取值时等待的时间(秒)，如果没有在指定的时间内输入，将不再等待
> 参数：
> 	变量：指定读取的变量名

* 案例1：从控制台输入一个NUM1

    ```shell
    #!/bin/bash
    read -p "请输入NUM1：" NUM1
    echo "NUM1=$NUM1"
    ```

* 案例2：从控制台输入一个NUM2，在10秒内输入

    ```shell
    #!/bin/bash
    read -t  10 -p "请输入NUM2：" NUM2
    echo "NUM2=$NUM2"
    ```

### 18.7 函数

#### 18.7.1 函数介绍

shell编程和其他语言一样，有系统函数，也可以自定义函数，系统函数中，介绍以下两个。

#### 18.7.2 系统函数

##### basename

> **基本语法**：
> 	`basename [pathname] [suffix]`		**功能**：返回完整路径最后/的部分，常用于获取文件名
> 	`basename [string] [suffix]`		**功能**：删除所有的前缀包括最后一个'/'，然后将字符串显示出来
> 	suffix为后缀，如果suffix被指定了，basename会将pathname和string中的suffix去掉

* 案例：返回/home/aaa.test.txt的"test.txt"部分    `basename /home/aaa.test.txt`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240117201335734.png" alt="image-20240117201335734" style="zoom:80%;" />

##### dirname

> **基本语法**：`dirname 文件绝对路径`
> **功能**：从给定的绝对路径返回去掉文件名的剩余路径

* 案例：返回/home/aaa/test.txt的/home/aaa    `dirname /home/aaa/test.txt`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240117201827198.png" alt="image-20240117201827198" style="zoom:80%;" />

#### 18.7.3 自定义函数

##### 基本语法

```shell
[ function ] funname[()]
{
		Action;
		[return int;]
}
```

调用直接写函数名：funname [值]

* 案例：计算输入两个参数的和

    ```shell
    #!/bin/bash
    function getSum() {
    		SUM=$[$n1+$n2]
    		echo "SUM=$SUM"
    }
    
    # 输入两个值
    read -p "请输入第一个数n1：" n1
    read -p "请输入第二个数n2：" n2
    # 调用函数
    getSum $n1 $n2
    ```

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240117202853485.png" alt="image-20240117202853485" style="zoom:80%;" />

### 18.8 shell编程综合案例

#### 18.8.1 需求分析

> 1.每天凌晨2:30备份数据库jntm到/data/backup/db
> 2.备份开始和备份结束能够给出相应的提示信息
> 3.备份后的文件要求以备份时间为文件名，并打包成.tar.gz的形式，比如：2021-03-12_230201.tar.gz
> 4.在备份的同时，检查是否有10天前备份的数据库文件，如果有就将其删除

#### 18.8.2 

`vim mysql_db_backup.sh`

```shell
#!/bin/bash
# 备份目录
BACKUP=/data/backup/db
# 当前时间
DATETIME=$(date + %Y-%m_%d_%H%M%S)
# 数据库地址
HOST=localhost
# 数据库用户名
DB_USER=root
# 数据库密码
DB_PW=123456
# 备份的数据库名
DATABASE=jntm

# 创建备份目录，如果不存在就创建
[ ! -d "${BACKUP}/${DATETIME}" ] && mkdir -p "${BACKUP}/${DATETIME}"

# 备份数据库
mysqldump -u${DB_USER} -p${DB_PW} --host=${HOST} -q -R --datebases ${DATABASE} | gzip > ${BACKUP}/${DATETIME}/$DATETIME.sql.gz

# 将文件处理成.tar.gz
cd ${BACKUP}
tar zcvf $DATETIME.tar.gz ${DATETIME}

# 删除10天前的备份文件
find ${BACKUP} -atime +10 -name "*.tar.gz" -exec rm -rf {} \;
echo "备份数据库${DATEBASE}成功"
```

`chmod 744 mysql_db_backup.sh`
`crontab -e`，编辑以下内容

```shell
30 2 * * * /usr/sbin/mysql_db_backup.sh
```



## 19-Ubuntu

### 19.1 Ubuntu的root用户

#### 19.1.1 介绍

安装Ubuntu成功后，都是普通用户权限，并没有最高root权限，如果需要使用root权限，通常会在命令前加 sudo。

一般使用su 命令直接切换到root用户，但是如果没有给root设置初始密码，就会抛出`su:Authentication failure`

#### 19.1.2 给root设置初始密码

1.输入`sudo passwd`，接着输入两次密码
2.设置好密码后，输入`su root`，接着输入密码，切换到root用户。提示符**$代表一般用户**，**#代表root用户**
3.输入exit会退出root并返回一般用户

### 19.2 apt软件管理和远程登录

#### 19.2.1 apt软件操作的相关命令

> **`sudo apt-get update`		更新源**
> **`sudo apt-get install package`		安装包**
> **`sudo apt-get remove package`        删除包**
>
> `sudo apt-cache search package`		搜索软件包
> **`sudo apt-cache show package`        获取包的相关信息，如说明、大小、版本等**
> `sudo apt-get install package --reinstall`		重新安装包
>
> `sudo apt-get -f install`		修复安装
> `sudo apt-get remove package --purge`		删除包，包括配置文件
> `sudo apt-get build-dep package`        安装相关的编译环境
>
> `sudo apt-get upgrade`		更新已安装的包
> `sudo apt-get dist-upgrade`		升级系统
> `sudo apt-cache depends package`		了解该包依赖哪些包
> `sudo apt-cache rdepends package`		查看该包被哪些包依赖
> **`sudo apt-get source package`        下载该包的源代码**

##### apt换源

**清华大学开源软件镜像网站**    https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/，**注意选择版本**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240118181232280.png" alt="image-20240118181232280" style="zoom:80%;" />

* 安全起见，建议先备份文件

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240118181535648.png" alt="image-20240118181535648" style="zoom:80%;" />

1.切换到root用户，输入密码	`su root`
2.进入/etc/apt目录下	`cd /etc/apt`
3.将source.list替换为空	`echo '' > source.list`
4.编辑source.list，写入清华镜像（https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/）	`vi source.list`

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ bionic-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

5.更新源	`sudo apt-get update`

### 19.3 远程登录Ubuntu

和CentOS不一样，Ubuntu默认没有安装SSHD服务（使用netstat指令查看：apt install net-tools），因此无法远程登录

#### 19.3.1 安装sshd和启用

命令行输入`sudo apt-get install openssh-server`

执行上面指令之后，在当前Linux就安装了SSH服务端和客户端

执行`service sshd restart`，启动sshd服务，会监听端口22

#### 19.3.2 一台Linux远程登录另一台Linux

在创建服务器集群时，会使用到该技术

1.使用`ifconfig`命令查看ip地址
2.命令行输入：`ssh 用户名@IP`    注意：如果出现错误，查看是否有该文件 ~/.ssh/known_ssh，尝试删除文件
3.退出可用`exit`或`logout`



## 20-日志管理

### 20.1 基本介绍

1.日志文件是重要的系统信息文件，其中记录了许多重要的系统事件，包括用户的登录信息、系统的启动信息、系统的安全信息、邮件相关信息、各种服务相关信息。
2.日志对于安全来说也很重要，它记录了系统每天发生的各种事情，通过日志来检查错误发生的原因，或者收到攻击时攻击者留下的痕迹。

* **/var/log是系统文件日志的保存位置**

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240118193348849.png" alt="image-20240118193348849" style="zoom:80%;" />

### 20.2 常用的系统日志

| 日志文件              | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| **/var/log/boot.log** | 系统启动日志                                                 |
| **/var/log/cron**     | 记录与系统定时任务相关的日志                                 |
| /var/log/cups         | 记录打印信息的日志                                           |
| /var/log/dmesg        | 记录了系统在开机时内核自检的信息，也可以使用dmesg命令直接查看内核自检信息 |
| /var/log/btmp         | 记录错误登录的日志。这个文件是二进制文件，不能直接用vi查看，而是要使用lastb查看。命令如下：[root@localhost log]#lastb |
| **/var/log/lasllog**  | 记录系统中所有用户最后一次的登录时间的日志，这个文件也是二进制文件，要使用lasllog命令查看 |
| **/var/log/mailog**   | 记录邮件信息的日志                                           |
| **/var/log/message**  | 记录系统重要消息的日志，这个日志文件中会记录Linux中绝大多数重要信息。如果系统出现问题，首先要检查的就是这个日志文件。 |
| **/var/log/secure**   | 记录验证和授权方面的信息，只要设计账户和密码的程序都会记录，比如系统的登录、ssh登录、su切换用户、sudo授权，甚至添加用户和修改用户密码都会记录在这个日志文件中 |
| /var/log/wtmp         | 永久记录所有用户的登录、注销信息，同时记录系统的启动、重启、关机事件，是二进制文件，使用last命令查看 |
| **/var/log/ulmp**     | 记录当前已经登录的用户的信息。这个文件会随着用户的登录和注销而不断变化，只记录当前登录用户的信息。此文件不能用vi查看，而是使用w、who、users等命令查看 |

### 20.3 日志管理服务

* 查询Linux中的rsyslogd服务是否启动	`ps -aux | grep "rsyslogd" | grep -v "grep"`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240118201353521.png" alt="image-20240118201353521" style="zoom:80%;" />

* 查询rsyslogd服务的自启动状态    `systemctl list-unit-files | grep rsyslog`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240118201449370.png" alt="image-20240118201449370" style="zoom:80%;" />

### 20.4 配置文件

编辑文件的格式为：`*.*`，其中第一个\*代表日志类型，第二个\*代表日志级别

#### 20.4.1 日志类型

* 配置文件：/etc/rsyslog.cong

> auth									pam产生的日志
> authpriv							 ssh、ftp等的的登录信息的验证信息
> corn									事件任务相关
> kern									内核
> lpr										打印
> mail									 邮件
> mark(syslog)-rsylog		  服务内部的消息，时间标识
> news									新闻组
> user									 用户程序产生相关信息
> uucp									unix to unix copy主机间相关的通信
> local 1-7							自定义的日志设备

#### 20.4.2 日志级别

* 配置文件：/etc/rsyslog.cong

> debug			有调试信息，日志通信最多
> info				一般信息日志，最常用
> notice			最具有重要性的普通条件的信息
> warning		警告级别
> err				 错误级别，阻止某个功能或者模块不能正常工作的信息
> crit				严重级别，阻止整个系统或者整个软件不能正常工作的信息
> alert			 需要立即修改的信息
> emerg		 内核崩溃等重要信息
> none		什么都不记录

**注意：从上到下，级别从低到高，记录信息越来越少**

* 由日志服务rsyslogd记录的日志文件，格式包含以下4列

    > 1.事件产生的事件
    > 2.产生事件的服务器的主机名
    > 3.产生事件的服务名或程序名
    > 4.事件的具体信息

* 日志查看实例，查看/var/log/secure日志

#### 20.4.3 日志管理服务应用实例

* 在/etc/rsyslog.conf中添加一个日志文件/var/log/hsp.log，当有事件发送时（比如sshd服务相关事件），该文件会接收到信息并保存，演示重启、登录的情况，看看是否有日志保存。

1.`vim /etc/rsyslog.conf`，增加如下内容
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119132325776.png" alt="image-20240119132325776" style="zoom:80%;" />

2.`> /var/log/hsp.log`
3.`reboot`，使用ssh登录，接着查看日志内容`cat /var/log/hsp.log | grep sshd`
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119132702638.png" alt="image-20240119132702638" style="zoom:80%;" />



### 20.5 日志轮替

#### 20.5.1 基本介绍

日志轮替就是把旧的日志文件移动并改名，同时建立新的空日志文件，当旧日志文件超出保存的范围之后，就会进行删除。

#### 20.5.2 日志轮替文件命名

1.CentOS7使用logrotate进行日志轮替管理，要想改变日志轮替文件名字，通过/etc/logrotate.conf配置文件中"dateext"参数
2.如果配置文件中有"dateext"参数，那么日志会用日期来作为日志文件的后缀，例如：secure-20201010。这样日志文件不会重叠，也就不需要日志文件的改名，只需要指定保存日志个数，删除多余的日志文件即可。
3.如果配置文件中没有"dateext"参数，日志文件就需要改名了。当第一次进行日志轮替时，当前的"secure"日志会自动改名为"secure.1"，然后新建"secure"日志，用来保存新的日志。当第二次进行日志轮替时，"secure.1"会自动改名为"secure.2"，当前的"secure"会自动改名为"secure.1"，然后新建"secure"日志，用来保存新的日志，以此类推。

#### 20.5.3 logrotate配置文件

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119140739641.png" alt="image-20240119140739641" style="zoom:80%;" />

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119140750429.png" alt="image-20240119140750429" style="zoom:80%;" />

##### 参数说明

| 参数                    | 参数说明                                                     |
| ----------------------- | ------------------------------------------------------------ |
| daily                   | 日志的轮替周期是每天                                         |
| weekly                  | 日志的轮替周期是每周                                         |
| monthly                 | 日志的轮替周期是每月                                         |
| rotate 数字             | 保留的日志文件的个数，0代表没有备份                          |
| compress                | 日志轮替时，旧的日志进行压缩                                 |
| create mode owner group | 建立新日志，同时指定新日志的权限、所有者和所属组             |
| mail address            | 当日志轮替时，输出内容提供邮件发送到指定的邮件地址           |
| missingok               | 如果日志不存在，则忽略该日志的警告信息                       |
| notifempty              | 如果日志为空文件，则不进行日志轮替                           |
| minsize 大小            | 日志轮替的最小值，只有日志达到这个最小值才会轮替，否则就算事件到了也不会轮替 |
| 不轮替                  |                                                              |
| size 大小               | 日志只有大于指定大小时才会进行日志轮替，而不是按照时间轮替   |
| dateext                 | 使用日期作为日志轮替文件的后缀                               |
| sharedscripts           | 在此关键字之后的脚本只执行一次                               |
| prerotate/endscript     | 在日志轮替之前执行简本命令                                   |
| postrotate/endscript    | 在日志轮替之后执行简本命令                                   |

#### 20.5.4 把自己的日志加入日志轮替

* 方法1：直接在/etc/logrotate.conf配置文件中写入该日志文件的轮替策略
* 方法2：在/etc/logrotate.d目录中新建该日志的轮替文件，在该轮替文件中写入正确的轮替策略，因为该目录中的文件都会被"include"到主配置文件中，所以也可以把日志加入轮替。

推荐使用第二种方法，因为系统中需要轮替的日志非常多，如果全部写入/etc/logrotate.conf文件，那么这个文件的可管理性就会非常差，不利于文件的维护。

**/etc/logrotate.d轮替文件**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119145511520.png" alt="image-20240119145511520" style="zoom:80%;" />

进入/etc/logrotate.d目录下，`vim hsplog`，写入如下内容
```shell
/var/log/hsp.log
{
    missingok
    daily
    copytruncate
    rotate 7
    notifempty
}
```

#### 20.5.5 日志轮替机制原理

日志轮替之所以可以在指定的时间备份日志，是依赖系统定时任务。在/etc/cron.daily目录，就会发现这个目录中有logrotate文件（可执行），logrotate提供这个文件依赖定时任务完成的。
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119150245198.png" alt="image-20240119150245198" style="zoom:80%;" />

### 20.6 查看内存日志

journalctl可以查看内存日志，这里我们看看常用的指令

`journalctl`
`journalctl -n 3`
`journalctl --since 19:00 --until 19:10:10`    查看起始时间到结束时间的日期可加日期
`journalctl -p err`    报错日志
`journalctl -o verbose`    日志详细内容
`journalctl _PID=1245 _COMN=sshd`    查看包含这些参数的日志
或者`journalctl | grep sshd`

**注意：`journalctl `查看的是内存日志，重启清空**

#### 20.6.1 案例

* 使用journalctl | grep sshd 来看看用户登录清空，重启系统，再次查询，看看日志变化

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119163848340.png" alt="image-20240119163848340" style="zoom:80%;" />



## 21-备份与恢复

* 安装dump和restore

    > 如果Linux没有dump和restore指令，需要先执行`yun -y install dump`、`yum -y install restore`

### 21.1 使用dump完成备份

#### 21.1.1 基本介绍

dump支持分卷和增量备份（所谓增量备份是指备份上次备份后修改/增加过的文件，也称差异备份）

#### 21.1.2 语法

`dump [-cu] [-123456789] [-f <备份后文件名>] [-T <日期>] [目录或文件系统]`
`dump [] -wW`

> -c：创建新的归档文件，并将由一个或多个文件参数所指定的内容写入归档文件的开头
> -0123456789：备份的层级。0为最完整备份，会备份所有文件。若指定0以上的层级，则备份至上一次备份以来修改或新增的文件，到9后，可以再次轮替。
> -f <备份后文件名>：指定备份后文件名
> -j：调用bzlib库压缩备份文件，也就是将备份后的文件压缩成bz2格式，让文件更小
> -T <日期>：指定开始备份的时间与日期
> -u：备份完毕后，在/etc/dumpdares中记录备份的文件系统，层级，日期与时间等
> -t：指定文件名，若该文件已存在备份文件中，则列出名称
> -W：显示需要备份的文件及其最后一次备份的层级，时间，日期
> -w：与-W类似，但仅显示需要备份的文件

#### 21.1.3 案例

* 案例1：将/boot分区所有内容备份到/opt/boot.bak.bz2文件中，备份层级为0	`dump -0uj -f /opt/boot.bak.bz2 /boot`
* 案例2：在/boot目录下拷贝一个文件，备份层级为1，注意比较这次生成的备份文件boot1.bak有多大    `dump -1uj -f /opt/boot.bak1.bz2 /boot`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119190245218.png" alt="image-20240119190245218" style="zoom:80%;" />

### 21.2 使用restore完成恢复

#### 21.2.1 基本介绍

restore目录用来恢复已备份的文件，可以从dump生成的备份文件中回复原文件

#### 21.1.2 基本语法

`restore [模式选项] [选项]`

共有4个模式，不能混用，**在一次命令中只能指定一种**

> -C：使用对比模式，将备份的文件与已存在的文件相互对比
> -i：使用交互模式，在进行还原操作时，restore指令将依序询问用户
> -r：进行还原模式
> -t：查看模式，看备份文件有哪些文件

>  选项：-f <备份设备>：从指定的文件中读取备份数据，进行还原操作

#### 21.1.3 案例

* 案例1：比较备份文件和原文件的区别(先将hello.java改为hello100.java)    `mv /boot/hello.java /boot/hello100.java`

    `restore -C -f boot.bak1.bz2`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119193018458.png" alt="image-20240119193018458" style="zoom:80%;" />

* 案例2：restore命令查看模式，看备份文件有哪些数据/文件    `restore -t -f boot.bak0.bz2`
* 案例3：restore命令还原模式。注意细节：如果有增量备份，需要把增量备份文件也进行恢复，有几个增量备份文件，就要恢复几个，按顺序恢复即可。
    **`mkdir /opt/boottmp`**-->**`cd /opt/boottmp`**-->**`restore -r -f /opt/boot.bak0.bz2`**-->**`restore -r -f /opt/boot.bak1.bz2`**

* 案例4：restore命令恢复备份的文件或者整个目录的文件`restore -r -f 备份好的文件`

    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240119195238902.png" alt="image-20240119195238902" style="zoom:80%;" />



## 22-Linux可视化管理：webmin和bt运维工具

### 22.1 Webmin

#### 22.1.1 基本介绍

Webmin是功能强大的基于Web的Unix/Linux系统管理工具，管理员通过浏览器访问Webmin的各种管理功能并完成相应的管理操作。除了个版本的Linux以外还可用于：AIX、HPUX、Solaris、Unixware、Irix和FreeBSD等系统。

#### 22.1.2 安装webmin和配置

1.下载地址：http://download.webmin.com/download/yum/，用下载工具下载即可
2.安装：`rpm -ivh webmin-1.700-1.noarch.rpm`
3.重置密码 /usr/libexec/webmin/changepass.pl /etc/webmin root test，root是webmin的用户名，这里把webmin的root用户密码改成了test
4.修改webmin服务的端口号（默认10000，处于安全目的）`vim /etc/webmin/miniserv.conf`，将port=10000和listen=10000修改为其他端口
5.重启webmin

> **/etc/webmin/restart	重启**
> **/etc/webmin/start	启动**
> **/etc/webmin/stop	停止**

6.防火墙开放6666端口

```
firewall-cmd --zone=public --add-port=6666/tcp --permanent  # 配置防火墙开放6666端口
firewall-cmd --reload  # 更新防火墙配置
firewall-cmd --zone=public --list-ports  # 查看已开放的端口号
```

7.登录webmin

http://ip:6666，使用root账号和重置的密码test

### 22.2 bt（宝塔）

#### 22.2.1 基本介绍

bt宝塔Linux面板是提升运维效率的服务器管理软件，支持一键LAMP/LNMP/集群/监控/网站/FTP/数据库/JAVA等多项服务器管理功能。

#### 22.2.2 安装和使用

1.安装：`yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh`
2.安装成功后控制台显示登录地址，账户



## 23-Linux面试题

### 23.3 MySQL数据库忘记密码如何找回

**1.修改文件/etc/my.cnf	 `vim /etc/my.cnf`，添加下面一行**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120142341901.png" alt="image-20240120142341901" style="zoom:80%;" />
**2.重启mysqld服务	 `service mysqld restart`**
**3.登录MySQL     mysql -u root -p，输入空密码登录**
**4.使用数据库mysql	 `use mysql;`**
**5.修改user表的authentication_string字段     `update user set authentication_string=password("123456") where user='root';`**
**6.刷新	 `flush privileges;`**
**7.退出mysql，`exit`**
**8.再次编辑/etc/my.cnf，将添加的内容注释掉**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120143510632.png" alt="image-20240120143510632" style="zoom:80%;" />
**9.重启mysqld服务	 `service mysqld restart`，用新密码登录即可**



### 23.4 统计ip访问情况，要求分析nginx访问日志(access.log)，找出访问页面数量在前2位的ip

* access.log内容如下
    <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120144103052.png" alt="image-20240120144103052" style="zoom: 67%;" />

**1.使用awk按空格分割     `cat access.log | awk -F " "`，得到两列内容，$1代表第一列（即ip），$2代表第二列**
**2.将ip列输出并排序	 `cat access.log | awk -F " " '{print $1}' | sort`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120144552336.png" alt="image-20240120144552336" style="zoom: 67%;" />
**3.使用uniq对ip进行数量统计	 `cat access.log | awk -F " " '{print $1}' | sort | uniq -c`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120144830008.png" alt="image-20240120144830008" style="zoom:67%;" />
**4.使用sort的nr参数对数量从大到小排序     `cat access.log | awk -F " " '{print $1}' | sort | uniq -c | sort -nr`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120145136903.png" alt="image-20240120145136903" style="zoom:67%;" />

**5.使用head取前两条     `cat access.log | awk -F " " '{print $1}' | sort | uniq -c | sort -nr | head -2`**

![image-20240120145312702](D:\Software\Typora\复制的图片\typora-user-images\image-20240120145312702.png)



### 23.5 使用tcpdump监听本机，将来自ip 192.168.200.1，tcp端口为22的数据，保存输出到tcpdump.log，用来做数据分析

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120150245352.png" alt="image-20240120150245352" style="zoom:80%;" />



### 23.6 常用的nginx模块，有什么作用

**rewrite模块：实现重写功能**
**access模块：来源控制**
**ssl模块：安全加密**
**ngx_http_gzip_module模块：网络传输压缩模块**
**ngx_http_proxy_module模块：实现代理**
**ngx_http_upstream_module模块：实现定义后端服务器列表**
**ngx_cache_purge：实现缓存清除功能**



### 23.7 列举Linux高级命令，至少6个

**netstat 网络状态监控**
**top 系统运行状态**
**lsblk 查看硬盘分区**
**ps -aux 查看运行进程**
**chkconfig 查看服务启动状态**
**systemctl 管理系统服务** 



### 23.8 Linux查看内存、io读写、磁盘存储、端口占用、进程查看目录是什么

#### 23.8.1 查看内存

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120155258526.png" alt="image-20240120155258526" style="zoom: 80%;" />

#### 23.8.2 io读写

**`iotop`，如果没有该指令先下载（`yum install iotop`）**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120155557129.png" alt="image-20240120155557129" style="zoom:80%;" />

#### 23.8.3 磁盘存储

**`df -lh`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120155843484.png" alt="image-20240120155843484" style="zoom:80%;" />

#### 23.8.4 端口占用

**`netstat -tunlp`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120160046224.png" alt="image-20240120160046224" style="zoom:80%;" />

#### 23.8.5 进程查看

**`ps -aux | grep xxx`，grep可不加**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120160243569.png" alt="image-20240120160243569" style="zoom:80%;" />



### 23.9 使用Linux命令计算t2.txt第二列的和并输出

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120160548272.png" alt="image-20240120160548272" style="zoom: 80%;" />
**`cat t2.txt | awk -F " " '{sum+=$2} END {print sum}'`**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120160736016.png" alt="image-20240120160736016" style="zoom:80%;" />



### 23.10 shell脚本如何检查一个文件是否存在？并给出提示

```shell
if [ -f 文件名 ]
then
	echo "存在"
else
	echo "不存在"
fi
```



#### 23.11 写一个shell脚本，对文本t3.txt中无序的一列数字排序，并将其总和输出

```
9
8
7
6
5
4
3
2
10
```

**`sort -nr t3.txt | awk '{sum+=$0; print $0} END {print "和="sum}'`**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240120161659388.png" alt="image-20240120161659388" style="zoom:80%;" />



### 23.12 写出指令查找当前文件夹(/home)下所有文本文件包含“cat”的文件名称

**`grep -r "cat" /home | cut -d ":" -f 1`**



### 23.13 写出统计/home目录下所有文件个数和所有文件总行数的指令

**`find /home -name "*.*" | wc -l`，列出所有文件**

**`find /home -name "*.*" | xargs wc -l`，列出所有文件及每个文件的行数**



### 23.14 每天晚上10:30，打包站点目录/var/spool/mail备份到/home下（每次备份按时间上生成不同的备份包，比如按照年月日时分秒）

**1.编写脚本mail.sh    `vim mail.sh`**

```shell
#!/bin/bash
cd /var/spool/mail && /bin/tar zcf /home/mail-`date +%Y-%m-%d_%H_%M_%S`.tar.gz mail/
```

**2. 给脚本加执行权限     `chmod u+x /root/mail.sh`**

**2.加入任务	 `crontab -e`**

```shell
30 20 * * * /root/mail.sh
```

