本文主要参考
<a href="https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000">git教程</a>


以及自己在实践中碰到的一些问题.
  

# 实习中碰到的问题及技巧

1. 删除远程库中不需要的文件:  首先删除本地库中的文件:rm命令  然后添加到git: git add --all     然后使用:git commit -m "commit相关说明"   最后push到远程库:git push origin master    即可
2. 删除远程库中不需要的分支:    git push origin --delete <name>  
  
3.在push之前merge错了,怎么办?比如你开发是拉的staging分支,但是你把dev分支merge进来了，push出错怎么办:

  0.先复制你的修改,以便于在第4步时直接将修改复制进去
  然后如下操作:
  1. 拉staging分支
  git checkout -b staging origin/staging
  git pull
  2. 删除你的旧分支
  git branch -D ssd-james
  3. 重新创建分支(基于staging)
  git checkout -b ssd-james
  4. 重新修改
  5. git commit -a -m 'add ssd life'
  6. 强制更新
  git push origin ssd-james --force（当远程没有ssd-james分支时，会提示你是否要提交merge request，merge到哪个分支）

4.公司的开发流程：
  
  0.git clone 
  1. 拉staging分支
  git checkout -b staging origin/staging
  git pull
  2. 重新自己的分支进行开发(基于staging)
  git checkout -b staging-james
  3. 修改代码
  4. git add   git commit
  5. push代码提交merge_request
  git push origin staging-james --force（当远程没有ssd-james分支时，会提示你是否要提交merge request，merge到哪个分支）
5.merge产生冲突时的解决：
    打开冲突文件，修改冲突部分，然后git commit,然后再merge

# 安装git
1. sudo apt-get install git
2. 安装完成后,需要设置你的名字与邮箱:
    - git config --global user.name "Your Name"
    - git config --global user.email "email@example.com"
    - 注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。


# 创建版本库
   - 版本库又名仓库(repository),可以理解为一个目录,这个目录里面的所有文件都可以被git管理起来,
   每个文件的修改删除git都能跟踪.创建版本库的步骤如下:
1. 使用mkdir命令在本地目录下创建一个空目录作为本地版本库的存储位置.
2. 在刚创建的目录下使用 git init命令初始化版本库,使该目录变成git管理的版本库.

3. 添加文件到git仓库:
   - git add <file>,注意,可反复多次使用,添加多个文件,也可以用git add -all 一次性添加所有.
   - git commit -m "需要说明的东西" 
  

# 时光机穿梭
(版本库的相关删除修改版本回退等操作)
1. 要随时掌握工作区的状态，使用git status命令。

2. 如果git status告诉你有文件被修改过，用git diff <文件名> 可以查看修改内容


## 版本回退

 1. HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。  (其中commit_id用git log命令可以查询   输入commit_id的时候只需要输入前四位即可)

 2. 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

 3. 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。


## 工作区和暂存区

 1. 工作区:你在电脑上能看到的目录,比如learngit文件夹就是一个工作区.

 2. 暂存区:

    - 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
   -    
![暂存区stage](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

   
    - 前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

        第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
        第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
        

## 管理修改

1. git跟踪并管理的是修改，而非文件：当修改同一文件时，如果不用git add到暂存区，那就不会加入到commit中！！
即：第一次修改--》git add-->第二次修改--》git commit    


## 撤销修改
1. 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

2. 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

3. 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考“版本回退”一节，不过前提是没有推送到远程库。


## 删除文件
1. 添加一个新文件test.txt到GIT并且提交：git add  git commit提交后，就在本地以及版本库均有文件了，
当用命令rm test.txt删除本地文件后，你可以有两个操作：
    - 可以用git checkout -- test.txt在版本库中找回你删除的本地库
    - 用git rm test.txt从版本库中删除该文件，并且git commit -m "remove test.txt"，之后文件就从版本库中删除了。



# 远程仓库
1. 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

      $ ssh-keygen -t rsa -C "youremail@example.com"
    你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

    如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

2. 第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

    然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

      github-addkey-1

    点“Add Key”，你就应该看到已经添加的Key：

      github-addkey-2

    - 为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

    - 当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了

## 添加远程库

    - 你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，
    这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作。做法如下：
   1. 登录github,新建一个repository,名字与本地文件名相同
   2. git remote add origin git@github.com:james/learngit.git
   3. 关联后，使用命令git push -u origin master第一次推送master分支的所有内容
   4. 此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改

**说明**：2.中git@...是你自己github的ssh链接。
         远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。
         3.中由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的          master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
     
## 从远程库克隆

- 假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

- 首先，登陆GitHub，创建一个新的仓库.
然后使用git clone 命令克隆：如git clone git@github.com:james/gitskills.git



# 分支管理

## 创建与合并分支
因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
Git鼓励大量使用分支：

   - 查看分支：git branch

   - 创建分支：git branch "name"

   - 切换分支：git checkout "name"

   - 创建+切换分支：git checkout -b "name"

   - 合并某分支到当前分支：git merge "name"

   - 删除分支：**本地**git branch -d "name"   **远程** git push origin --delete "name"

   - 博客里面画的分支图没太弄懂 

## 解决冲突

  1. 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

  2. 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

  3. 用git log --graph命令可以看到分支合并图。  
       - 详情：<a href="https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840202368c74be33fbd884e71b570f2cc3c0d1dcf000">

## 分支管理策略

   - 在实际开发中，我们应该按照几个基本原则进行分支管理：

1. 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

2. 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

3. 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![fenzhi](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)


**小结**
   - Git分支十分强大，在团队开发中应该充分应用。

   - 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。


## Bug分支
   - 当你手头工作没做完不能提交，然后要紧急解一个其他的bug那么就需要用到下面的方法：

        - 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

        - 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。


## Feature分支
  **添加新功能时的分支**

   - 每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

**小结**

   - 开发一个新feature，最好新建一个分支；  新建分支与之前的相同
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。


## 多人协作


### 推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git
就会把该分支提送到远程库对应的远程分支上：
比如想要推送dev分支到远程：
git push origin dev

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

### 抓取分支

多人协作时，大家都会往master和dev分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：

   $ git clone git@github.com:michaelliao/learngit.git
   
当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。不信可以用git branch命令看看：

$ git branch
* master

我用的是在同一哥电脑的另一个目录下做的测试,我这里出现了一个问题：在git branch 时出现如下问题：fatal: Not a git repository (or any of the parent directories): .git    使用git init命令即可解决。


现在，你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：

    $ git checkout -b dev origin/dev
现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程：

    $ git add env.txt

    $ git commit -m "add env"
    [dev 7a5e5dd] add env
     1 file changed, 1 insertion(+)
     create mode 100644 env.txt

    $ git push origin dev
    Counting objects: 3, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To github.com:michaelliao/learngit.git
    f52c633..7a5e5dd  dev -> dev

你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：

    $ cat env.txt
    env

    $ git add env.txt

    $ git commit -m "add new env"
    [dev 7bd91f1] add new env
    1 file changed, 1 insertion(+)
    create mode 100644 env.txt

    $ git push origin dev
    To github.com:michaelliao/learngit.git
    ! [rejected]        dev -> dev (non-fast-forward)
    error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
    hint: Updates were rejected because the tip of your current branch is behind
    hint: its remote counterpart. Integrate the remote changes (e.g.
    hint: 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

    $ git pull
    There is no tracking information for the current branch.
    Please specify which branch you want to merge with.
    See git-pull(1) for details.

    git pull <remote> <branch>

    If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：

    $ git branch --set-upstream-to=origin/dev dev
    Branch 'dev' set up to track remote branch 'dev' from 'origin'.
  再pull：

    $ git pull
    Auto-merging env.txt
    CONFLICT (add/add): Merge conflict in env.txt
    Automatic merge failed; fix conflicts and then commit the result.
这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：

    $ git commit -m "fix env conflict"
    [dev 57c53ab] fix env conflict

    $ git push origin dev
    Counting objects: 6, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
    Total 6 (delta 0), reused 0 (delta 0)
    To github.com:michaelliao/learngit.git
       7a5e5dd..57c53ab  dev -> dev
   
   多人协作的工作模式通常如下:
   1. 首先,试图用命令 git push origin <branch-name>推送自己的修改;
   2. 如果推送失败,有可能是远程分支比你的本地版本靠前,需要用git pull合并;
   3. 如果合并有冲突,则需要解决一下冲突,并且在本地提交(git add  git commit命令)
   4. 没有冲突或者解决掉冲突后,再用git push origin <branch-name>推送就可以.
   
   如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
  
  ##Rebase
  
    当你发现commit太多，但是你只希望push上去只有一次commit那么rebase可以帮你忙：
    1. 首先  git log查看commit记录
    2. 然后 git rebase -i (版本号)   注：这个版本号需要是你需要commit到的那个版本的前一个版本
    3. 这时会进入一个界面除了最上面的pick  其他全部改为s，改完之后，保存
    4. 注释掉不需要的commit,然后保存即可
    
详情：
<a href="https://www.jianshu.com/p/4a8f4af4e803">git-rebase</a>

