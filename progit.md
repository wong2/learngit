读progit的过程中记下一下东西

###基础：
* git status
* git add
* 暂存状态(在下一次commit时提交的)
* 修改后的文件也要用git add加到暂存区
* 要养成一开始就设置好.gitignore文件的习惯
* git diff 查看当前文件与暂存区快照间的差异
* git diff --cached 查看已经暂存起来的变化
* git commit
* git commit -a 把所有已经跟踪过的文件暂存起来一并提交，从而跳过git add步骤 
* 从git中移除某个文件：git rm [-f] 同时会从文件系统中删除之
* git rm --cached xxxx 可将某个文件解除git管理
* git mv 进行文件重命名
* git log 查看提交历史，图形化工具比如gitk, gitg
* git commit --amend 用当前暂存区的文件替换最后一次提交
* 撤销对某文件的修改： git checkout -- xxx

###远程仓库
* git remote [-v]
* git remote add remote-name url
* git fetch remote-name, fetch只是把数据拉取到本地，不会自动合并
* git push remote-name branch-name
* git remote show xxx
* git remote rm xx

###标签
* git tag，列出标签
* git tag -a tagname
* git show tagname
* git tag xxxx: 轻量级标签

###协议:
* ssh: 
    * 如果需要安全的write access，用ssh比较合适
    * 但该协议不能提供匿名服务，像github上的那种任何人都可以clone的，不能用ssh
* git:
    * 快
    * 适合read access不需要认证的
    * 没有认证
* http:
    * 配置简单
    * 不够高效和智能

总结： write access的用ssh, anonymous read-access的用git

###分布式工作流程：
介绍了几种用使用git的工作流程

* 集中式工作流
很好理解，就是一台放代码仓库的中心服务器,开发者都是与它打交道：
![集中式](http://progit.org/figures/ch5/18333fig0501-tn.png)

    缺点：如果两个开发者从中心服务器上clone了代码，都做了修改，那么只有第一个开发者可以顺利的推送修改到服务器，第二个开发者在提交他的修改前，必须先下载、合并服务器上的数据，解决冲突后才能再推送。

* 集成管理员工作流

![集成管理员](http://progit.org/figures/ch5/18333fig0502-tn.png)

    1. 项目维护者创建了公共仓库(blessed repository)
    2. 贡献者clone该仓库，并建立自己的公共仓库(developer public)
    3. 贡献者在自己电脑上开发，然后push到自己的公共仓库上去
    4. 贡献者通知项目维护者，请求拉取自己的修改
    5. 项目维护者在自己本地的仓库里把贡献者的仓库加为远程仓库,合并新代码，测试
    6. 维护者把合并后的更新推送到主仓库(blessed repository)

    github上用的最多的就是这种工作流,比如第2步就是fork，4就是pull request

* 司令官与副官工作流

    一般像linux kernel这种超大型的项目才会用到。。感觉就是在 集成管理员工作流 基础上，分成很多小组，每个小组有个负责人，每个小组内使用集成工作流，然后各组长整合代码提交给总司令.
