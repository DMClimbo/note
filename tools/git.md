# git

git是目前世界上最先进的分布式版本控制系统，由linus用c语言编写。git跟踪并管理的是修改，而非文

件

​      

## 安装git 

[安装git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)

安装完git后需要做几件事来定制git环境，每台计算机只需配置一次， 程序升级时会保留配置信息。

> $ git config --global user.name "Your Name"
>
> $ git config --global user.email "email@example.com"

使用--global参数表示这台机器上所有git仓库都会使用这个配置，也可以对某个仓库指定不同的用户名和地址

​    

## 创建仓库

新建一个空目录，用git bash打开当前目录并输入`git init `把这个目录编程git可以管理的仓库 。

仓库建好后目录下会多一个`.git`目录，用来跟踪管理版本库，不能手动修改。

​       

## 将文件添加进仓库

所有版本控制系统只能跟踪文本文件的改动，比如TXT文件，网页和代码等等，但图片视频这些二进制

文件无法跟踪。而word格式是二进制格式，所以Git无法跟踪word文件，windows下不要使用自带的记

事本编辑任何文本文件，可能会报语法错误。

​        

- 用命令`git add` 告诉git，把文件添加到仓库

> $ git add README.md

- 用`git commit`告诉git,把文件提交到仓库

> $ git commit -m "wrote a README file"

-m后面输入的是本次提交的说明，方便在历史记录里找到改动记录，如果输入`git commit`导致出错，

需要打开.git文件夹，然后删除index.lock

​      

## 版本控制

`git status` 查看仓库当前状态

`git diff` 查看修改

`git log` 查看修改日志 ，按q退出

`git reset --hard HEAD^ `   版本回退，HEAD表示当前版本，上一个版本就是HEAD^,上上一个版本就是HEAD^^

 `git checkout  --  readme.md`表示把readme文件在工作区的修改全部撤销

​      

## 基本概念

- 工作区：在电脑里能看到的目录

- 版本库：工作区中的隐藏目录`.git` 。版本库里存了很多东西，其中最重要的就是称为stage（或者

index）的暂存区，还有自动创建的第一个分支master，以及指向master的一个指针叫做HEAD

​    

`git add`实际就是把文件修改添加到暂存区，`git commit`实际是把暂存区所有内容提交到当前分支。

一旦提交后，如果对工作区没做任何修改，那么工作区就是“干净的” 

​      

git是分布式版本控制系统，同一个git仓库，可以分布到不同的机器中，Github就是提供git仓库托管服

务的

​        

## 远程仓库

- 添加远程仓库点[这里](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)

- 推送&克隆

  > git push  origin master 
  >
  > git clone git@github.com:DMClimbo/note.git

- 参与Github开源项目

  在开源项目下点击“Fork”就在自己账号下克隆了一个相同的仓库，一定要从自己的账号下克隆才能

  推送修改。如果希望官方库能接受自己的修改，可以在Github上发起一个pull request。

  

