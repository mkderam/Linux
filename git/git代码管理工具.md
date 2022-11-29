### git的核心概念
1. 工作区：是个人或着开发着在本地计算机端锁看到的目录
2. 暂存区：也称索引，用于保存临时保存对资源的所有改动操作
3. 仓库去：又分为本地参考与远程仓库两类
### git 的常用命令
#### 帮助命令
```bash
git help
```
#### 仓库管理命令
```git
git init
功能：初始化Git仓库

git clone
功能： 复制仓库，默认只会复制master 分支
基本用法：
git clone remotes/origin/dev   #复制远程的dev分支
git clone xxx  dir_name				 #复制指定仓库到指定目录
git clone https://github.com/XXX/XXX.git  docgit

git add . 							#将所有修改提交至暂存区
git add xx							#将指定文件提交至暂存区

git commit
功能：提交暂存区文件到远程仓库
基本用法：
git commit -am "注释"   #提交时带上注释
```
#### 分支管理命令
```git
git branch
功能：创建分支
基本用法：
git branch branch_name			#创建具体分支
git branch 									#显示本地所有分支
git branch -d branch_name   #删除指定分支

git chenkout
功能： 切换分支
git chenkout branch_name

git pull
功能：拉去远程仓库所有分支仓库更新并合并到本地
git pull master master   #将远程仓库master 分支的更新拉去到本地，与本地master 分支合并

git push
功能：推送本地仓库所有分支更新到远程仓库
基本用法：
git push orign master      				#将本地分支推送到远程分支
git push -u origin master  				#将本地分支推送到远程分支(如无远程分支则创建，用于初始化仓库)
git push origin <local_branch> 		#创建远程分支，orgin是仓库名
git push origin <local_branch>:<remote_branch>   #创建远程分支
git push origin   :<remote_branch>			#先删除远程本地分支，然后删除远程分支


git merge 
功能：合并分支
基本用法：
git maerge '要合并的分支'  --allow-unrelated-histories
```
#### 查看操作命令
```git
git diff
功能：查看比较文件和版本之间的差异
基本用法：
git diff <file_name>										#查看当前文件和暂存区的文件差异
git diff <commit1><commit2>  dir_name		#比较两侧提交的的差异并输出到指定目录
git diff <branch1><branch2>  						#比较来个分支之间的差异
git diff --staged												#比较暂存区和版本之间差异
git diff --cached												#比较暂存区和版本库之间的差异
git diff --stat													#仅比较统计信息


git log
功能：查看提交记录
基本用法：
git log <file_name>										#查看当前文件每次提交记录
git log -p <file_name>								#查看每次详细修改内容的diff
git log -p -2													#查看最近两次详细修改的diff
git log  --stat												#查看提交统计的信息


git show
功能：用于显示类型的对象(一个或多个，比如标签，提交)
基本用法：
git show c18bf569											#显示某次改动的修改记录
git show v1.0.0											#显示标签v1.0.0以及标签指向的对象
git show v1.0.0  -s --format=s% v1.0.0^   #显示标签v1.0.0 指向的提交主题


git status
功能：用于显示工作目录和暂存区的状态
基本用法:
git status 命令显示的文件一共三种状态。
1.已添加暂存区，但没有提交的文件，也就是add 单没有commit 的文件
2.已修改，但没有添加到暂存区的文件
3.追踪到的文件
基本用法：
git status --ignored     			#可以查看被加入忽略文件中的文件
git status --short						#以简洁的方式输出信息

```
#### 其他命令
```git
git tag
功能：用于打标签和标记
基本用法：
git  tag  											#列出所有的标签
git tag v1.0.0  								#新建标签
git  tag -a v1.0.0  -m  ‘verson 1.0.0’    #新建带注释的标签

git remote
功能：用于查看关联的远程仓库信息
基本用法：
git remote												#显示所有关联的远程仓库名称
git remote -v											#显示所有关联的远程仓库名称 详细信息
git remote rename name1 name2     #重命名
git remote rm name								#删除远程仓库关联
git remote show origin						#查看指定管理仓库的信息
git remote add name url						#添加指定远程仓库
```
#### 全局设置命令
```git
git config
功能：命令用于获取并设置存储库或全局选项
基本用法：
git config --global user.name "xxx"
git config --global user.email "XXX@XXX.XXX"
git config --list 																#列出相关配置
```
### 使用git(windows) 远程推送到github
#### 第一次配置

1. 安装git(windows)

略

2. 创建github项目

略

3. 打开git bash

![image.png](https://cdn.nlark.com/yuque/0/2022/png/34405776/1669706924227-574da0aa-02a7-47a7-875b-70326e14817b.png#averageHue=%23ece7e6&clientId=ue9b97472-730c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=313&id=u1cd8d398&margin=%5Bobject%20Object%5D&name=image.png&originHeight=313&originWidth=279&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14049&status=done&style=none&taskId=u4bb6a001-28ef-4d88-a6b9-f33aa719ac9&title=&width=279)

4. 生成公钥私钥
```git
ssh-keygen -t rsa

```

5. 生成公钥私钥后在C:\Users\deram\.ssh 目录下找到id_rsa.pub 打开后复制公钥信息
6. 打开github设置

![image.png](https://cdn.nlark.com/yuque/0/2022/png/34405776/1669707281880-1321ea89-05ab-4b16-840a-c6c601d06e9a.png#averageHue=%2311161d&clientId=ue9b97472-730c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=277&id=u44e97e9d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=277&originWidth=342&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12275&status=done&style=none&taskId=u65453082-cb90-42c2-86d5-0f061c75e85&title=&width=342)![image.png](https://cdn.nlark.com/yuque/0/2022/png/34405776/1669707305012-bff3ce24-5d21-44ba-9663-be6b8b795e11.png#averageHue=%230e1219&clientId=ue9b97472-730c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=284&id=u526da8c6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=765&originWidth=1046&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54480&status=done&style=none&taskId=u79802a1a-fcab-400c-b944-1ef72d78ea2&title=&width=388)

7. 粘贴公钥信息

![image.png](https://cdn.nlark.com/yuque/0/2022/png/34405776/1669707398774-ff2daceb-cdcc-4f42-bcb7-c2c7eaa0d83c.png#averageHue=%230c1219&clientId=ue9b97472-730c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=294&id=u8bfcaab6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=539&originWidth=864&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46935&status=done&style=none&taskId=u9db91928-886f-49db-9afd-6c93115de39&title=&width=471)

8. 在git端创建自己的信息在代码提交时会用到此信息此信息保存在<git安装目录>/gitconfig，初始化git仓库
```git
git config --global user.name "xxx"
git config --global user.email "XXX@XXX.XXX"
git remote add '名字' 仓库git连接 

git init			#初始化一个目录为仓库
新建文件
git add
git commit  -am "注释"
git chenkout  main 
git push  -u origin main

```
