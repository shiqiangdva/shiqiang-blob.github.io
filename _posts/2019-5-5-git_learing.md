第一章:  Git基础

01 | 课程综述

Git 官网： https://git-scm.com
GitHub： https://github.com
GitLab： https://about.gitlab.com
SVN： https://subversion.apache.org

02 | 安装Git
 
在官网一顿下一步, 在命令行输入: git - -version 检验是否安装成功(版本)

03 | 使用Git之前需要做的最小配置 

# 本节知识点

## 查看git命令有哪些
git config

## 添加配置

git config [--local | --global | --system] user.name 'Your name'
git config [--local | --global | --system] user.email 'Your email'

## 查看配置

git config --list [--local | --global | --system]

## 区别

local：区域为本仓库
global: 当前用户的所有仓库
system: 本系统的所有用户


04 | 创建第一个仓库并配置local用户信息

## 创建一个空的本地git仓库
git init your_project(创建项目仓库 your_project为你的项目文件夹命名)

git config --local user.name ‘shiqiangdva’(创建本地库username)
git config --local user.email '1114005726@qq.com'(创建本地库email)

git config --local —list(检查设置成功没)


## 添加文件 初次提交
git status(查看此刻状态)

git add xxxfilename(添加新增的xxxfile)

git commit -m 'Add Readme’(提交 m是提交备注信息 ‘填写的备注信息内容’)

git log(查看提交记录, 包括作者邮箱提交文件以及备注信息)

注意: 在global文件夹中创建local文件夹,设置local username和email那么这个文件夹就是local仓库




05 | 通过几次commit来认识工作区和暂存区


## 对于已经被git跟踪的文件,进行了修改,那么想要提交这些文件只需要执行下面代码:

(
	1. cp -r ../xxx/file .  ->  拷贝xxx/file文件夹下的所有文件 到当前目录( . 就是表示当前目录)
	2. ls -al 查看当前目录下的 所有文件(详细信息)
	3.vi xxx/file   ->  查看file文件下的内容  并可编辑
	3.1 a -> 键进入编辑   shift + : -> 输入命令   :w写文件 :w!写文件忽略警告 :wq 写文件后退出 :q 退出  :q!强制退出编辑器  :x退出编辑器,如果文件有改动则保存退出
	4. mkdir 创建文件夹
	5. echo xxxx > fileName (向某文件写入xxxx内容)
	5. rm -rf <doc> (删除<doc>文件夹中所有内容) *(慎用!!!)
)

##注意:
git add -u：将文件的修改、文件的删除，添加到暂存区。
git add .：将文件的修改，文件的新建，添加到暂存区。
git add -A：将文件的修改，文件的删除，文件的新建，添加到暂存区。

git add -A相对于git add -u命令的优点 ： 可以提交所有被删除、被替换、被修改和新增的文件到数据暂存区，而git add -u 只能操作跟踪过的文件
git add -A 等同于git add -all



06 |   给文件重命名的简便方法

# 使用git命令变更文件名
方法1:(正常方法,但是比较麻烦,不推荐使用)
步骤1:git mv oldFileName newFileName
步骤2:git add newFileName

方法2: git mv oldFileName newFileName(一条命令直接完成,较为简单,但是还是麻烦)

方法3: git add -A (代表的含义看上面05节总结处)

危险命令:git reset --hard (代表删除工作区以及暂存的内容,不影响commit记录)



07 | 通过git log 查看版本演变历史

## 查看单行的简洁历史记录(截图如下)
git log --oneline
## 查看最近的四条简洁历史
git log --oneline -n4 (4代表只看最近的4条)

## 查看本地有多少分支
git branch -v

## 查看远端有多少分支
git branch -a / git branch -av

## 创建并切换到该分支下
git checkout -b <分支名> <commit点>

## 提交时直接用 -am 可以省去 git add(不推荐使用)
git commit -am '备注信息'


## 查看所有分支的详细历史信息
git log —all

## 看看最近的几条数据
Git log -<数字>

## 显示图表的形式(加上--graph后分之关系表现的更为直观) (推荐这样使用!)
git log --all —oneline -n4 —graph

注: git log 指向当前分支, 也可以后面添加分支名来指定分支信息


08 | gitk: 通过图形界面工具来查看版本历史

## 打开git自带的图形管理界面
gitk --all (—all git可视化图形界面 查看所有分支内容)


09 | 探秘.git目录(可以略过)

1. git目录中的 HEAD文件内容 指明了当前工作的分支
2. git checkout master 切换到主分支
3. git目录下 config文件内容 存放了git的配置信息(用户名以及邮箱等)
4. git目录下 git/refs/heads 存放当前所有分支的对象
5. git目录下refs/tags 存放所有的标记tags



10 | commit / tree / blob三个对象之间的关系

## git查看xxx文件内容
git cat-file -p xxx

## git查看xxx文件类型
git cat-file -t xxx

个人理解: 
每一次提交都产生一个commit文件 (内部存储着一个tree文件与提交人的个人信息提交时间和它相关连的父节点的commit信息id) -> 其中存储的tree存储着本次提交的详细内容(tree可以简单的理解为一个带有唯一id值的文件夹或者文件, 它内部存储了数据内容变更的详细信息的blob, 通过id来访问具体的每条内容的blob数据) -> blob为存储的每个文件的具体内容通过id来容许被tree访问(通过链式的id绑定设计,可以存储每次commit的具体内容,节省存储空间的占用)




11 | 练习思考(答案如图所示)



12 | 分离头指针情况下的注意事项

## 切换到新创建的分支
git checkout -b xxx (xxx为某个commit对象序列)

## 分离头指针就是把 -b去掉  也不接分支名 单纯的切换到xxx这个commit值上 (此时就会分离头与分支形成单独的且临时的一个地址  变更也能够正常的被修改以及提交但是一段时间会被git回收删除, 所以需要及时的绑定到git分支上)
git checkout  xxx (xxx为某个commit对象序列)



##  新建分支到某个xxx commit上(如下图所示)
git branch <new branch name> <xxx commit值>




13 | 进一步的理解HEAD和branch

## 注意下面命令是在主分支下新建分支, 要想在分支下在新建分支需要在命令后在加分支的名字
1.git checkout -b branchName
2.git checkout -b branchName from BranchName

## 比较两个commit之间的差异
git diff xxxx  oooo (xxxx 和 oooo 是两个commit对象的序列值)

注意: HEAD无论何种状态, 它指向的都会是commit对象(哪条分支下的哪次commit或者分离头状态下的单独的commit对象)



第二章: 独自使用Git时的常见场景

14 | 怎么删除不需要的分支

## 删除分支
git branch -d  <xxxBranchName> 
## 强制删除分支
git branch -D  <xxxBranchName> 
 注意: 使用-d 在删除前Git会判断在该分支上开发的功能是否被merge. 如果没有,不能删除. 如果merge到了其它分支, 但之后又在其上做了开发, 使用-d还是不能删除. -D会强制删除. 使用-D代表开发人员确认其风险,能够把控对删除的风险控制, 那你就可以用-D来强制删除分支.




15 | 怎么修改最新commit的message?


## 对最近一次的commit 中的message做变更
git commit --amend





16 | 怎么修改老旧commit的message?

## 修改老commit message信息
git rebase -i xxx(想要修改commit序列号的父commit序列号!!!)
进入之后会进行控制编辑(r,reword) —> 在进行message编辑



17 | 怎样把连续的多个commit整理成1个?

## 整合几个连续commit提交记录为一个 选择那几个连续commit序列号的前一个commit序列号也就是其父commit序列号
git rebase -i xxx
进入之后会进行控制编辑(s,squash) -> 在进行编辑 message 信息保存




18  | 怎样把间隔的几个commit整理成一个

同样使用上面的git rebase -i xxx 命令在编辑中把想要合并的commit放在一起重复上述步骤 <小心使用commit的合并!!!>




19  |  怎样比较暂存区和HEAD所含文件的差异

## 暂存区与HEAD指针指向的commit对象 所含文件的different所用的命令:
git diff --cached

注意: 什么意思呢?就是放到暂存区的内容(git add xxx)与最近一次的commit中的内容做diff比较.

20 | 怎样比较工作区和暂存区所含文件的差异

## 比较工作区和暂存区的所有文件的差异
git diff
## 比较工作区和暂存区的某文件差异 ( —fileName )
git diff --fileName(比较的是指明的后面fileName的文件差异)   




21 | 如何让暂存区恢复成HEAD的一样?

## 恢复暂存区 与 之前最近提交的commit一致(也就是说暂存区的内容退回到工作区中)
git reset HEAD



22 | 如何让工作区的文件恢复为和缓存区一样?

##注意: 想要变更工作区就用checkout  想要变更暂存区就用reset
暂存区恢复成HEAD：git reset HEAD
工作区恢复成暂存区：git checkout -- <file>




23 | 怎样取消暂存区部分文件的更改到工作区

git reset HEAD -- <fileName>





24 | 取消最近的几次提交

## 退回到<commit-id(commit对象序列)>这次提交的状态, 之后的commit提交就将会被删掉
git reset --hard <commit-id(commit对象序列)>




25 | 看看不同提交的指定文件的差异


## 比较分支的不同 (全比较/文件比较)
git diff xx oo
git diff xx oo —— <fileName>
注意:   xx 和 oo 既能表示分支又能表示commit-id






26 | 正确删除文件的方法

## 取消暂存区并取消变更
git reset --hard HEAD

## 删除文件(直接放进暂存区不需要手动到文件夹中删除)
git rm <fileName>






27 | 开发中临时加塞了紧急任务怎么处理?

## 暂时存储起来
git stash

## 查看暂时存储库信息
git stash list
## 恢复暂时存储内容 方法1(区别: 暂存库中依旧保存这条信息)
git stash apply

## 恢复暂时存储内容 方法2(区别: 暂存库中拿出来的信息 将被删除掉)
git stash pop






28 | 如何指定不需要Git管理的文件


## 把想忽略的文件添加到 .gitignore git就将忽略这些格式或目录下的内容
## 常用 配置文件示例:
1: 忽略 .a 文件
*.a

2: 但否定忽略 lib.a, 尽管已经在前面忽略了 .a 文件
!lib.a

3: 仅在当前目录下忽略 TODO 文件， 但不包括子目录下的 subdir/TODO
/TODO

4: 忽略 build/ 文件夹下的所有文件
build/

5: 忽略 doc/notes.txt, 不包括 doc/server/arch.txt
doc/*.txt

6: 忽略所有在doc/directory下的的.pdf 文件 
doc/**/*.pdf








29 | 如何将Git仓库备份到本地?




















## 哑协议
git clone --bare /xxx/gitProjectName/.git ya.git
## 智能协议
git clone --bare file:///xxx/gitProjectName/.git zhineng.git
(注意1: --bare  代表不clone工作区中的内容)
(注意2: 项目路径后需要添加.git后缀 然后加上命名)
(注意3: 智能协议需要加file://)

## 与克隆库(zhineng)进行关联 git remote add zhineng file:///xxx/zhineng.git

## 当原始库发生变更(比如新建了一个分支)要push到远端
git push zhineng
(注意: 这里git会出提示 按照他提示的命令输入就好)




第三章:  Git与GitHub简单同步


30 | 注册一个GitHub账号

俺有两个号~  哼~  这节纯扯淡





31 | 配置公私钥







32 | 在GitHub上创建个人仓库
这还用教么? 但建仓库要是真有一天轮到我去干了, 那我就是大牛了,走向人生巅峰了!


33 | 把本地仓库同步到GitHub

- git remote -v 查看远程(本地)版本库信息
- git remote add xxx(别名) <url> 添加githup远程版本库
- git remote -v 查看远程版本库信息
- git fetch xxx(别名) 拉取远程版本库
- git merge -h 查看合并帮助信息
- git merge --allow-unrelated-histories githup/master 合并githup上的master分支（两分支不是父子关系，所以合并需要添加 --allow-unrelated-histories）
- git push xxx(别名) 推送同步到Githup仓库







第四章:  Git多人单分支集成协作时的简单场景



34 | 不同人修改了不同文件如何处理?

## clone后在本地查看远端分支
git branch -a / git branch -av

## 创建本地分支并指向远端分支
git checkout -b <本地分支名(最好起名与远端分支名保持一致)> <远端分支名>
( —这样的好处是本地分支与远端分支联系起来, git push 命令就不在需要在后面接上远端的分支名了— )

当其他人修改不同文件并进行了push, 而本人不知道自己本地是否为最新的代码,方法1:可以先pull在push, 方法2: 先git fetch 在merge 在push


35 | 不同人修改了同文件的不同区域如何处理?

##不同人修改了同文件的不同区域与34节类似, 但是需要记住一些概念(纯个人总结理解):
fast-forword 看了英语翻译为快进，结合git branch -av 中的 ahead 和behind，ahead是本地仓库比远端仓库多commit，behind是本地仓库比远端仓库少commit。对正常的备份系统来说，我本地只能比备份多，备份不可能比我本地多才是。然而，git 由于多用户提交原因出现备份比本地多了，本地滞后了，所以需要pull一下，让本地比备份相等或多，这种情况就是fast forward ，也就是我本地要比备份快进.


36 | 不同人修改了同文件的同一区域如何处理?

## git pull 与本地有冲突时, 会提示内容冲突需要merge, 冲突的文件也会提示出来,如图所示:




注意: 上面是通过提示检测出冲突文件,之后手动通过命令vim/vi 去修改文件在执行git commit -> git push, 还可以通过pull后git 自动merge失败,知道了有代码冲突, 直接使用 git mergetool来进行可视化工具解决冲突.



37 | 同时变更了文件名和文件内容如何处理?

##注: 本节内容与34和35节类似,git会非常智能的通过pull命令来自动merge, 个人理解总结如下:
    前面章节讲git的文件存储时，说git存放blob文件时是以文件内容来区分的，并不以文件名来区分；此处的变更文件名操作和变更文件内容的操作能够自动被git处理，原因就在于blob文件并没有发生修改的冲突. 如果其中一个人既变更了文件名又修改了文件，同时另一个人也修改了该文件的同一位置的内容，就会被git识别为冲突，而不能自动进行处理了.


38 | 把同一文件改成了不同的文件名如何处理?

##如下图所示, 两个人同时修改了文件名,一个人改成了index1,一人改成了index2,其中一个人push到了远端,另一人pull后,就会报文件冲突, 解决方案git也会友好的进行提示,需要删除不需要保留的文件,添加需要保留的文件:

git add <fileName>
git rm <fileName>











##补充: 当有人将不想添加到git管控的文件,忘记在gitignore文件中进行配置,误将这些文件push到了远端, 之后再把这些文件补充到了gitignore中去,会造成一些麻烦,如果仅仅用git rm再push的话，本地和远端的文件都会被删除，在远端删除后pull也是同理,解决方案:
1.git ls-files 查看暂存区内已进行版本控制的文件
2.git rm --cached <文件名> 将文件移除版本控制
3.编辑.gitignore文件，将不想加入版本控制的文件写进去, (详细方法可参考github上的.gitignore文件)





第五章:  Git集成使用禁忌


39 | 禁止向集成分支进行push -f 操作

个人理解:
如果发现之前提交的commit不想要了,想恢复成之前的样子, 假如是自己独自使用的分支,可以采用push -f 的方式.团队集成分支,通常做法不是去掉不想要的commit,而是把不想要的commit的内容采用revert的方式生成新的commit,以此去掉不想要的变更,然后push到远端.
假如你使用了git reset --hard <commit序列号>将指针指向了历史版本中的某个commit,或者你本地的commit并不是远端的最新的一次commit,当你使用git push -f <分支名>指令后(-f为强制执行),你会 强制变更本条分支远端与本地的历史记录进行刷新,使分支历史变的动荡.

##注: 可以尝试使用 git reflog 命令查找历史，然后利用 git reset --hard HAED@{n} 的方式恢复(我没验证过是否可行)




40 | 禁止向集成分支执行变更历史的操作

##个人理解: 当一个人对集成分支进行了变基操作,将多个commit进行了合并等操作,就会导致其他人提交代码造成问题,因为不再是fast forwork, 切记当提交的分支是团队开发时,不能进行变基的操作.


第六章:  初识GitHub


41 | GitHub为什么会火?



42 | GitHub都有哪些核心功能?

嗯... ...


43 | 怎么快速淘到感兴趣的开源项目?

1.可以进行高级搜索: https://github.com/search/advanced 
2.搜索框中搜索的关键字是开源项目的名称以及项目描述
3.搜索栏中可以添加in < 等代码,详情查看1.中的高级搜索


44 | 怎样在GitHub上搭建个人博客

1. 制作个人博客请github搜索:  barryclark/jekyll-now, 三部教程很简单.
2. 我的github个人博客地址为:  https://shiqiangdva.github.io/


45 | 开源项目怎么保证代码质量?

如何在github中成为一个开源项目的贡献者




46 | 为何需要组织类型的仓库?

1. GitHub中组织机构仓库的Members成员, Team分组, Repositories成员的权限申请等介绍
2. 仓库管理 请求介绍 权限介绍等




第七章:  使用GitHub进行团队协作



47 | 创建团队的项目

GitHub创建项目时就可以选择个人或者组织
创建后可以添加team和配置权限以及人员



48 | 怎样选择适合自己团队的工作流?

1.主干开发只使用月google Facebook等超强编码能力的团队进行使用
















2. git flow过程过于复杂, 不适用于敏捷开发.













3. github flow与上面对比两种对比, 较为符合大众需求.





49 | 如何挑选合适的分支集成策略?

## 对于产品发布测试等问题: 
   如果采用特性分支开发方式（即：一个master多个特性分支）。比如：有个特性分支f1已经开发完成后还没测试，应该才采取下面那个方案：
方案1：
1、测试人员基于f1分支完成测试功能
2、合并f1到master
3、上线master
方案2：
1、合并f1到master
2、基于master(或拉取一个production分支)做测试
3、上线production

如果采用方案1，我感觉有以下缺点
在第二步骤其实并不能保证没有合并冲突或合并过程中产生的bug。所以步骤1的测试意义不大。
如果在merge完成后再测试一遍，又浪费测试资源和时间。
如果采用方案2，我感觉缺点是：
如果合并到master后，业务方或其他原因说又不上线了。如果这时候又有一个需求f2要上线，还得把master上合并的f1分支剥离下来，这个剥离的具体做法是对f1 merge的节点进行revert，还是怎么做？



50 | 启用issue跟踪需求和任务

在setting中启动issues功能后, 大家都能够进行提出issues共同交流.



51 | 如何用project管理issue?

看板模式


52 | 项目内部怎么实施code review?

code review代码分支合并时的评审检测



53 | 团队写作时如何做多分支的集成?

方法1: (create a merge commit) Megre pull request: 
    此方法来合并分支,只将分支当成一个大版本进行合并,不包含分支的commit记录.

方法2: (create a merge commit) Squash and merge: 
    此方法相当于将分支的历史也合并到了master之中.

方法3:(create a merge commit) Rebase and merge:  
    此方法要是你不懂git rebase 变基就放弃吧而且很麻烦, 需要本地进行与远端的变基操作, 然后会报出多次的冲突需要merge,merge后再git add .操作在进行 git rebase —continue, 需要合并的次数取决于与远端的commit差异数量, 当git status查看没有问题时,在进行git push操作, 之前的两种方法在github上会自动帮助操作与合并的冲突,但是rebase方式github无法帮助我们解决此问题,需要我们本地进行变基操作,很是麻烦除非特别需要, 但是这种方式的好处是, 在github中查看历史提交记录的线形图时, 每一个分支和master都是直线的,很清晰.



54 | 怎样保证集成的质量?

Codecov等第三方的代码检测插件, 集成到github中, 在pull request合并分支时会根据设定来检测代码是否满足合并的要求

##注: 剩下的一章是讲GitLab的分支发布, 和扯淡, 就不记录了.










































