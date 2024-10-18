# **Git 中的一些基本概念**

**工作区、暂存区和 Git 仓库区**

* 工作区（Working Directory）： 当我们在本地创建一个 Git 项目，或者从 GitHub 上 clone 代码到本地后，项目所在的这个目录就是“工作区”。这里是我们对项目文件进行编辑和使用的地方。
* 暂存区（Staging Area）： 暂存区是 Git 中独有的一个概念，位于 .git 目录中的一个索引文件，记录了下一次提交时将要存入仓库区的文件列表信息。使用 git add 指令可以将工作区的改动放入暂存区。
* 仓库区 / 本地仓库（Repository）： 在项目目录中，.git 隐藏目录不属于工作区，而是 Git 的版本仓库。这个仓库区包含了所有历史版本的完整信息，是 Git 项目的“本体”。


## 1. 常用 Git 操作


**基础指令**

| 指令             | 描述                                       |
| ---------------- | ------------------------------------------ |
| `git config`   | 配置用户信息和偏好设置                     |
| `git init`     | 初始化一个新的 Git 仓库                    |
| `git clone`    | 克隆一个远程仓库到本地                     |
| `git status`   | 查看仓库当前的状态，显示有变更的文件       |
| `git add`      | 将文件更改添加到暂存区                     |
| `git commit`   | 提交暂存区到仓库区                         |
| `git branch`   | 列出、创建或删除分支                       |
| `git checkout` | 切换分支或恢复工作树文件                   |
| `git merge`    | 合并两个或更多的开发历史                   |
| `git pull`     | 从另一仓库获取并合并本地的版本             |
| `git push`     | 更新远程引用和相关的对象                   |
| `git remote`   | 管理跟踪远程仓库的命令                     |
| `git fetch`    | 从远程仓库获取数据到本地仓库，但不自动合并 |

**进阶指令**

| 指令                | 描述                                                 |
| ------------------- | ---------------------------------------------------- |
| `git stash`       | 暂存当前工作目录的修改，以便可以切换分支             |
| `git cherry-pick` | 选择一个提交，将其作为新的提交引入                   |
| `git rebase`      | 将提交从一个分支移动到另一个分支                     |
| `git reset`       | 重设当前 HEAD 到指定状态，可选修改工作区和暂存区     |
| `git revert`      | 通过创建一个新的提交来撤销之前的提交                 |
| `git mv`          | 移动或重命名一个文件、目录或符号链接，并自动更新索引 |
| `git rm`          | 从工作区和索引中删除文件                             |

每个指令都有其特定的用途和场景，详细的使用方法和参数可以通过命令行的帮助文档（`git command -h`,例如 `git pull -h`）来获取更多信息。


## 2. 食用小 tips

[](https://github.com/InternLM/Tutorial/blob/camp3/docs/L0/Git/readme.md#4-%E9%A3%9F%E7%94%A8%E5%B0%8F-tips)

### 2.1 全局设置 vs. 本地设置

[](https://github.com/InternLM/Tutorial/blob/camp3/docs/L0/Git/readme.md#41-%E5%85%A8%E5%B1%80%E8%AE%BE%E7%BD%AE-vs-%E6%9C%AC%E5%9C%B0%E8%AE%BE%E7%BD%AE)

* **全局设置** ：这些设置影响你在该系统上所有没有明确指定其他用户名和电子邮件的 Git 仓库。这是设置默认用户名和电子邮件的好方法。
* **本地设置** ：这些设置仅适用于特定的 Git 仓库。这对于你需要在不同项目中使用不同身份时很有用，例如区分个人和工作项目。

### 2.2 如何配置

[](https://github.com/InternLM/Tutorial/blob/camp3/docs/L0/Git/readme.md#42-%E5%A6%82%E4%BD%95%E9%85%8D%E7%BD%AE)

1. **全局设置用户信息** 打开终端或命令提示符，并输入以下命令来设置全局用户名和电子邮件地址：

   ```shell
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

   这里的 `"Your Name"` 和 `"your.email@example.com"` 应替换为你自己的姓名和电子邮件。
2. **本地设置用户信息** 首先，确保你当前处于你想要配置的 Git 仓库的目录中。然后，输入以下命令来仅为该仓库设置用户名和电子邮件地址：

   ```shell
   git config --local user.name "Your Name"
   git config --local user.email "your.email@example.com"
   ```

   同样，替换 `"Your Name"` 和 `"your.email@example.com"` 为该特定项目中使用的姓名和电子邮件。

### 2.3 验证设置

[](https://github.com/InternLM/Tutorial/blob/camp3/docs/L0/Git/readme.md#43-%E9%AA%8C%E8%AF%81%E8%AE%BE%E7%BD%AE)

在设置完用户信息后，你可能想要验证这些设置以确保它们被正确应用。

* **查看全局配置** ：

```shell
  git config --global --list
```

* **查看仓库配置** ：

```shell
  git config --local --list
```

* **查看特定配置项** ：

```shell
  git config user.name
  git config user.email
```

### 2.4 Git 四步曲

[](https://github.com/InternLM/Tutorial/blob/camp3/docs/L0/Git/readme.md#44-git-%E5%9B%9B%E6%AD%A5%E6%9B%B2)

在Git的日常使用中，下面四步曲是常用的流程，尤其是在团队协作环境中。

**添（Add）**

* **命令** ：`git add <文件名>` 或 `git add .`
* **作用** ：将修改过的文件添加到本地暂存区（Staging Area）。这一步是准备阶段，你可以选择性地添加文件，决定哪些修改应该被包括在即将进行的提交中。

**提（Commit）**

* **命令** ：`git commit -m '描述信息'`
* **作用** ：将暂存区中的更改提交到本地仓库。这一步是将你的更改正式记录下来，每次提交都应附带一个清晰的描述信息，说明这次提交的目的或所解决的问题。

**拉（Pull）**

* **命令** ：`git pull`
* **作用** ：从远程仓库拉取最新的内容到本地仓库，并自动尝试合并到当前分支。这一步是同步的重要环节，确保你的工作基于最新的项目状态进行。在多人协作中，定期拉取可以避免将来的合并冲突。

**推（Push）**

* **命令** ：`git push`
* **作用** ：将本地仓库的更改推送到远程仓库。这一步是共享你的工作成果，让团队成员看到你的贡献。

帮助团队成员有效地管理和同步代码，避免工作冲突，确保项目的顺利进行。正确地使用这些命令可以极大地提高开发效率和协作质量。
