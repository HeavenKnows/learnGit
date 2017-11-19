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