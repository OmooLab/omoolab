## 从自己的分支开始

1. 拉取分支

```bash
git clone [repo.git]
cd [repo-name]
```

2. 创建自己的分支

```bash
git checkout -b [your-name]/[do-something] # 比如 manan/dev
```

3. 首次推送分支到远程

```bash
git push -u origin [branch-name]
```

4. 本地一些改动

```bash
git add .
git commit -m [message]
```

5. 推送改动

```bash
git push
```

## 合并到`main`

确保自己的东西和`main`别差太远了，合并前，先从`main`来取并合并到自己的分支

```bash
git checkout main
git pull # origin main
git checkout [branch-name] # 回到特征分支
git merge main
```

或者直接

```bash
# 确保在特征分支
git pull origin main
```

如果冲突，会进入`([branch-name]|MERGING)` 状态

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