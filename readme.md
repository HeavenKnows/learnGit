# git 笔记

1. 创建git仓库
   git init

2. 把文件添加到仓库
   git add

3. 把文件提交仓库
   git commit

4. 查看仓库状态
   git status

5. 查看本文件和仓库版本的区别
   git diff

6. 查看git日志（commit 信息）
   git log

7. 版本回退
   git reset --hard HEAD^ 回到上个版本
       	     	    HEAD^^上上个版本
		    ...
   git reset --hard <commit ID>回到某次提交的版本

8. 查看使用的git命令的log
   git reflog
   在这里可以看到每次commit ID的前几位；

9. 工作区、暂存区、版本库
   在本地创建仓库的目录叫做：		工作区
   工作区内有一个.git隐藏目录叫做：	版本库
   版本库内有stage（或index）叫做：	暂存区
   版本库内还有master分支

   git add会把文件添加到暂存区，git commit会将暂存区的文件提交到当前分支；

   git管理的是修改，不是文件；

10. 撤销工作区的修改
    git checkout -- <file>

    命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

    一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

    -- 是必须加的，否则就变成了切换分支

11. 撤销添加到暂存区的修改
    git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区

12. 删除文件
    git rm <file>
    一般会直接从工作区删除文件；这时git status会显示delete；使用git rm并git commit从版本库中删除该文件

    如果在commit之后不小心删除了工作区的文件，可以用git checkout -- <file>找回文件
    git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
    记得只是版本库里的最新版本，提交之后修改的内容是找不回来的。


13. git push origin master

14. git clone 用户名@ip：目录

15. 创建并切换分支
    git checkout -b <name>	=	git branch <name>
    		    			git checkout <name>

16. 查看当前分支
    git branch

17. 合并分支
    git merge