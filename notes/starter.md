# 必装软件/工具

## 安装 Git

Git 是版本管理工具，任何数字工作都离不开它。

打开 windows powershell，运行

```powershell
winget install Git.Git
```

安装时中注意下面两点，其他默认下一步
- 勾选添加 Git Bash 到终端（Windows Terminal）
- 选择`main`作为默认主分支名（默认是`master`）


安装完毕后，打开终端（Windows Terminal），点击 v 按钮，点击设置。默认配置文件选择 Git Bash，保存。重启终端，后面命令行的操作都通过终端的 Git Bash 完成

设置本设备 git 的身份信息

```bash
git config --global user.name [your-name]
git config --global user.email  [your-email]
```

初始化 lfs 以获取对大文件的支持

```bash
git lfs install
```


## 安装 VS Code

VS Code 是最基础的 IDE，AI 编程 IDE 都基于它的源码，例如Cursor。

```bash
winget install vscode
```

## 安装包管理器

AI Agent 实现功能就是靠的是「工具超市」提供小工具，而包管理器（Package Manager）负责从「工具超市」上下载、更新、管理它们。Agent 会由于实践方式不统一，导致设备上存在大量的乱装的东西。

目前世界上最大的两个「工具超市」
- Javascript 的 npm
- Python 的 pypi

给它们装最好的包管理器吧
### Volta

管理 Node.js 的工具，它可以比 npm 原生更好的管理由 Javascript 写的工具。

```bash
winget install Volta.Volta
```

重启终端，安装 node 

```bash
volta install node
```

### Uv

极速 Python 包和项目管理工具，不管是用 Python 做开发还是使用 Python 写的工具都离不开它

```bash
winget install --id=astral-sh.uv -e
```


## 安装 claude code

Claude code 不用介绍了，建议通过 [Volta](#Volta) 安装 Claude Code CLI

```bash
volta install @anthropic-ai/claude-code
```


（可选）安装 cc-switch
https://github.com/farion1231/cc-switch/releases

（可选）安装 vscode claude 插件
https://code.claude.com/docs/zh-CN/vs-code

（可选）安装 obsidian claude 插件
https://github.com/YishenTu/claudian/releases