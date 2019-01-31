#时光机穿梭
1. 要随时掌握工作区的状态，使用git status命令。

2. 如果git status告诉你有文件被修改过，用git diff <文件名> 可以查看修改内容

##版本回退

 1. HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。  (其中commit_id用git log命令可以查询   输入commit_id的时候只需要输入前四位即可)

 2. 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

 3. 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

##工作区和暂存区
 1. 工作区:你在电脑上能看到的目录,比如learngit文件夹就是一个工作区.

 2. 暂存区:

    - 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
    - 图片实例
![暂存区stage](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)
   
    - 前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

        第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

##管理修改
1. git跟踪并管理的是修改，而非文件：当修改同一文件时，如果不用git add到暂存区，那就不会加入到commit中！！
即：第一次修改--》git add-->第二次修改--》git commit    是行的

##撤销修改
1. 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

2. 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

3. 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考“版本回退”一节，不过前提是没有推送到远程库。


##删除文件
1. 添加一个新文件test.txt到GIT并且提交：git add  git commit提交后，就在本地以及版本库均有文件了，
当用命令rm test.txt删除本地文件后，你可以有两个操作：
    - 可以用git checkout -- test.txt在版本库中找回你删除的本地库
    - 用git rm test.txt从版本库中删除该文件，并且git commit -m "remove test.txt"，之后文件就从版本库中删除了。


#远程仓库
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

##添加远程库

    - 你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作。做法如下：
   1. 登录github,新建一个repository,名字与本地文件名相同
   2. git remote add origin git@github.com:james/learngit.git
   3. 关联后，使用命令git push -u origin master第一次推送master分支的所有内容
   4. 此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改

**说明**：2.中git@...是你自己github的ssh链接。
远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。
3.中由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
     
##从远程库克隆

- 假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

- 首先，登陆GitHub，创建一个新的仓库.
然后使用git clone 命令克隆：如git clone git@github.com:james/gitskills.git



#分支管理

##创建与合并分支
因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
Git鼓励大量使用分支：

   - 查看分支：git branch

   - 创建分支：git branch <name>

   - 切换分支：git checkout <name>

   - 创建+切换分支：git checkout -b <name>

   - 合并某分支到当前分支：git merge <name>

   - 删除分支：**本地**git branch -d <name>   **远程** git push origin --delete <name>

   - 博客里面画的分支图没太弄懂 

**##解决冲突**

  1. 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

  2. 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

  3. 用git log --graph命令可以看到分支合并图。  
       - 详情：<a href="https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840202368c74be33fbd884e71b570f2cc3c0d1dcf000">

##分支管理策略
   - 在实际开发中，我们应该按照几个基本原则进行分支管理：

1. 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

2. 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

3. 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![fenzhi](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)


**小结**
   - Git分支十分强大，在团队开发中应该充分应用。

   - 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

##Bug分支
   - 当你手头工作没做完不能提交，然后要紧急解一个其他的bug那么就需要用到下面的方法：

        - 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

        - 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

##Feature分支
  **添加新功能时的分支**

   - 每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

**小结**

   - 开发一个新feature，最好新建一个分支；  新建分支与之前的相同
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。


**##多人协作##**


##推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git
就会把该分支提送到远程库对应的远程分支上：
比如想要推送dev分支到远程：
git push origin dev

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

##抓取分支

多人协作时，大家都会往master和dev分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：

$ git clone git@github.com:michaelliao/learngit.git
Cloning into 'learngit'...
remote: Counting objects: 40, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 40 (delta 14), reused 40 (delta 14), pack-reused 0
Receiving objects: 100% (40/40), done.
Resolving deltas: 100% (14/14), done.
当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。不信可以用git branch命令看看：

$ git branch
* master

我这里出现了一个问题：在git branch 时出现如下问题：fatal: Not a git repository (or any of the parent directories): .git    使用git init命令即可解决。


