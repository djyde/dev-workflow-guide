# 开发团队工作流程规范

Author: Randy Lu <randypriv@gmail.com>

Last updated: 2016-01-19

## 前言

此规范意在规范开发团队的开发流程，如果做到以下所有

## 项目开发迭代流程

一个项目必须有一个主要负责人，该负责人负责控制项目的 Pull Request, issue, tag 等等，即整个项目的代码质量和方向。不允许直接对项目进行代码提交，所有代码均通过 merge request 进行合并。

> 此规定主要针对大于两个项目贡献者的项目。

### 分支管理

项目的主分支为 `master`，不稳定的开发分支为 `dev`。`master` 必须保证绝对可用性（即正常运行）。`dev` 分支为测试分支。除去这两个分支外，**在远程仓库中只能存在特性分支**。

> TIPS: 『特性分支』的意思是，此分支相对于正在运行的分支，只存在某一个特性的差别，通常用于不稳定的功能。

> 比如正在试验一个新的功能，这个新的功能在通过用户内测后才能决定是否成为正式功能，那么就可以在项目中从 `master` 中 checkout 出一个存在此功能的特性分支，试验时上线这个分支。最后如果决定纳入为正式功能，则合并到 `master`，否则下线该分支。

### 贡献代码

作为代码贡献者时，先把项目 fork 到自己的 namespace 下，再创建新的分支进行开发，分支名称可分为 `feature/foo`, `hotfix/bar` 等，由自己决定命名。开发进行完毕后可以对项目作出 pull request，等待负责人进行合并。

> TIPS: 开发时有可能出现开发时 master 分支或者 dev 分支指针前移的情况，这种情况下开发者尽量使用 rebase 将前移的 commit 合并，以避免多余的 merge log. 

> 关于 rebase 可以在 https://git-scm.com/book/en/v2/Git-Branching-Rebasing 查看更多。

### 提交代码

进行 commit 时，如果该 commit 与某 issue 相关，必须在 commit message 后添加 issue refer, 例如：

```bash
$ git commit -m '修复登录串号 fix kiwi-team/liubai-account#6'
```

> 这样做极有利于 code review，因为 Gitlab/Github 会在 issue 中自动显示相关 commit。

### 项目管理

项目负责人需要对项目的 issue 进行管理，比如打 tag, assign. `tag` 在 Gitlab 中称作 `label`, 可分为 `bug`, `enhancement`, `question` 等等，只要项目负责人能理解即可。

> TIPS: 正确使用 Milestone 功能可以使项目负责人对项目整体进度更清晰。

当 Milestone 完成后，项目即可进入测试阶段。测试完成后即可合并到 `master` 分支上线。

### 版本迭代

版本成功迭代后，项目负责人需要在 `master` 分支打 tag, `tag name` 为当前项目的版本号。

建议在 Gitlab/Github 上进行打 tag，tag message 列出该版本**新增了哪些功能**、**修复了哪些问题**；附件包含该版本所编译出来的可执行文件（比如打包后的 `apk`, 提供给其它平台使用的 `.js` 脚本等）。
