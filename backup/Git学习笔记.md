# ---Git学习笔记---



----



# Git是什么？

Git 是一个免费的、开源的分布式版本控制系统，可以快速高效地处理从小型到大型的各种项目。

特点：

* 易于学习
* 体积小
* 性能极快



# 版本控制

版本控制是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统。

版本控制其实最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本，方便版本切换





# Git 常用命令

## 设置用户签名



命令：

```sh
git config --global user.name 用户名
git config --global user.email 邮箱
```

命令分别设置用户名和邮箱



只需要设置一次即可



签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看 到，以此确认本次提交是谁做的。Git 首次安装必须设置一下用户签名，否则无法提交代码。

这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系。





## 初始化本地库



命令：

```sh
git init
```



使用：

```sh
PS C:\Users\mao\Desktop\test> ls
PS C:\Users\mao\Desktop\test> git init
Initialized empty Git repository in C:/Users/mao/Desktop/test/.git/
PS C:\Users\mao\Desktop\test> ls
PS C:\Users\mao\Desktop\test> cd .git
PS C:\Users\mao\Desktop\test\.git> ls


    目录: C:\Users\mao\Desktop\test\.git


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2022/6/29     21:09                hooks
d-----         2022/6/29     21:09                info
d-----         2022/6/29     21:09                objects
d-----         2022/6/29     21:09                refs
-a----         2022/6/29     21:09            112 config
-a----         2022/6/29     21:09             73 description
-a----         2022/6/29     21:09             23 HEAD


PS C:\Users\mao\Desktop\test\.git> cd hooks
PS C:\Users\mao\Desktop\test\.git\hooks> ls


    目录: C:\Users\mao\Desktop\test\.git\hooks


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         2022/6/29     21:09            478 applypatch-msg.sample
-a----         2022/6/29     21:09            896 commit-msg.sample
-a----         2022/6/29     21:09           4655 fsmonitor-watchman.sample
-a----         2022/6/29     21:09            189 post-update.sample
-a----         2022/6/29     21:09            424 pre-applypatch.sample
-a----         2022/6/29     21:09           1643 pre-commit.sample
-a----         2022/6/29     21:09            416 pre-merge-commit.sample
-a----         2022/6/29     21:09           1374 pre-push.sample
-a----         2022/6/29     21:09           4898 pre-rebase.sample
-a----         2022/6/29     21:09            544 pre-receive.sample
-a----         2022/6/29     21:09           1492 prepare-commit-msg.sample
-a----         2022/6/29     21:09           2783 push-to-checkout.sample
-a----         2022/6/29     21:09           3650 update.sample


PS C:\Users\mao\Desktop\test\.git\hooks>
```





## 查看本地库状态



命令：

```sh
git status
```



使用：

```sh
PS C:\Users\mao\Desktop\test> git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
PS C:\Users\mao\Desktop\test>
```



新增一个文件：hello.txt

内容为123456



```sh
PS C:\Users\mao\Desktop\test> ls


    目录: C:\Users\mao\Desktop\test


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         2022/6/29     21:13              6 hello.txt


PS C:\Users\mao\Desktop\test>
```



再次查看：

```sh
PS C:\Users\mao\Desktop\test> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.txt

nothing added to commit but untracked files present (use "git add" to track)
PS C:\Users\mao\Desktop\test>
```







## 添加至暂存区



将工作区的文件添加到暂存区

命令：

```sh
git add 文件名
```



使用：

```sh
PS C:\Users\mao\Desktop\test> git add hello.txt
PS C:\Users\mao\Desktop\test>
```



查看状态：

```sh
PS C:\Users\mao\Desktop\test> git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   hello.txt

PS C:\Users\mao\Desktop\test>
```





## 提交到本地库



将暂存区的文件提交到本地库

命令：

```sh
git commit -m "日志信息" 文件名
```



使用：

```sh
PS C:\Users\mao\Desktop\test> git commit -m "第一次提交" hello.txt
[master (root-commit) 50e12c6] 第一次提交
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
PS C:\Users\mao\Desktop\test>
```



```sh
PS C:\Users\mao\Desktop\test> git status
On branch master
nothing to commit, working tree clean
PS C:\Users\mao\Desktop\test>
```



```sh
PS C:\Users\mao\Desktop\test> git log
commit 50e12c68902ad1e302203dfbaf1d27b4a7382a6d (HEAD -> master)
Author: mao <1296193245@qq.com>
Date:   Wed Jun 29 21:18:00 2022 +0800

    第一次提交
PS C:\Users\mao\Desktop\test>
```





## 历史版本

查看历史版本：



查看版本信息：

```sh
git reflog
```

查看版本详细信息：

```sh
git log
```





使用：

```sh
PS C:\Users\mao\Desktop\test> git reflog
50e12c6 (HEAD -> master) HEAD@{0}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test>
```

```sh
PS C:\Users\mao\Desktop\test> git log
commit 50e12c68902ad1e302203dfbaf1d27b4a7382a6d (HEAD -> master)
Author: mao <1296193245@qq.com>
Date:   Wed Jun 29 21:18:00 2022 +0800

    第一次提交
PS C:\Users\mao\Desktop\test>
```





## 版本穿梭



命令：

```sh
git reset --hard 版本号
```





使用：

添加两个提交：

```sh
PS C:\Users\mao\Desktop\test> git reflog
50e12c6 (HEAD -> master) HEAD@{0}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
12345
PS C:\Users\mao\Desktop\test> git commit -m "第二次提交" hello.txt
[master d5c5757] 第二次提交
 1 file changed, 2 insertions(+), 1 deletion(-)
PS C:\Users\mao\Desktop\test> git reflog
d5c5757 (HEAD -> master) HEAD@{0}: commit: 第二次提交
50e12c6 HEAD@{1}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
12345
1234
PS C:\Users\mao\Desktop\test> git commit -m "第三次提交" hello.txt
[master 4139c77] 第三次提交
 1 file changed, 1 insertion(+)
PS C:\Users\mao\Desktop\test> git reflog
4139c77 (HEAD -> master) HEAD@{0}: commit: 第三次提交
d5c5757 HEAD@{1}: commit: 第二次提交
50e12c6 HEAD@{2}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test> git status
On branch master
nothing to commit, working tree clean
PS C:\Users\mao\Desktop\test>
```



现在是第三个版本：

```sh
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
12345
1234
PS C:\Users\mao\Desktop\test>
```

```sh
PS C:\Users\mao\Desktop\test> git reflog
4139c77 (HEAD -> master) HEAD@{0}: commit: 第三次提交
d5c5757 HEAD@{1}: commit: 第二次提交
50e12c6 HEAD@{2}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test>
```



切换到第二个版本：

命令：

```sh
git reset --hard d5c5757
```

```sh
PS C:\Users\mao\Desktop\test> git reset --hard d5c5757
HEAD is now at d5c5757 第二次提交
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
12345
PS C:\Users\mao\Desktop\test>
```



切换到第一个版本：

```sh
PS C:\Users\mao\Desktop\test> git reset --hard 50e12c6
HEAD is now at 50e12c6 第一次提交
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
PS C:\Users\mao\Desktop\test>
```



切换回第三个版本：

```sh
PS C:\Users\mao\Desktop\test> git reflog
50e12c6 (HEAD -> master) HEAD@{0}: reset: moving to master
50e12c6 (HEAD -> master) HEAD@{1}: reset: moving to 50e12c6
d5c5757 HEAD@{2}: reset: moving to d5c5757
4139c77 HEAD@{3}: commit: 第三次提交
d5c5757 HEAD@{4}: commit: 第二次提交
50e12c6 (HEAD -> master) HEAD@{5}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test> git reset --hard 4139c77
HEAD is now at 4139c77 第三次提交
PS C:\Users\mao\Desktop\test> cat hello.txt
123456
12345
1234
PS C:\Users\mao\Desktop\test> git reflog
4139c77 (HEAD -> master) HEAD@{0}: reset: moving to 4139c77
50e12c6 HEAD@{1}: reset: moving to master
50e12c6 HEAD@{2}: reset: moving to 50e12c6
d5c5757 HEAD@{3}: reset: moving to d5c5757
4139c77 (HEAD -> master) HEAD@{4}: commit: 第三次提交
d5c5757 HEAD@{5}: commit: 第二次提交
50e12c6 HEAD@{6}: commit (initial): 第一次提交
PS C:\Users\mao\Desktop\test>
```







# Git 分支操作

