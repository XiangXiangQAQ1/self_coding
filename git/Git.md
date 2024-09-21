# **github**
1. 图片加速
    根据你的 GitHub 仓库地址改为正确的 CDN 地址：
    https://cdn.jsdelivr.net/gh/{你的github用户名}/{仓库名称}/{具体路径}
    例如：https://cdn.jsdelivr.net/gh/xiangxiangQAQ1/self_coding@main/photos/fpx.jpg
    xiangxiangQAQ1: github 用户名，self_coding: 仓库名称，photos/fpx.jpg: 具体路径




**以下文字\统一代表空格**
# **tips**
1. HEAD^: 上一个版本 HEAD^^: 上上一个版本 HEAD~100: 上100个版本
2. alias: 创建命令别名 
    ```bash
    alias load=“/usr/local/bin/git”
    ```


# **初始化设置**

- 配置用户名：
    ```bash
    git config --global user.name "Your Name"
    ```

- 配置邮箱：
    ```bash
    git config --global user.email "mail@example.com"
    ```

- 存储配置
    ```bash
    git config --global credential.helper store
    ```

# **创建仓库**

- 创建一个新的本地仓库：
    ```bash
    git init <project-name>
    如果省略<project-name>，则在当前目录创建。
    ```

- 克隆一个远程仓库：
    ```bash
    git clone <url>
    ```


# **四个区域**
- 工作区（Working Directory）：就是你在电脑里能实际看到的目录
- 暂存区（Stage/Index）：用来临时存放未提交的内容 一般在.git目录下的index中
- 本地仓库（Repository）：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库
- 远程仓库（Remote Repository）：托管在远程服务器上的仓库 常用的有GitHub、GitLab、Gitee

# **文件状态**

- Untracked：未跟踪，未被纳入版本控制
    ```bash
    新建的文件
    ```

- Modified：已修改，已修改但未被纳入版本控制
    ```bash
    编辑过的文件
    ```

- Staged：已暂存，已修改且已纳入版本控制的文件
    ```bash
    git add <file>
    ```

- Committed：已提交，已记录在本地仓库中的版本
    ```bash
    git commit -m "message"
    ```

# **查看状态和差异**

- **git status**: 查看仓库状态，列出还未提交的新的或修改的文件。
- **git log --oneline**: 查看提交历史，`--oneline` 表示简介模式。
- git log --graph --oneline --decorate --all: 查看提交历史，图形化显示。
-  q: 退出查看历史
- **git rm \<file>**: 从工作区和暂存区删除一个文件，并将这次删除放入暂存区。
    也可以先用 rm \<file> 删除文件，然后再用 git add \<file> 将删除放入暂存区。
- **git diff**: 显示工作区与暂存区的差异。
  - git diff --cached: 显示暂存区与上次提交之间的差异。
  - git diff head head^: 查看工作区和上一个版本之间的差异。
  - git diff --stat: 显示工作区和暂存区的差异统计信息。
  - 
- **git diff \<commit-id> \<commit-id>**: 查看两个提交之间的差异。
- **git ls-files**: 查看暂存区以及提交中的文件列表。

# **添加和提交**

- **git add \<file>**: 添加一个文件到暂存区。例如，`git add .` 表示添加所有文件到暂存区。
- **git commit -m\<file>**: 提交一个文件到本地仓库。
- **git commit -m "message"**: 提交所有暂存区的文件到本地仓库。
- **git commit -am "message"**: 提交所有已修改的文件到本地仓库，同时跳过暂存区的步骤。

# **撤销和恢复**

- **git mv \<file> \<new-file>**: 移动一个文件到新的位置。
- **git rm  \<file>**: 删除一个文件，并将这次删除放入暂存区。
- 
- **git checkout \<file> \<commit-id>**: 恢复一个文件到之前的版本。
- **git checkout -b dev 615d31f**：chenckout也可以恢复分支
- **git revert \<commit-id>**: 重置当前分支的 HEAD 为之前的某个提交，并删除所有之后的提交。
  - `--hard` 参数表示重置工作区和暂存区。
  - `--soft` 参数表示仅重置暂存区。
  - `--mixed` 参数表示重置工作区。
- **git reset --mixed \<commit-id>**: 重置当前分支的 HEAD，保留工作区更改。
- **git restore --staged \<file>**: 撤销暂存区的文件，重新放回工作区（`git add` 的反向操作）。
- 恢复工作区的的文件(恢复到最近的提交状态，丢弃对文件的所有未提交更改，但不会对暂存区的文件更改)
     ```bash
    git restore  file.txt
    ```
- 接受自己的版本，即用当前分支的内容解决冲突
    ```bash
    git restore --ours file.txt
    ```
- 接受别人的版本，即用另一个分支的内容解决冲突
    ```bash
    git restore --theirs file.txt
    ```


- **恢复工作区中的文件**
恢复工作区中的文件到最近的提交状态（即丢弃对文件的所有未提交更改）：
```bash
git restore file.txt
```

- **git reflog** : 查看历史操作记录(但是不能恢复已删除的文件)


# **分支**

- **git branch**:查看所有本地分支， 当前分支前面会有一个星号*， -r查看远程分支， -a查看所有分支。
- **git branch <branch-name>**:创建一个新的分支。
- **git branch -d <branch-name>**: 删除一个已经合并的分支。
- **git branch -D <branch-name>**: 删除一个分支，不管是否合并。
- **git tag <tag-name>**: 给当前的提交打上标签，通常用于版本发布。
- **git merge --no-ff -m message <branch-name>**:合并分支， --no-ff参数表示禁用 Fast Forward模式， 合并后的历史有分支， 能看出曾经做过合并， 而-ff参数表示使用 FastForward模式， 合并后的历史会变成一条直线。


- **git squash <branch-name>**:合并&挤压（squash） 所有提交到一个提交。
- rebase ：会将当前分支的提交历史“复制”到目标分支上，并保留当前分支的提交历史
- rebase 操作可以把本地未 push 的分叉提交历史整理成直线看起来更加直观 但是 如果多人协作时不要对已经推送到远程的分支执行 rebase 操作;
rebase 不会产生新的提交 而是把当前分支的每一个提交都“复制”到目标分支上 然后再把当前分支指向目标分支 而 merge 会产生一个新的提交这个提交有两个分支的所有修改

```bash
git checkout <dev>
git rebase <main>
```




# **Stash**

- **git stash save "message"**: Stash 操作可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。
  - **-u**: 将所有未跟踪的文件也一并存储。
  - **-a**: 将所有未跟踪的文件和忽略的文件也一并存储。
  - **save 参数**: 存储的信息，可以不写。
- **git stash list**: 查看所有 stash。
- **git stash pop**: 恢复最近一次 stash。
- **git stash pop stash@{2}**: 恢复指定的 stash（stash@{2} 表示第三个 stash，stash@{0} 表示最近的 stash）。
- **git stash apply**: 重新应用最近一次 stash。
- **git stash drop stash@{2}**:pop和apply的区别是， pop会把stash内容删除， 而 apply不会。可以使用 git stash drop 来删除stash。
- **git stash clear**: 删除所有 stash。



# **远程仓库**
- **git remote add \<remote-name> \<remote-url>**: 添加远程仓库。
- **git remote -v**: 查看远程仓库。
- **git remote rm \<remote-name>**: 删除远程仓库。
- **git remote rename \<old-name> \<new-name>**: 重命名远程仓库。
- git push :提交代码到远程仓库（然后再发起 pull request）
- **git pull --rebase**: 将本地改动的代码 rebase 到远程仓库的最新代码上，以保持干净、线性的提交历史。
- **git pull \<remote-name> \<branch-name>**: 从远程仓库拉取代码，默认拉取远程仓库名 `origin` 的 `master` 或 `main` 分支。(会自动合并一次，若失败，则依然需要手动合并)
- **git push \<remote-name> \<branch-name>**: 推送代码到远程仓库（然后再发起 pull request）。
- **git fetch \<remote-name>**: 获取所有远程分支，但并不会自动合并。
- **git branch -r**: 查看远程分支。
- **git fetch \<remote-name> \<branch-name>**: Fetch 某一个特定的远程分支。


# **特殊文件**

- **git** Git仓库的元数据和对象数据库
- **.gitignore**: 忽略文件，不需要提交到仓库的文件,只能忽略未被追踪的文件
     
- **.gitattributes**: 指向当前分支的指针。
- **.git**: Git 仓库的元数据和对象数据库。
- **.gitkeep**: 使空目录被提交到仓库。
- **.gitmodules**: 记录子模块的信息。
- **.gitconfig**: 记录仓库的配置信息。



# **GitFlow**
GitFlow 是一种流程模型，用于在Git上管理软件开发项目

- 主分支（master/main）：代表了项目的稳定版本，每个提交到主分支的代码都应该是经过测试和审核的。
- main上会有版本号的标签，1.2.3 分别代表了主板本、次版本、修订版本。
- 
- 开发分支（develop)：用于日常开发。所有的功能分支、发布分支和修补分支都应该从开发分支派生出来。

- 功能分支（feature）：用于开发单独的功能或者特性。每个功能分支都应该从开发分支派生，并在开发完成后合并回开发分支。
- 例如 feature-login-page

- 发布分支（release)：用于准备项目发布。发布分支应该从开发分支派生，并在准备好发布版本后合并回主分支和开发分支。


- 热修复分支（hotfix）：用于修复主分支上的紧急问题。热修复分支应该从主分支派生，并在修复完成后，合并回主分支和开发分支。
-  hotfix-#issueid-desc
-  


# **Git grapg**
- 这个到还好，就是对比分支的提交历史,然后观察各个提交的差异

# **Git history**
- 可以查看文件的修改历史
    - more:selecte this commit
- view: 显示这次commit的修改信息
- worksapce：显示工作区与上次commit中对应文件的差异

# **一种常用的工作流**
1. 每次想在本地修改代码之前，先执行 `git pull` 命令，拉取最新的代码。
2. 而后，git checkout -b my feature，新建一个分支，并切换到该分支。
3. 进行下一步操作前，先用diff，看一下自己到底做了什么改变
4. git add，把文件存在暂存区，then git commit
5. git push origin my feature，把分支推送到远程仓库。
6. 很有可能push的时候main分支又有改动了，所以需要 git switch main，然后 git pull origin main，拉取最新的代码。
7. 接着，git switch my feature -> git merge main or git rebase main，合并main分支到my feature分支。
8. 然后，git push -f origin mu-feature，强制推送到远程仓库。(如果前面使用了rebase命令)
9. 而后，在github上发起一个pull request，等待review
10. 最后，管理者squash and merge
11. 最后的最后，git switch main -> git pull origin main -> git branch -d my feature

# **参考资料**
1. 【【GeekHour】一小时Git教程】https://www.bilibili.com/video/BV1HM411377j?p=12&vd_source=49973f1ca384c0644711e64309368e8e
2. 【十分钟学会正确的github工作流，和开源作者们使用同一套流程】https://www.bilibili.com/video/BV19e4y1q7JJ?vd_source=49973f1ca384c0644711e64309368e8e