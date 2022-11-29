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

git connit
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
 
