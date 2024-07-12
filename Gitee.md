# Gitee

## 1.Git-仓库操作

### 1.1 查看git版本

**指令**：**`git -v`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202201526324.png" alt="image-20240202201526324" style="zoom:80%;" />

### 1.2 创建仓库

#### 1.2.1 创建本地仓库

**1.创建文件夹local-rep-1**
**2.进入文件夹，右键点击`Open Git Bash here`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202202044242.png" alt="image-20240202202044242" style="zoom:80%;" />
**3.在命令行窗口输入`git init`**
<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202202338969.png" alt="image-20240202202338969" style="zoom:80%;" />

#### 1.2.2 克隆远程仓库

**指令：`git clone 仓库url`**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202203621460.png" alt="image-20240202203621460" style="zoom:80%;" />

##### 修改仓库克隆到本地的名称`git clone 仓库url 别名`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202204013438.png" alt="image-20240202204013438" style="zoom:80%;" />

#### 1.2.3 配置仓库

在克隆后的仓库右键，点击**`Open Git Bash here`**

**配置用户**：`git config user.name xiao-xiao-liang`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202204600814.png" alt="image-20240202204600814" style="zoom:80%;" />

**配置邮箱**：`git config user.email 2901815578@qq.com`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202204636218.png" alt="image-20240202204636218" style="zoom:80%;" />

在.git 文件夹中有一个config文件，刚才的配置保存到此文件中

**全局配置**：`git clone --global`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240202205815785.png" alt="image-20240202205815785" style="zoom:80%;" />

上面的配置保存到此文件中："C:\Users\ZL\.gitconfig"



## 2.文件操作

`git status`查看仓库状态

在仓库 local-rep-1 新建 a.txt文件，右键打开命令行，输入`git status`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203131126509.png" alt="image-20240203131126509" style="zoom:80%;" />

`git add`，将文件放到暂存区

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203131302465.png" alt="image-20240203131302465" style="zoom:80%;" />

`git commit -m 新增文件`，将文件从暂存区提交到仓库

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203131645704.png" alt="image-20240203131645704" style="zoom:80%;" />

### 2.1 误删除

#### 2.1.1 创建仓库local-rep-3

#### 2.1.2 右键打开git命令行，输入`git init`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203132351047.png" alt="image-20240203132351047" style="zoom:80%;" />

#### 2.1.3 在local-rep-3新建a.txt，执行`git add a.txt`，`git commit -m aaa`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203132511890.png" alt="image-20240203132511890" style="zoom:80%;" />

#### 2.1.4 将local-rep-3下的a.txt删除

#### 2.1.5 命令行输入`git restore a.txt`

即将文件从存储区恢复到工作区



> **如果将文件删除并且提交，可以恢复到文件删除之前的版本**

**1.删除a.txt**
**2.git add a.txt**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203133358882.png" alt="image-20240203133358882" style="zoom:80%;" />

**3.git commit -m dddd**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203133421641.png" alt="image-20240203133421641" style="zoom:80%;" />

**4.git log --oneline**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203133437914.png" alt="image-20240203133437914" style="zoom:80%;" />

**5.git reset --hard 版本号**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203133553900.png" alt="image-20240203133553900" style="zoom:80%;" />

但是会出现版本丢失的问题

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203133800832.png" alt="image-20240203133800832" style="zoom:80%;" />

要解决此问题，可以使用`git revert 版本号`



## 3.分支操作

### 3.1 新建文件夹local-rep-4

### 3.2 双击进入文件夹，右键打开git命令行

### 3.3 执行`git init`

### 3.4 创建分支`git branch 分支名称`

> 需要注意的是，创建分支需要先进行提交操作，因此如果是初始化之后的仓库，执行`git branch`会报错

#### 3.4.1 新建a.txt

#### 3.4.2 将文件放到暂存区

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203134748062.png" alt="image-20240203134748062" style="zoom:80%;" />

#### 3.4.3 将文件从暂存区放到存储区

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203134800036.png" alt="image-20240203134800036" style="zoom:80%;" />

#### 3.4.4 创建分支user

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203134927971.png" alt="image-20240203134927971" style="zoom:80%;" />

> **可在以下路径查看分支创建情况**
> **D:\test\local-rep-4\.git\refs\heads**
> <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203135029753.png" alt="image-20240203135029753" style="zoom:80%;" />

#### 3.4.5 查看分支情况

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203140520456.png" alt="image-20240203140520456" style="zoom:80%;" />

''*''代表当前所在分支

#### 3.4.6 切换分支

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203140657385.png" alt="image-20240203140657385" style="zoom:80%;" />

可以看到，已经成功切换到user分支

#### 3.4.7 创建分支并切换到分支

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203140900556.png" alt="image-20240203140900556" style="zoom:80%;" />

### 3.5 删除分支

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203141122521.png" alt="image-20240203141122521" style="zoom:80%;" />

### 3.6 合并分支及解决冲突

#### 3.6.1 在master添加c文件，并add、commit

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203141505572.png" alt="image-20240203141505572" style="zoom:80%;" />

#### 3.6.1 在order分支添加c文件，并add、commit

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203141700706.png" alt="image-20240203141700706" style="zoom: 80%;" />

#### 3.6.2 切换到master分支，`git merge order`

会提示冲突，人工判断一下，重新add、commit



## 4.标签操作

创建文件夹 local-rep-5，并初始化

添加a.txt文件，并add、commit

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203142338922.png" alt="image-20240203142338922" style="zoom:80%;" />

修改a.txt，并add、commit

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203142447891.png" alt="image-20240203142447891" style="zoom:80%;" />

添加b.txt，并add、commit

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203142611272.png" alt="image-20240203142611272" style="zoom:80%;" />

查看提交记录**`git log`**

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203142639514.png" alt="image-20240203142639514" style="zoom:80%;" />

> 这里发现版本号太长并且不知道某个版本具体做了什么操作，因此可以使用标签来进行标记
> <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203143218074.png" alt="image-20240203143218074" style="zoom:80%;" />
>
> 1
>
> <img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203143338352.png" alt="image-20240203143338352" style="zoom:80%;" />



## 5.远程仓库

`git remote add/rename/remove 名称 url`

<img src="D:\Software\Typora\复制的图片\typora-user-images\image-20240203143823248.png" alt="image-20240203143823248" style="zoom:80%;" />

提交代码到远程仓库

> 注意失败的话，需要ssh密码

ssh-keygen -t rsa -Cconfig中的url

`ssh-keygen -t rsa -Chttps://gitee.com/xiao-xiao-liang/Algorithm.git`

**密钥在C:\Users\ZL\\.ssh中**