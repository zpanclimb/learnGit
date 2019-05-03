# 常用Git命令

## Git帮助

+ `$ git help <verb>`
  + 例如，要想获得 `config` 命令的手册，执行:`$ git help config`

+ `$ git <verb> --help`

+ `$ man git-<verb>`

--------------------------------------------------

## 检查配置

+ 查看 `Git` 的版本：`$ git version`

+ 检查 Git 的某一项配置：`git config <key>`

+ 查看配置信息：`$ git config --list`

--------------------------------------------------

## 绑定编辑器

+ 例如：绑定 Vim 编辑器：`$ git config --global core.editor Vim`

--------------------------------------------------

## Git Bash 界面

+ 清除 `Git Bash` 界面中的内容：`$ clear`

--------------------------------------------------

## 用户信息

### 全局信息

+ 添加或者修改全局用户名：`$ git config --global user.name "your name"`

+ 添加或者修改全局邮箱地址：`$ git config --global user.email "email address"`

+ 查看全局用户名：`$ git config --global user.name`

+ 查看全局邮箱地址：`$ git config --global user.email`

+ 查看全局配置信息：`$ git config --global --list`

### 局部信息

+ 添加或者修改局部用户名：`$ git config user.name "your name"`

+ 添加或者修改局部邮箱地址：`$ git config user.email "email address"`

+ 查看局部用户名：`$ git config --local user.name`

+ 查看局部邮箱地址：`$ git config --local user.email`

+ 查看局部配置信息：`$ git config --local --list`

+ 查看本地用户：`$ whoami`

--------------------------------------------------

## 目录 / 文件夹操作

+ 进入下一级目录：`$ cd <direction>`

+ 返回上一级目录：`$ cd ..`

+ 进入到本地用户目录：`$ cd ~`

+ 创建一个新目录：`$ mkdir <direction>`

+ 显示目录中的内容：
  + 显示内容较为简洁：`$ ls`
  + 显示内容较为详细：`$ ll`
  + 显示全部内容：`$ ls -ah`

+ 移动目录：`$ mv dir-1 dir-2`
  + 注：将目录 'dir-1' 移动到目录 'dir-2' 下成为其子目录

+ 重命名目录：`$ mv old new`
  + 注：将目录名 'old' 更改为 'new'

+ 删除空目录：`$ rmdir <direction>`
  + 注：此命令只能删除空目录

+ 删除目录：`$ rm -r <direction>`
  + 注：此命令使用递归将目录下的所有内容全部删除，再删除自身

--------------------------------------------------

## 文件操作

### 创建、查看、删除文件

+ 创建一个文件：`$ touch <file>`
  + 例如：创建一个文件名为 'example' 的 'txt' 文件：`$ touch example.txt`

+ 移动文件：`$ mv example.txt dir`
  + 注：将文件 'example.txt' 移动到目录 'dir' 下

+ 重命名文件：`$ mv old.txt new.txt`
  + 注：将文件名 'old' 更改为 'new'，文件类型不变

+ 复制文件：`$ cp new.txt ./dir`
  + 注：将文件 'new.txt' 复制到同级目录 'dir' 下

+ 查看文件内容：
  + `$ cat <file>`
  + `$ head <file>`
  + `$ tail <file>`

+ 查看文件的开头几行内容：`$ head -3 <file>`
  + 注：查看文件的前三行内容

+ 查看文件的倒数几行内容：`$ tail -f -n 3 <file>`
  + 注：查看文件的倒数三行内容

+ 删除文件：
  + 只删除工作区的文件：`$ rm <file>`
    + 注：执行此命令需要手动使用 `add` 命令将删除操作添加到暂存区

  + 同时删除工作区和暂存区的文件：`$ git rm <file>`
    + 注：执行此命令自动将删除操作添加到暂存区

+ 覆盖文件内容：`$ echo "content" > <file>`

+ 追加内容到文件末尾：`$ echo "content" >> <file>`

+ **文件的重要操作：删除与恢复**
  + **删除**
    + `$ rm <file>`
    + `$ git rm <file>`

  + **恢复文件内容，或者撤销删除操作**
    + 对文件的修改或者删除操作还在工作区，但是还没有添加到暂存区，恢复文件只需要一步：`$ git checkout -- <file>`
  
    + 对文件的修改或者删除操作已添加到暂存区，但是还没有提交到版本库，恢复文件需要两步：
      + 第一步，从暂存区移除：`$ git reset HEAD <file>`
      + 第二步，撤销删除操作：`$ git checkout -- <file>`
  
    + 如果删除操作已经提交至版本库：那么请使用版本回退

### 比较文件的差异

+ 比较工作区和暂存区的文件差异：`$ git diff`

+ 比较暂存区与最新本地版本库：`$ git --cached`

+ 比较工作区与最新本地版本库：`$ git HEAD`

+ 比较工作区与指定 `commit_id` 的差异：`$ git commit_id`

+ 比较暂存区与指定 `commit_id` 的差异：`$ git --cached commit_id`

+ 比较两个 `commit-id` 之间的差异：`$ git commit_id commit_id`

--------------------------------------------------

## 版本库相关操作

### 新建版本库与提交版本

+ 从已存在的目录新建一个版本库：`$ git init`

+ 查看工作区与暂存区的内容：`$ git status`

+ 将操作从工作区添加到暂存区：`$ git add <file>`
  + 注：`add` 命令可以执行多次，将多个操作添加到暂存区

+ 将操作从暂存区提交到版本库：`$ git commit -m "此次提交说明"`
  + `commit` 命令可以一次性将暂存区的操作提交至版本库：

    ```text
      git add file1.txt
      git add file2.txt
      git commit -m "此次提交了两个文件"
    ```

### 撤销操作

+ 撤销工作区的文件修改：`$ git checkout -- <file>`
  + 注：此命令只能撤销工作区的文件修改

+ 移除暂存区中文件至未跟踪状态：`$ git rm --cached <file>`
  + 使用此命令可将文件的状态置为 `untracked files`

+ 移除暂存区中文件准备提交状态：`$ git reset HEAD <file>`
  + 注：当存在提交历史时可使用此命令，将文件从暂存区移除，并放到工作区

+ 撤销上一次提交并将暂存区文件重新提交：`$ git commit --amend`
  + 带上提交信息：`$ git commit --amend -m "commit message"`
  + 注：如果自上次提交以来你还未做任何修改（例如，在上次提交后马上执行了此命令），那么快照会保持不变，而你所修改的只是提交信息
  + 注：如果暂存区中内容已修改，最终你只会有一个提交：第二次提交将代替第一次提交的结果

### 查看日志与历史

+ 查看提交日志：`$ git log`
  + 一行内显示简写：`$ git log --oneline`
  + 将每一个提交日志缩减为一行显示：`$ git log --pretty=oneline`
  + 缩短 `commit_id` ，一行内显示：`$ git log --pretty=oneline --abbrev-commit`
  + 查看指定文件的提交日志，并且缩减为一行显示：`$ git log --pretty=oneline <file>`
  + 查看提交日志的详情：`git log -p`
  + 注：`git log` 不能查看已删除的提交日志，即如果进行了版本回退，那么回退版本号之后再提交的日志都不能查看，如要查看全部提交日志，请使用 `$ git reflog`

+ 查看所有分支的所有提交日志：`$ git reflog`
  + 注：此命令可以查看所有分支的所有提交日志（包括 `commit` 和 `reset` 的操作），包括已经被删除的 `commit` 记录，`git log` 则不能查看已经被删除了的 `commit` 记录

+ 查看命令行历史记录：`$ history`

+ **版本回退：**
  + 方式一：`$ git reset --hard HEAD^`
    + 注：上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成 `HEAD~100`
  + 方式二：`$ git reset --hard commit_id`
    + `commit_id` 指的是每次提交操作的版本号，使用 `$ git log` 命令可以查看全部提交操作的版本号，一般取版本号的前 7 位即可
  + 注：`reset` 有三个参数：`--mixed` 、`--soft` 、`--hard`
    + `--mixed`：使用此参数，暂存区内容会被丢弃，工作区内容保持不变
    + `--soft`：使用此参数，暂存区和工作区的内容都保持不变
    + `--hard`：使用此参数，工作区和暂存区的内容都会被丢弃

--------------------------------------------------

## 远程仓库

### 查看远程仓库的信息

+ 查看远程仓库名称：`$ git remote`

+ 查看远程仓库的详细信息：`$ git remote -v`
  + 可抓取的远程仓库地址：`origin  git@github.com:your/yourRepos.git (fetch)`
  + 可推送的远程仓库地址：`origin  git@github.com:your/yourRepos.git (push)`
  + 注：如果没有抓取或者推送的权限，就看不到相应的地址

+ 查看远程仓库的引用信息：`$ git ls-remote`
  + 注：此命令可获得远程引用的完整列表

### 连接与取消连接远程仓库

+ 连接远程仓库：
  + 方式一：`$ git remote add origin git@github.com:your/yourRepos.git`
  + 方式二：`$ git remote add origin https://github.com/your/yourRepos.git`
  + 注：这里远程仓库的默认名字是 `origin`,也可以改成别的

+ 取消与远程仓库的连接：`$ git remote rm origin`

+ 修改远程仓库地址：`$ git remote origin set-url <URL>`

### 推送到远程仓库

+ 推送到远程仓库同时指定默认远程仓库：`$ git push -u origin master`
  + 注：第一次推送本地 `master` 分支到远程仓库时，加上了 `-u` 参数，Git 不但会把本地的  `master` 分支内容推送到远程仓库新的 `master` 分支，还会把本地的 `master` 分支和远程的 `master` 分支关联起来，指定 `origin` 为默认远程仓库，在以后的推送或者拉取时就可以简化命令。

+ 推送到远程仓库：`$ git push origin master`
  + 注：将该分支上的所有本地提交推送到远程仓库 `origin` 的分支 `master`

+ 推送到远程仓库：`$ git push origin`
  + 注：将当前分支推送到远程仓库 `origin` 的对应分支。如果当前分支只有一个追踪分支，那么分支名称都可以省略

+ 推送本地分支推送到远程仓库的分支：`$ git push origin <local-branch>:<remote-ranch>`
  + 例如：将本地分支 `local-branch` 推送到远程仓库的 `remote-branch` 分支,如果远程仓库没有 `remote-branch` 分支就会创建新分支，并且接收本地分支的所有提交
  + 可以通过这种格式来推送本地分支到一个命名不相同的远程分支

### 从远程仓库拉取

+ Git 中从远程的分支获取最新的版本到本地有两个命令：
  + `git fetch`：此命令从服务器上抓取本地没有的数据时，它并不会修改工作目录中的内容。 它只会获取数据然后让你自己合并
  
      ```text
      git fetch orgin master //将远程仓库的 master 分支下载到本地当前 branch 中
      git log -p master ..origin/master //比较本地的 master 分支和 origin/master 分支的差别
      git merge origin/master //进行合并
      ```

    + 也可以用以下指令：多创建一个临时分支保存远程最新内容，合并之后再将其删除

    ```text
    git fetch origin master:temp  //从远程仓库 master 分支获取最新，在本地建立 temp 分支
    git diff temp  //将当前分支和 temp 进行对比
    git merge temp //合并 temp 分支到当前分支
    ```

  + `git pull`：从远程获取最新版本并 `merge` 到本地
  
    ```text
    git pull origin master
    上述命令其实相当于 git fetch 和 git merge
    ```
  
  + 比较 `fetch` 和 `pull` ：
    + 简单地讲：`pull` = `fetch` + `merge`
    + 使用 `fetch`：在 `merge` 前，我们可以查看更新情况，然后再决定是否合并

+ 抓取远程仓库最新的内容：`$ git fetch --all`

+ 抓取远程分支最新内容到当前分支： `git fetch origin <branch-name>` 
  + 注：此命令从远程仓库中抓取本地没有的数据，并且更新本地数据库,并设定当前分支的 `FETCH_HEAD` 为对应的远程仓库分支
  + 注：你需要比较远程分支内容和当前分支内容的差异，视需要手动将远程分支合并到本地分支 `$ git merge origin/<branch-name>`

+ 拉取远程仓库分支到当前分支：`$ git pull origin <branch-name>`
  + 例如：`$ git pull origin master`：将远程仓库 `origin` 的分支 `master` 拉取到当前分支

+ 拉取远程分支到本地指定分支：`$ git pull origin <remote-branch>:<local-branch>`

+ 克隆远程仓库：`$ git clone git@github.com/your/yourRepos.git`
  + 注：将远程仓库完整的克隆一份到本地 Git 开始路径下

--------------------------------------------------

## 分支管理

+ 分支：
  + 版本库的提交操作只会提交到当前分支上，其他分支不受影响
  + 对文件做的更改如果在当前分支上提交，那么改变只能在此分支上可以查看，其他分支上看不到文件的改变，其他分支还停留在最后一次提交的位置
  + 合并分支之后，彼此分支之间的进度就统一了

+ 分支管理：
  + `master` 分支：此分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面进行工作
  + `dev` 分支：此分支是工作分支，是不稳定的。在需要发布新版本时：把 `dev` 分支合并到 `master` 上，在 `master` 分支上发布新版本
  + `own-branch`：团队每个人自己的工作分支，时不时的将工作进度合并到 `dev` 分支上，构成整个团队的开发进度
  + `issue` 分支：此分支是 `Bug` 分支，每个 `Bug` 都可以通过一个新的临时分支来修复，如 `issue-001`，修复后再合并分支，然后将临时分支删除
  + `feature` 分支：开发新功能，实验性功能分支；每添加一个新功能，可以新建一个 `feature` 分支，在上面开发，完成后合并分支，最后删除该  `feature` 分支

### 查看分支

+ 查看 `HEAD` 指向：`$ git show HEAD`

+ 查看当前本地版本库的所有分支：`$ git branch`

+ 查看当前本地版本库与远程仓库的所有分支：`$ git branch -a`

+ 查看分支的合并情况：用带参数的 `git log` 也可以看到分支的合并情况
  + `$ git log --graph`
  + `$ git log --graph --pretty=oneline`
  + `$ git log --graph --pretty=oneline --abbrev-commit`

+ 查看本地分支与其远程跟踪分支（上游分支）：`git branch -vv`
  + 注：此命令可比较本地分支与其跟踪分支的提交状况

### 比较分支的不同

+ 查看 `dev` 分支有，而 `master` 分支没有的：`$ git log dev ^master`
  + 注：两个分支比较，`^` 表示对应分支没有的提交

+ 查看 `dev` 分支比 `master` 分支多提交了哪些内容：`$ git log master..dev`
  + 注：`..` 后面的分支比之前的分支多提交了哪些内容

+ 不知道谁提交的多谁提交的少，只想知道有什么不同：`$ git log dev...master`

+ 比较不同时显示出每个提交是在哪个分支上：`$ git log --left-right dev...master`
  + 注：显示结果中：`<` 代表提交在 `dev` 分支上，`>` 代表提交在 `master` 分支上

+ 比较本地分支与远程分支的不同：`$ git log -p <local-branch>..origin/<remote-branch>`
  
### 创建分支

+ 创建本地新分支：`$ git branch new`
  + 注：以最新一次 `commit` 为参考创建一个新分支 `new`,新分支的提交日志与参考的提交日志一致

+ 以某次 `commit` 为参考创建本地新分支：`git branch branch_name [commit_id/HEAD/master]`
  + 注：参考只要是一个可以标识 `commit` 的引用就可以

+ 创建远程新分支：`$ git push origin new`
  + 注：此命令作用是将本地当前分支内容推送到远程分支，但是如果远程仓库中没有 `new` 分支，那么就会创建新分支 `new` 并推送内容

+ 切换分支：`$ git checkout new`
  + 注：切换到分支 `new`

+ 创建新分支并切换到新分支：`$ git checkout -b new`
  + 注：创建一个新分支 `new`，并切换到此新分支。相当于执行了两条命令：
    + `$ git branch new`
    + `$ git checkout new`

+ 基于远程分支创建本地分支：`$ git checkout -b new origin/new`
  + 注：本地新建一个分支 `new`，并切换到新建的分支 `new`，并且建立本地分支 `new` 与远程分支 `origin/new` 的跟踪关系
  + 此命令可以自定义本地分支名称，但是本地分支和远程分支的名称最好一致

+ 基于远程分支创建本地分支：`$ git checkout --track origin/<branch-name>`
  + 注：此命令创建的本地分支与远程分支同名，并且自动建立跟踪关系，同时切换到本地新建分支

+ 建立本地分支和远程分支的关联：`$ git branch --set-upstream-to=origin/dev dev`
  + 注：建立本地 `dev` 分支与远程 `origin/dev` 分支的链接

### 合并分支

+ 合并分支：把当前分支与被合并分支两个分支的最新快照以及二者最近的共同祖先进行三方合并，合并的结果是生成一个新的快照，并提交

+ 合并指定分支到当前分支：`$ git merge new`
  + 注：`git merge` 命令用并于合指定分支到当前分支。比如当前分支是 `master` ，那么此命令就是将 `new` 分支合并到 `master` 上
  + 注：此命令使用的是 `fast forward` 模式，在这种模式下，删除被合并分支后，会丢掉分支信息

+ 合并远程分支到本地当前分支：`$ git merge origin/<branch-name>`

+ 合并指定分支到当前分支并且不使用 `fast forward` 模式：`$ git merge --no-ff -m "commit message" <branch-name>`
  + 注：`--no-ff` 表示强制禁用 `fast forward` 模式，Git 就会在`merge` 时生成一个新的 `commit`，这样，从分支历史上就可以看出分支信息

### 变基：`rebase`

+ [详情参阅](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)

+ Git 中，整合来自不同分支的修改主要有两种方法：`merge` 以及 `rebase`，即合并分支与变基

+ 变基：`rebase` 命令将提交到某一分支（当前需要变基的分支）上的所有修改都移至另一分支(目标基底)上，就好像“重新播放”一样。

+ 请注意，无论是通过变基，还是通过三方合并，整合的最终结果所指向的快照始终是一样的，只不过提交历史不同罢了。 变基是将一系列提交按照原有次序依次应用到另一分支上，而合并是把最终结果合在一起
+ 执行变基操作后，视需要在目标基底分支上进行合并分支，将目标基底更新

+ **变基的风险**，使用变基要用它得遵守一条准则：
  + **不要对在你的仓库外有副本的分支执行变基**
  + 总的原则是：只对尚未推送或分享给别人的本地修改执行变基操作清理历史，从不对已推送至别处的提交执行变基操作

+ 将当前分支变基到另一分支（目标基底）：`$ git rebase master`
  + 注：此例中目标基底是 `master` 分支，将当前分支的提交整合到 `master` 分支

+ 将从一个分支上创建的分支变基到另一个分支：`$ git rebase --onto master server client`
  + 此例中： `client` 分支是从`server` 分支上创建的，只想单独变基 `client` 分支到 `master` 分支
  + 以上命令的意思是：取出 `client` 分支，找出处于 `client` 分支和 `server` 分支的共同祖先之后的修改，然后把它们在 `master` 分支上重放一遍

+ 快速地进行变基：`$ git rebase master server`
  + 注：此命令可以直接将特性分支（即本例中的 `server`）变基到目标分支（即 `master`）上。这样做能省去你先切换到 `server` 分支，再对其执行变基命令的多个步骤

### 删除分支

+ 撤销上一次的合并分支：`$ git merge --abort`

+ 删除当前本地版本库的指定分支：`$ git branch -d new`
  + 注：删除分支 `new`，此分支必须是被合并过的分支

+ 强制删除未合并过的分支：`$ git branch -D <branch-name>`
  + 注：分支存在修改但还没有被合并，如果删除将会丢失修改，系统会阻止删除操作。如果要强行删除，需要使用大写的 `-D` 参数

+ 删除远程仓库指定分支：
  + 方式一：`$ git push origin -d new`
  + 方式二：`$ git push origin :new`

### 储藏分支 - `stash`

+ 储存并隐藏未完结的修改/未提交的修改：`$ git stash`
  + 注：将工作区和暂存区中没有 `commit` 的内容隐藏起来，之后在工作区中就是干净的。把当前工作现场“储藏”起来，可以等到以后恢复现场后继续工作
  + 注：可以多次将未提交的修改储藏，如同一个栈
  + 注：当想要切换分支时当前分支存在未提交的修改时，不能切换分支，此时可使用此命令将未提交的修改储藏起来，再切换到其他分支

+ 查看 `stash` 储藏的内容：`$ git stash list`

+ 将 `stash` 最后一条记录储藏的内容恢复到工作区：`$ git stash apply`
  + 注：执行此命令将内容恢复后，`stash` 内容并不删除，你需要用 `git stash drop` 来删除
  + 注：最后一条记录如同栈顶

+ 将指定的 `stash` 储藏的内容恢复到工作区：`$ git stash apply stash@{num}`
  + 注：将 `stash` 储藏的内容的第 `num` 条记录恢复到工作区，`num` 从 0 开始

+ 移除 `stash` 储藏的内容：`$ git stash drop`
  + 注：此命令每次只能删除一条储藏记录

+ 恢复的同时删除 `stash` 内容：`$ git stash pop`
  + 注：当恢复时没有产生冲突，此命令恢复的同时会删除此次 `stash` 内容记录
  + 注：当恢复时产生冲突，此命令恢复之后会保留此次 `stash` 内容记录
  
--------------------------------------------------

## 标签管理

+ 标签：`tag` 是一个让人容易记住的有意义的名字，它跟某个 `commit` 绑在一起

+ Git 的标签是版本库的快照，但其实它就是指向某个 `commit` 的指针（跟分支很像,但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的

+ 标签默认是打在分支最新提交的 `commit` 上的

+ 注意：标签总是和某个 `commit` 挂钩。如果这个 `commit` 既出现在 `master` 分支，又出现在 `dev` 分支，那么在这两个分支上都可以看到这个标签

### 查看标签

+ 查看所有标签：`$ git tag`

+ 查看指定标签的信息：`$ git show <tag-name>`

### 新建标签

+ 给某个分支打标签：`$ git tag <tag-name>`
  + 在 Git 中打标签非常简单，首先，切换到需要打标签的分支上,然后打上标签

+ 给指定的 `commit_id` 打上标签：`$ git tag <tag-name> <commit_id>`
  + 注：如果当时忘记了打标签，那么事后还可以根据对应的 `commit_id` 来创建标签

+ 创建带有说明的标签：`$ git tag -a v0.1 -m "version 0.1 released" commit_id`
  + 用 `-a` 指定标签名，`-m` 指定说明文字

+ 推送某个标签到远程：`$ git push origin <tagname>`
  + 注：推送本地标签到远程，所以此标签必须已存在

+ 一次性推送全部未推送过的本地标签到远程：`$ git push origin --tags`

### 删除标签

+ 因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除

+ 删除本地某个标签：`$ git tag -d <tag-name>`

+ 删除远程仓库的标签：`$ git push origin :refs/tags/<tag-name>`

+ 删除远程仓库的标签：`$ git push origin -d <tag-name>`

## 常见的问题

### 与文件操作相关

+ **设置 'Git' 的用户主目录：**
  + 问题描述：在 'Windows' 下安装 'Git' 后，默认的用户主目录和开始路径一般都是：C:\Users\用户名。很多人都不想将一些运行文件放在默认路径下，想要放在别的地方
  + 解决方式：可采用配置环境变量的方式修改用户主目录的默认路径
    + 鼠标右键 '此电脑' --> '属性' --> '高级系统设置' --> '环境变量' -->'***的用户变量'
    + 新建 用户变量 `Home`，将路径设置为你想要的路径
    + 如果在原来的用户主目录下已经生成了.ssh、.gnupg、.bash_history、.gitconfig等文件，直接把这些文件拷贝到你新设定的用户主目录下即可
    + 重启 'Git' 即可

+ **设置 'Git' 的开始路径：**
  + 问题描述：在 'Windows' 下安装 'Git' 后，默认的用户主目录和开始路径一般都是：C:\Users\用户名。但是这并不是你放置 'repository' 的工作目录，不想每次启动 'Git Bash' 或者 'Git CMD' 都要手动进入你的工作目录
  + 解决方式：通过修改快捷方式的路径即可修改默认路径
    + 找到 'Git Bash' 或者 'Git CMD' 的快捷方式，鼠标右键 --> '属性'
    + 会看到 '目标' 和 '起始位置' ，如下：

    ```text
      目   标 : G:\Git\git-bash.exe --cd-to-home
      起始位置 : %HOMEDRIVE%%HOMEPATH%
    ```
  
    + 去掉 '目标'的：`--cd-to-home`
    + 修改 '起始位置' 为自定义的 'Git' 本地仓库的路径，如：`G:\Git Workspace`
    + 重启 'Git' 即可

+ **输入 `$ git add <file>` 后出现警告：**
  + 如下

    ```text
    warning: LF will be replaced by CRLF in ......  
    The file will have its original line endings in your working directory.
    ```

  + 问题原因：原因是路径中存在 / 的符号转义问题：false就是不转换符号，默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题
  + 解决方法，输入命令:
    `$ git config --global core.autocrlf false`

### 与远程仓库相关

+ **如果在第一次推送到远程仓库时出现不能推送的错误**
  + 显示以下的错误信息

    ```text
    error: failed to push some refs to 'https://github.com/your/repository.git'
    hint: Updates were rejected because the remote contains work that you do not have locally. This is usually caused by another repository pushing
    hint: ......
    ```
  
  + 问题原因：因为远程仓库中已经进行了初始化操作，已经存在 readme.md 或者其他文件了，所以需要先pull下来。命令如下：`$ git pull origin master`

  + 这时又会报错：

    ```text
    前面有些内容， ......
    fatal: refusing to merge unrelated histories
    ```

  + 解决方法：意思是说这两个库有不相干的历史记录而无法合并，重新执行以下命令即可成功 `pull`：
  `$ git pull origin master --allow-unrelated-histories`
  + 但是这时会可能会提示必须输入提交的信息，默认会打开 vim 编辑器，先按 i 切换到插入模式，
    写完后 Esc→：→wq 即可保存退出编辑器。如果不进入 vim 编辑器，则会自动生成一个合并代码的 `commit`。
    然后再使用前面的命令push将本地提交推送到远程仓库。后面如果本地还有 `commit`，
    就可以直接用 `$ git push origin master` 推送

+ **使用 `$ git push` 命令时出现错误**
  + 提示如下：

    ```text
      fatal: The current branch master has no upstream branch.
      To push the current branch and set the remote as upstream, use git push --set-upstream origin master
    ```

  + 接下来输入：`$ git branch --set-upstream-to=origin/master master`；又会出现如下提示：
  
    ```text
      error: the requested upstream branch 'upstream/master'does not exist
      hint:......
    ```
  
  + 问题原因：本地分支没有与远程分支建立关联

  + 解决方法:
    + 第一步：`$ git pull origin master --allow-unrelated-histories`
    + 第二步：`$ git branch --set-upstream-to=origin/master master`

### 与分支操作相关

+ **当执行合并分支命令 `git merge` 时，出现冲突导致不能合并分支**
  + 出现如下提示：

    ```text
    Auto-merging test.txt
    CONFLICT (content): Merge conflict in test.txt
    Automatic merge failed; fix conflicts and then commit the result.
    ```

  + 问题原因：很可能是当前分支与想要合并的分支各自都分别有新的提交
    + 这时可以使用 `git status` 查看冲突的文件，也可以使用 `cat` 命令查看冲突的内容
    + 可以使用 `$ git log --graph` 查看分支合并情况

  + 解决方法：当 Git 无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
    + 解决冲突就是把 Git 合并失败的文件 **手动编辑** 为我们希望的内容，再提交

+ **删除分支出错**
  + 显示如下错误信息

    ```text
    error: The branch 'temp' is not fully merged.
    If you are sure you want to delete it, run 'git branch -D temp'.
    ```

  + 问题原因：提示被删除的分支修改了内容还没有未被合并过，如果删除将会丢失修改，系统会阻止删除操作。
  + 解决方法：合并分支之后再删除，或者强制删除分支：`$ git branch -D <branch-name>`

## 使用 Git 注意的地方

+ **`cd` 命令进行目录切换时需要注意目录中的空格：**
  + 解决方式一：使用 `""` 引号将目录名括起来
  + 解决方式二：使用 `\` 加上空格，代替直接输入空格

+ **分支合并**
  + 如果需要合并的两个分支**都各自有新的提交**，这时使用分支合并命令很可能会产生冲突。此时应该 **手动编辑** 合并失败的文件为我们希望的内容。然后再提交，最后再重新执行合并命令
  + 如果只是其中一个分支有新的提交，合并应该就没有问题