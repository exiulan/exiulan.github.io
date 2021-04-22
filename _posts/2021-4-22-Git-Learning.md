1.使用git的最小配置
配置user信息
git config --global user.name ""
git config --global user.name ""
缺省等同于 local
git config --local 对某个仓库有效
git config --global 对当前用户soy仓库有效
git config --system 对系统所有登录用户有效

显示config的配置，加--list
git config --list --local
2.建git仓库
两种场景
》把已有的项目代码纳入Git管理
$cd 项目代码到所在的文件夹
$git init
》新建的项目直接Git管理
$cd 某个文件夹
$git init your_project #会在当前路径下创建和项目明细同名的文件夹
$cd your_project
$git commit -m"Add"
$git status
$git add 文件夹
$git log
3.认识工作区和暂存区
工作目录——git add----暂存区-----git commit-----历史版本
git已经跟踪过的文件修改之后
git add -u提交到暂存区 git commit -m"提交信息"
4.git文件名变更文件名
常规步骤
  》重命名工作区文件名字
  》git add 重命名之后的文件
  》git rm 原文件名
  》git commit -m""
git reset --hard 清除暂存区和工作区变更
一键操作
git mv 原文件名 重命名的文件名
git commit -m""
5.查看历史记录
git log --oneline 查看简洁的历史记录
git log -n4 --oneline 查看最近4次简洁的记录
git log branch -av 查看有多少分支
git help --web log查看git log的帮助文档
git log 查看当前分支的信息
git log --all 查看所有分支的信息
git log --all --graph查看所有分支的父子关系
创建分支
git checkout -b 分支名 哪个分支信息
git commit -am"上传信息"
6.通过图形界面查看版本历史
gitk弹出界面
7.探秘.git目录
切换分支：git checkout 分支名
config：本地仓库配置的信息
HEAD:当前仓库工作分支
refs:包括heads和tag,heads包括所有分支，master里面存放的是一个object
git cat-file -t 5709642d 查看存放的类型
git cat-file -p 5709642d 查看存放的内容
5709642d是一个hash值 可以唯一标识一个对象
git branch -av 查看分支
objects目录：里面是文件夹名+hash值可以查看存放文件的内容及类型，packets是所有内容的打包存储
blob表示文件
7.commit、blob及tree之间的关系
commit --tree---tree-blob\tree
blob内容相同的文件
tree:表示文件
object对象包含一个commit
commit包括tree,tree下面是blob
8.分离头指针情况下的注意事项
分离头指针：变更没有指向任何分支
9.进一步理解HEAD和branch
比较两个文件差异
git diff  hash1 hash2
git diff HEAD HEAD^1 比较HEAD和其父亲
git diff HEAD HEAD~1 比较HEAD和其父亲
疑问：怎么创建分支，怎么合并分支，怎么打tag
分支是主干代码的一个拷贝，不增加新功能，只修复bug
tag也是主干代码的一份拷贝
10.怎么删除不需要的分支
git branch -d 分支名
git branch -D 分支名
11.怎么修改commit的message
git log -1 查看最近一次commit的信息
git commit --amend 对最近一次变更的commit信息做变更
git rebase -i 父commit信息：变更之前commit的信息
-------------------------------以上内容是在维护自己的分支上进行处理，没有集成到团队分支--------------------------------
    12.怎么把多个commit整理成1个
   git rebase -i 父commit信息：连续的多个commit整理成1个，连续多个的其余几个改为s
     git rebase -i 父commit信息：不连续的多个commit整理成1个,放在一起
    13.怎么比较暂存区和HEAD所含文件的差异
    git diff --cached 比较暂存区和HEAD所含文件的差异
    HEAD指向最后一次提交
  14.怎么比较暂存区和工作区所含文件的差异
   git diff:打印工作区和暂存区所有差异
   15.如何让暂存区恢复成和HEAD的一样
   git reset HEAD：暂存区文件全部恢复成HEAD一样（取消暂存）
     git reset HEAD -- 文件名：暂存区部分文件全部恢复成HEAD一样
  16.如何让工作区文件恢复为和暂存区一样
  git checkout -- 文件名：让工作区文件变更为和暂存区一样
  17.消除最近几次提交
  git reset --hard hash值
   18.看看不同提交的指定文件的差异
  git diff 分支名1 分支名2 -- 文件名：比较分支1和分支2中某个文件的差异
   19.正确删除文件的方法
   git rm 文件名：删除工作区和暂存区文件
   20.开发中临时加塞了紧急任务
git stash:存放文件stash
git stash apply:恢复文件到工作区，不会删除堆轧中文件
git stash list:查看stash中文件
git stash pop:恢复文件到工作区，删除stash中文件
21.如何指定不需要Git管理的文件
经过构建产生的文件，不需要放入git版本管理中，创建.gitignore文件
   如*.class、doc/，git不管理这些文件
22.如何将Git仓库备份到本地
常用的传输协议：
本地协议、http、https、ssh
智能协议和哑协议
--bare:不带工作区的裸仓库
哑协议：不显示进度
git clone --bare D:/learn/git_learning/.git ya.git
智能协议：显示进度
git clone --bare file://D:/learn/git_learning/.git zhineng.git
查看是否有远端仓库
git remote -v
创建远端仓库zhineng
git remote add zhineng file://D:\learn\backup\zhineng.git
同步本变更到本地其它的地方
git push zhinneg 
23.创建一个github账户
https://github.com
24.配置公私钥
头像下方有个help
add a new ssh key to your github account
ssh -keygen -t rsa -C "邮箱地址"
25.github创建个人仓库
创建repository
public:开放只读权限给其它人
26.把本地仓库同步到github
git remote -v 查看远端仓库
增加github站点：git remote add 远端仓库名 远端路径
fetch：下载
push:上传
git push 远端仓库名 --all:上传所有分支
git fetch 远端仓库名 分支名：下载
git branch -av：查看本地和远端分支
git push github master:上传master分支
fast-forwarts：分支与分支之间没有共同的祖先，非直推式方式
git pull:(fetch,远端分支和本地分支做merge)
git fetch 远端仓库名 分支名
合并历史独立的两颗树合并
git chectout 分支名
git merge --all-unrelated-histories github/分支名
rebase方法？？？？？？？，建立一条线性的分支
27.不同人修改了不同文件如何处理
不同人修改同一分支不同文件
空的工作区：
git clone 路径：拷贝文件到工作区
git clone 路径 文件：拷贝文件到工作区
git checkout -b 本地分支  远端分支：基于远端分支创建本地分支，并切换到本地分支
更新工作区变更到远端：
git add -u:添加到暂存区
git commit:提交到本地仓库
git push:提交到远端服务器
非空工作区：
git fetch 远端仓库名：更新本地工作区
git checkout -b 本地分支名 远端分支名：基于远端分支创建本地分支，并切换到本地分支（分支的hash值相同）
创建变更
git add -u:添加到暂存区
git commit:提交到本地仓库
git push:提交到远端服务器
假如本用户变更没有push，另一个用户变更了该分支的不同文件名且push（即远端和本地不是fast-forward）
git fetch 远端仓库名：更新本地工作区
git branch -av:提示 ahead 1,behind 1表示本用户有个commit，远端没有，远端有个commit，本地没有
git merge 远端分支名
git push 远端仓库名
28.不同人修改了相同分支同文件不同区域如何处理
git pull：本地和远端同步（同步远端仓库，更新本地仓库）
（git fetch;git merge 远端分支名）
29.不同人修改了相同分支同文件同区域如何处理
两个人修改了同一文件同一区域，其中一个人push完成后，另外一个人提交发生冲突的时候：
git pull:会报命令冲突
vi 文件名，沟通修改
git merge 远端分支名
git commit
git push
29.不同人修改了文件名和文件内容如何处理
两个人做变更，其中一个人修改了文件名，另一个人修改了文件内容
变更文件名：
git mv 文件原名 文件名修改后：变更文件名
git add -u
git commit
git push
变更文件内容
git commit
git pull
git push
两个人做变更，其中一个人修改了同1文件名，另一个人也修改了同1文件名
git pull:会出现两个文件名
git rm 文件名：删除其中一个文件名
git add 文件名
git commit
git push
30.禁止向集成分支执行push -f 操作
git push -f：不是fast-forward也能push,禁止使用
禁止向集成分支执行变更历史的操作？？？？？？
31.GITHUB的核心功能
文档（博客、wiki）、项目管理、集成（第三方提供）、团队管理、社会编码（开源）、存放代码等
MarketPlace
git 项目搜索
git 最好 学习 资料 in:readme stars:>1000
git 怎么搭建简洁的个人博客
blog easily start in:readme stars:>5000
fork到自己的目录中
新建组织？？？？

