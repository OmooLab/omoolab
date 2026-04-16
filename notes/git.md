# Git 基操

## 工作流程

我们选择 Git 作为版本管理的工具（确保已经安装 Git 和 VS Code，详见[starter](starter.md)），工作流程主要是以下 4 点：

- 大家在自己的「个人分支」工作，互不干扰
- 通过「提交」，有选择性地，确认改动到「个人分支」（个人审核 AI）
- 不时地，接收其他人在「主分支」的改动
- 通过「合并请求」，有监督地，确认改动到「主分支」（团队审核个人）

```mermaid
flowchart LR
  文件改动 -- 提交 --> 个人分支 -- 合并请求 --> 主分支
```

通过上述流程，个人的本地改动被，有选择性地、有监督地被同步到项目主分支。

有效避免同步盘方案下，高频改动文件的冲突和 AI 无法参与的尴尬。这样，即释放了本地创作的限制，又规范了线上协作的管理，还解决了私有盘无法分享的问题。接下来，我将详细描述操作步骤

### 在自己的「个人分支」工作

**1. 下载仓库（Repository）**

浏览器打开仓库地址 <https://git.omoolab.xyz/[orgn-name]/[repo-name]>，点右上的 Code 按钮，点击 Open with VS Code

![](assets/Pasted%20image%2020260415192621.png)

> 或 Bash 执行 `git clone [repo.git]`

> 默认不拉取大文件，以确保本地仓库体积
> Bash 执行 `git lfs pull --include [folder]` 来下载仅需要的大文件

**2. 创建自己的个人分支**

点左下角的`main`，点击 Create new branch...，然后输入分支名`[your-name]/[do-something]`(比如`manan/dev`)

![](assets/Pasted%20image%2020260415201156.png)

> 或 Bash 执行 `git checkout -b [your-name]/[do-something]`

创建后，首次推送分支到远程。这样远程也有属于你的分支了

![](assets/Pasted%20image%2020260415201626.png)

> 或 Bash 执行 `git push -u origin [branch-name]`


### 通过「提交」来确认改动到「个人分支」


**1. 有选择性地添加（Add）到暂存改动**

仓库的任何改动都会罗列在 Changes 下，此时它们并没有得到确认。点击 + 来添加到 Staged Changes 下（你可以只添加部分改动）

![](assets/Pasted%20image%2020260415202442.png)

> 或 Bash 执行 `git add [file]`

**2. 提交（Commit）暂存改动**

输入「提交说明」来记录改动了什么（或者点击小星按钮让 AI 来帮忙总结）。点击 Commit 按钮来确认改动。

![](assets/Pasted%20image%2020260415202608.png)

> 或 Bash 执行 `git commit -m [message]`

**3. 推送（Push）到远程的「个人分支」**

点击三个点按钮打开菜单，点击 Push 按钮

![](Pasted%20image%2020260415202931.png)

> 或 Bash 执行 `git push`

这步是工作中最常用的：一边工作，一边适时地 Add > Commit > Push

### 接收其他人在「主分支」的改动

当你在自己分支工作的时候，其他人也在不断更新「主分支」`main`。有时需要对齐一下，拉取（Pull）并合并（Merge）来自`main`的改动到你自己的分支。

点击三个点按钮打开菜单，点击 Pull from...，并选择`origin/main`（注意不是`main`分支，它是本地的，并非最新）

![](assets/Pasted%20image%2020260415230956.png)

> 或 Bash 执行 `git pull origin main`

如果冲突，会进入`([branch-name]|MERGING)` 状态，详见 [解决冲突](#解决合并冲突)

### 通过「合并请求」来确认改动到「主分支」

合并请求（Pull Request，PR）就是「个人分支」合并入「主分支」的申请

浏览器访问仓库主页，切换到「个人分支」，点击 New Pull Request 按钮（3）

![](assets/Pasted%20image%2020260415232911.png)

确认一下合并方向是否正确，然后填写 PR 标题和内容（改了什么，加了什么），最后点击 Create Pull Request

![](assets/Pasted%20image%2020260415233225.png)

PR 会加入队列，等待审核通过。通过后就会合并到`main`啦。

![](assets/Pasted%20image%2020260415233620.png)

> 注意，如果在提 PR 后，如果你又更新了你的分支，不必再次提 PR

> 注意，在提 PR 前，一定要在本地执行[同步「主分支」的改动](#同步「主分支」的改动)（且 push 到了远程「个人分支」）



## 一些小问题
### 多设备编辑同一分支

首先不推荐这样做，但是为了一个设备，新加分支也很没必要。但如果由一个人操作这些设备，比如个人的 macbook、iphone 共同编辑，只要严格遵守下面两条：
- 在 A 设备编辑，Commit 后立即 Push，以保证远程仓库及时更新
- 切换到 B 设备，在编辑前立即 Pull，以保证 B 设备及时更新

> 为什么不用 icloud？因为这样可以实现部分同步，能适应复杂的文件夹，打开也更快。

### 解决合并冲突

解决完冲突后，继续

```bash
git merge --continue
```

大文件处理完合并后，变成指针文件，这时候用下面指令拉回

```bash
git lfs pull
```

或者退出，不解决

```bash
git merge --abort
```
取消曾经追踪过的文件，但不删除文件

```bash
git rm --cached [file]
```