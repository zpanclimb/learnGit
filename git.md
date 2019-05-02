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

## Git Bash界面

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
+ 查看提交日志：
  + 查看全部的提交日志：`$ git log`
  + 将每一个提交日志缩减为一行显示：`$ git log --pretty=oneline`
  + 查看指定文件的提交日志，并且缩减为一行显示：`$ git log --pretty=oneline <file>`
+ 查看命令行历史记录：`$ history`
+ 版本回退：
  + 方式一：`$ git reset --hard HEAD^`
    + 注：上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成 `HEAD~100`
  + 方式二：`$ git reset --hard commit_id`
    + `commit_id` 指的是每次提交操作的版本号，使用 `$ git log` 命令可以查看全部提交操作的版本号，一般取版本号的前 7 位即可

--------------------------------------------------

## 远程仓库

+ 连接远程仓库：
  + 方式一：`$ git remote add origin git@github.com:your/yourRepos.git`
  + 方式二：`$ git remote add origin https://github.com/your/yourRepos.git`
  + 注：这里远程仓库的默认名字是 `origin`,也可以改成别的

+ 推送到远程仓库同时指定默认远程仓库：`$ git push -u origin master`
  + 注：第一次将本地仓库推送到远程仓库是可使用此命令。此命令将本地的 `master` 分支推送到 `origin` 主机，同时指定 `origin` 为默认主机，后面就可以不加任何参数使用 `git push` 了。
  + 注：第一次推送本地 `master` 分支时，加上了 `-u` 参数，Git 不但会把本地的  `master` 分支内容推送的远程新的 `master` 分支，还会把本地的 `master` 分支和远程的 `master` 分支关联起来，在以后的推送或者拉取时就可以简化命令。

+ 推送到远程仓库：`$ git push origin master`
  + 注：将当前分支推送到远程仓库 `origin` 的分支 `master`

+ 推送到远程仓库：`$ git push origin`
  + 注：将当前分支推送到远程仓库 `origin` 的对应分支。如果当前分支只有一个追踪分支，那么分支名称都可以省略

+ 推送本地分支到远程仓库的另一个分支：`$ git push origin local:master`
  + 注：将本地分支 `local` 推送到远程仓库的 `master` 分支

+ 从远程仓库拉取：`$ git pull origin master`
  + 注：将远程仓库 `origin` 的分支 `master`拉取到当前分支

+ 克隆远程仓库：`$ git clone git@github.com/your/yourRepos.git`
  + 注：将远程仓库完整的克隆一份到本地 Git 开始路径下

--------------------------------------------------

## 分支管理

+ 分支：
  + 版本库的提交操作只会提交到当前分支上，其他分支不受影响
  + 对文件做的更改如果在当前分支上提交，那么改变只能在此分支上可以查看，其他分支上看不到文件的改变，其他分支还停留在最后一次提交的位置
  + 合并分支之后，彼此分支之间的进度就统一了

+ 查看当前本地版本库的所有分支：`$ git branch`
+ 查看当前本地版本库与远程仓库的所有分支：`$ git branch -a`

+ 创建新分支：`$ git branch new`
  + 注：创建一个新分支 `new`

+ 切换分支：`$ git checkout new`
  + 注：切换到分支 `new`

+ 创建新分支并切换到新分支：`$ git checkout -b new`
  + 注：创建一个新分支 `new`，并切换到此新分支。相当于执行了两条命令：
    + `$ git branch new`
    + `$ git checkout new`

+ 合并指定分支到当前分支：`$ git merge new`
  + 注：`git merge` 命令用并于合指定分支到当前分支。比如当前分支是 `master` ，那么此命令就是将 `new` 分支合并到 `master` 上
  + 注：此命令使用的是 `fast forward` 模式，在这种模式下，删除被合并分支后，会丢掉分支信息

+ 合并指定分支到当前分支并且不使用 `fast forward` 模式：`$ git merge --no-ff -m "commit message" new`
  + 注：`--no-ff` 表示强制禁用 `fast forward` 模式，Git 就会在`merge` 时生成一个新的 `commit`，这样，从分支历史上就可以看出分支信息

+ 删除当前本地版本库的指定分支：`$ git branch -d new`
  + 注：删除分支 `new`

+ 删除远程仓库指定分支：
  + 方式一：`$ git push origin -d new`
  + 方式二：`$ git push origin :new`

+ 查看分支的合并情况：用带参数的 `git log` 也可以看到分支的合并情况
  + `$ git log --graph`
  + `$ git log --graph --pretty=oneline`
  + `$ git log --graph --pretty=oneline --abbrev-commit`

--------------------------------------------------

## 常见的问题

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

+ **`cd` 命令进行目录切换时需要注意目录中的空格：**
  + 解决方式一：使用 `""` 引号将目录名括起来
  + 解决方式二：使用 `\` 加上空格，代替直接输入空格

+ **输入 `$ git add <file>` 后出现警告：**
  + 如下

    ```text
    warning: LF will be replaced by CRLF in ......  
    The file will have its original line endings in your working directory.
    ```

  + 问题原因：原因是路径中存在 / 的符号转义问题：false就是不转换符号，默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题
  + 解决方法，输入命令:
    `$ git config --global core.autocrlf false`

+ **如果在第一次推送到远程仓库时出现不能推送的错误**
  + 显示以下的错误信息

    ```text
    error: failed to push some refs to 'https://github.com/your/repository.git'
    hint: Updates were rejected because the remote contains work that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
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

## 使用 Git 注意的地方

+ **分支合并**
  + 如果需要合并的两个分支**都各自有新的提交**，这时使用分支合并命令很可能会产生冲突。此时应该 **手动编辑** 合并失败的文件为我们希望的内容。然后再提交，最后再重新执行合并命令
  + 如果只是其中一个分支有新的提交，合并应该就没有问题