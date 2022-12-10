配置:
    name
        git config --global user.name "luotao"
    email
        git config --global user.email "511221995@qq.com"

使用git:
    git status
        查看当前仓库的状态
            未跟踪：没有被gif所管理
            已跟踪：已被gif管理
                暂存：文件修改已经保存，但是未提交到git仓库
                未修改：磁盘中的文件和git仓库中文件相同，没有修改
                已修改：磁盘中文件已经被修改，和git仓库中文件不同
                    已修改-->暂存-->未修改
    git init
        初始化仓库

    刚刚添加到项目中的文件处于未跟踪状态
        未跟踪-->暂存 
            git add <filename> 将文件切换到暂存状态
            git add * 将所有已修改或未跟踪的文件暂存
        暂存-->未修改
            git commit -m "xxxx" 将暂存的文件存储到仓库中，xxxx中最好写修改了什么功能
            git commit -a -m "xxxx" 提交所有已修改的文件(未跟踪的文件不会提交)
        未修改-->已修改
            修改代码后，文件会变为修改状态
        已修改-->暂存：
            git add <filename>

常用的命令
    重置文件
    	git restore <filename> 恢复到上一次未修改时的文件
        git restore --staged <filename> 取消暂存状态
    删除文件    
        git rm <filename> 这个只能删未修改的文件，已修改的文件不能删除
        git rm <filename> -f 强制删除，啥都能删

    移动文件
        git mv from to 重命名文件


分支
    git在存储文件时，每一次代码的提交都会创建一个与之对应的节点，git就是
        通过一个一个的节点来记录代码状态的。节点会构成一个树状结构，树状
        结构就意味着会存在分支，默认情况下仓库只有一个分支，命名为master
        在使用git时，可以创建多个分支，分支与分支之间相互独立，在一个分支
        修改代码不会影响其他的分支。

    操作
        查看当前分支
            git branch 
        创建新的分支
            git branch <branch name>
        删除分支
            git branch -d <branch name>
        切换分支
            git switch <branch name>
        创建并切换分支
            git switch -c <branch name>
        合并分支
            git merge <branch name>

    在开发中，都是在自己的分支上编写代码，代码编写完成后，再把自己的分支合并到主分支中
        

变基(rebase)
    在开发中除了通过merge来合并分支外，还可以通过变基来完成分支的合并
    我们通过merge合并分支时，在提交记录中会将所有的分支创建和分支合并的过程全部显示出来
        这样当项目比较复杂，开发过程比较波折时，我们必须反复的创建、合并、删除分支。这样
        一来将会使得我们代码的提交记录变得极为混乱

    原理：
        1.当发起变基时，git首先会找到两条分支最近的共同祖先
        2.对比当前分支相对于祖先的历史提交，并且它们提取出来存储到一个临时文件中
        3.将当前部分指向目标的基底
        4.以当前基底开始，重新执行历史操作
    变基和merge对于合并分支来说最终结果是一样的，但是变基会使得代码的提交记录更整洁更清晰
        注意，大部分情况下合并和变基是可以互换的，但是如果分支已经提交给了远程仓库，那么这时
        尽量不使用变基


远程仓库(remote)
    目前对于git的所有操作都是在本地进行的，但是在开发中显然不能这样，这时我们就需要一个git仓库
        远程的git仓库和本地的没有什么本质的区别，不同的是远程仓库可以被多人同时访问
        方便我们协同开发。在实际工作中，git服务器通常由公司搭建内部使用或是购买一些
        公共的私有git服务器。我们学校阶段，直接使用一些开放的公共git仓库。目前我们常用
        的库有两个：Github 和 Gitee(码云)

        将本地库上传github：
            git remote add origin https://github.com/luotaoQAQ/git-demo.git
                这里origin是随便取的远程仓库的名字，后面是远程仓库的url
            git branch -M main
                这个命令是修改分支的名字为main
            git push -u origin main
                将代码上传到服务器上

        将本地库上传gitee：
            cd existing_git_repo
            git remote add gitee https://gitee.com/luotaoQAQ/git-demo.git
            git push -u gitee "main"


    
