## 工作流

- 大家在自己的「个人分支」工作，互不干扰
- 通过「提交」，有选择性地确认改动到「个人分支」（个人审核 AI）
- 不时地，接收其他人在「主分支」的改动
- 通过「合并请求」，有监督地把确认改动到「主分支」（团队审核个人）


```mermaid
flowchart LR
  文件改动 -- 提交 --> 个人分支 -- 合并请求 --> 主分支
```


## 在自己的「个人分支」工作

**1. 下载仓库**

浏览器打开仓库地址 <https://git.omoolab.xyz/[orgn-name]/[repo-name]>，点右上的 Code 按钮，点击 Open with VS Code

![](assets/Pasted%20image%2020260415192621.png)

> 或 Bash 执行 `git clone [repo.git]`


**2. 创建自己的「个人分支」**

点左下角的`main`，点击`Create new branch...`，然后输入分支名`[your-name]/[do-something]`(比如`manan/dev`)

![](assets/Pasted%20image%2020260415201156.png)

> 或 Bash 执行 `git checkout -b [your-name]/[do-something]`

创建后，首次推送分支到远程。这样远程也有属于你的分支了

![](assets/Pasted%20image%2020260415201626.png)

> 或 Bash 执行 `git push -u origin [branch-name]`


## 通过「提交」来确认改动到「个人分支」

**1. 添加到 Staged Changes**

仓库的任何改动都会罗列在 Changes 下，此时它们都是暂时的。点击 + 来添加到 Staged Changes 下（你可以只添加部分改动）

![](assets/Pasted%20image%2020260415202442.png)

> 或 Bash 执行 `git add [file]`

**2. 提交 Staged Changes**

手动输入 Commit Message 来说明改动了什么，或者点击小星按钮让 AI 来帮忙总结。最后点击 Commit，完成「提交」。至此改动才被确认，记录到了 Git History 中。

![](assets/Pasted%20image%2020260415202608.png)

> 或 Bash 执行 `git commit -m [message]`

最后，你需要「推送」到远程仓库来完成和远程的同步，点击 Push。至此远程仓库也同步为了最新的版本。

**3. 同步到远程的「个人分支」**

![](Pasted%20image%2020260415202931.png)

> 或 Bash 执行 `git push`

这是工作中最常见的循环，一边制作，一边 commit + push

## 接收其他人在「主分支」的改动

当你在自己的分支工作的时候，其他人也在不断更新「主分支」`main`。有时需要对齐一下，同步并合并来自`main`的改动到你自己的分支。

点击 Pull from...，并选择`origin/main`（注意不是`main`分支，它是本地的，并非最新）

![](assets/Pasted%20image%2020260415230956.png)

> 或 Bash 执行 `git pull origin main`

如果冲突，会进入`([branch-name]|MERGING)` 状态，具体查看 [解决冲突](#解决冲突)

## 通过「合并请求」来确认改动到「主分支」

「主分支」`main`通过这样方式来接收大家的更新，这一步叫「合并请求」（Pull Request，简称 PR）。

浏览器访问仓库主页，切换到「个人分支」，点击 New Pull Request 按钮（3）

![](assets/Pasted%20image%2020260415232911.png)

确认一下合并方向是否正确，然后填写 PR 标题和内容（改了什么，加了什么），最后点击 Create Pull Request

![](assets/Pasted%20image%2020260415233225.png)

PR 会加入队列，等待审核通过。通过后就会合并到`main`

![](assets/Pasted%20image%2020260415233620.png)

> 注意，如果在提 PR 后，如果你又更新了你的分支，不必再次提 PR

> 注意，在提 PR 前，一定要在本地执行[同步「主分支」的改动](#同步「主分支」的改动)（并 push 到了远程）

## 解决冲突

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