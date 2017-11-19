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


13. 提交到远程仓库
    git push origin master

14. 从远程仓库下载
    git clone 用户名@ip：目录

15. 创建并切换分支
    git checkout -b <name>	=	git branch <name>
    		    			git checkout <name>

16. 查看当前分支
    git branch

17. 合并分支
    git merge <name>
    --no-ff参数可以屏蔽快速合并，这种方式会创建一个commit，之前那种是会丢失合并信息的
    git log --graph可以看到图形的合并信息

18. 删除分支
    git branch -d <name>

19. debug分支
    当需要debug某个分支时，就在那个分支下创建一个debug分支，debug结束后合并、删除；
    而debug任务来时若自己手头的工作还未完成，不能commit，那么可以使用：20

20. 储藏当前分支的任务（工作现场）
    git stash

21. 查看储存的分支（工作现场）
    git stash list

22. 恢复工作现场
    两种方式：
    1. git stash apply <stash@{n}>	不会删除工作现场的记录，需要用git stash drop删除
    2. git stash pop   			恢复并删除

23. feature分支
    要实现新的功能，最好新建一个feature分支，在该分支上工作；
    如果最后在合并时发现这个功能不想要了，要删除feature分支，会提示还没有合并；
    强行删除需要-D参数，git branch -D <name>

------------------------------------------------------------------------------------------
多人协作
------------------------------------------------------------------------------------------
24. 查看远程仓库信息
    git remote
    -v 详细信息

25. 从远程clone
    从远程clone下来只能看到master分支，那么如何clone远程的dev分支到本地呢？
    git checkout -b dev origin/dev	从oringin的dev创建，并切换到本地dev分支

26. 两个人都在本地修改了dev，然后想推送到远程，这时后push的人会提示冲突，怎么办？
    git pull从远程将最新的拉下来，在本地完成合并；

    这时会提示pull不下来，原因是没有指定本地dev分支与远程origin/dev分支的链接；
    可以使用：
    git pull <remote> <local_branch>
    或
    git branch --set-upstream dev origin/dev

----------------------------------------------------------------------------------------
其他
----------------------------------------------------------------------------------------
27. 创建标签
    git tag <name>
    标签类似commit ID，便于管理，默认打在当前分支最新commit上；
    想对之前的commit打标签，使用
    git tag <name> <commit_ID>

28. 查看标签
    git tag
    git show <tagname>查看某个标签具体信息

29. 给标签添加说明
    git tag -a <tagname> -m '说明' <commit_ID>

30. 给一个标签签名
    加-s参数
    但是必须安装了GPG

31. 删除标签
    -d参数
    标签一般都是保存在本地的；

32. 将标签推送到远程
    git push origin <tagname>
    一次性推送所有未推送的标签
    git push origin --tags

33. 删除远程的标签
    先删除本地的；再push
    git push origin :refs/tags/<tagname>