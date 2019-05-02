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

+ 重置 `Git Bash` 界面：`$ reset`

+ 清除 `Git Bash` 界面中的内容：`$ clear`

--------------------------------------------------

## 用户信息

+ 添加用户：`$ git config --global user.name "your name"`

+ 添加邮箱：`$ git config --global user.email your@example.com`

+ 查看用户名：`$ git config user.name`

+ 查看邮箱：`$ git config user.email`

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

+ 覆盖文件内容：`$ echo "message" > <file>`

+ 追加内容到文件末尾：`$ echo "message" >> <file>`

+ 显示暂存区和工作区的文件差异：`$ git diff`

+ **文件的重要操作：删除与恢复**
  + **删除**
    + `$ rm <file>`
    + `$ git rm <file>`

  + **恢复文件，或者说撤销删除操作**
    + 从工作区删除，还没有添加到暂存区，恢复文件只需要一步：`$ git checkout -- <file>`
    + 从工作区和暂存区删除，但是还没有提交到版本库，恢复文件需要两步：
      + 第一步，从暂存区移除：`$ git reset HEAD <file>`
      + 第二步，撤销删除操作：`$ git checkout -+ <file>`
    + 如果删除操作已经提交至版本库：那么只能使用版本回退
      + 版本回退方式一：`$ git reset --hard HEAD^`
      + 版本回退方式二：`$ git reset --hard commit_id`

--------------------------------------------------

## 版本库相关操作

+ 从已存在的目录新建一个版本库：`$ git init`

+ 将操作从工作区添加到暂存区：`$ git add <file>`

+ 将操作从暂存区提交到版本库：`$ git commit -m "此次提交说明"`
  + `add` 命令可以执行多次，将多个操作添加到暂存区；`commit` 命令可以一次性将暂存区的操作提交至版本库：

    ```text
      git add file1.txt
      git add file2.txt
      git commit -m "此次提交了两个文件"
    ```

+ 移除暂存区中文件准备提交状态：`$ git reset HEAD <file>`

+ 查看工作区与暂存区的内容：`$ git status`

+ 查看提交日志：`$ git log`
  + 将每一个提交日志缩减为一行显示：`$ git log --pretty=oneline`
  + 查看指定文件的提交日志，并且缩减为一行显示：`$ git log --pretty=oneline <file>`
  + 注：此命令不能查看已删除的提交日志，即如果进行了版本回退，那么回退版本号之后再提交的日志都不能查看，如要查看全部提交日志，请使用 `$ git reflog`

+ 查看所有分支的所有提交日志：`$ git reflog`
  + 注：此命令可以查看所有分支的所有提交日志（包括 `commit` 和 `reset` 的操作），包括已经被删除的 `commit` 记录，`git log` 则不能查看已经被删除了的 `commit` 记录

+ 查看命令行历史记录：`$ history`

+ 版本回退：
  + 方式一：`$ git reset --hard HEAD^`
    + 注：上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成 `HEAD~100`
  + 方式二：`$ git reset --hard commit_id`
    + `commit_id` 指的是每次提交操作的版本号，使用 `$ git log` 命令可以查看全部提交操作的版本号，一般取版本号的前 7 位即可

--------------------------------------------------

## 远程仓库

### 查看远程仓库的信息

+ 查看远程仓库的信息：`$ git remote`

+ 查看远程仓库的详细信息：`$ git remote -v`
  + 可抓取的远程仓库地址：`origin  git@github.com:your/yourRepos.git (fetch)`
  + 可推送的远程仓库地址：`origin  git@github.com:your/yourRepos.git (push)`
  + 注：如果没有抓取或者推送的权限，就看不到相应的地址

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

### 从远程仓库拉取

+ Git 中从远程的分支获取最新的版本到本地有两个命令：
  + `git fetch`：从远程获取最新版本到本地，不会自动 `merge`
  
      ```text
      git fetch orgin master //将远程仓库的 master 分支下载到本地当前 branch 中
      git log -p master ..origin/master //比较本地的 master 分支和 origin/master 分支的差别
      git merge origin/master //进行合并
      ```

    + 也可以用以下指令：

    ```text
    git fetch origin master: temp  //从远程仓库 master 分支获取最新，在本地建立 temp 分支
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

+ 从远程仓库拉取：`$ git pull origin master`
  + 注：将远程仓库 `origin` 的分支 `master` 拉取到当前分支

+ 从远程分支拉取到本地指定分支：`$ git pull origin <remote-branch>:<local-branch>`

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

+ 查看当前本地版本库的所有分支：`$ git branch`

+ 查看当前本地版本库与远程仓库的所有分支：`$ git branch -a`

+ 查看分支的合并情况：用带参数的 `git log` 也可以看到分支的合并情况
  + `$ git log --graph`
  + `$ git log --graph --pretty=oneline`
  + `$ git log --graph --pretty=oneline --abbrev-commit`

+ 查看本地分支的远程跟踪分支（上游分支）：`git branch -vv`

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

+ 在本地创建与远程分支对应的分支：`$ git checkout -b new origin/new`
  + 注：基于远程分支创建本地分支。本地新建一个分支 `new`，并切换到新建的分支 `new`，并且建立本地分支 `new` 与远程分支 `origin/new` 的跟踪关系，本地和远程分支的名称最好一致

+ 建立本地分支和远程分支的关联：`$ git branch --set-upstream-to=origin/dev dev`
  + 注：建立本地 `dev` 分支与远程 `origin/dev` 分支的链接

### 合并分支

+ 合并指定分支到当前分支：`$ git merge new`
  + 注：`git merge` 命令用并于合指定分支到当前分支。比如当前分支是 `master` ，那么此命令就是将 `new` 分支合并到 `master` 上
  + 注：此命令使用的是 `fast forward` 模式，在这种模式下，删除被合并分支后，会丢掉分支信息

+ 合并指定分支到当前分支并且不使用 `fast forward` 模式：`$ git merge --no-ff -m "commit message" new`
  + 注：`--no-ff` 表示强制禁用 `fast forward` 模式，Git 就会在`merge` 时生成一个新的 `commit`，这样，从分支历史上就可以看出分支信息

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