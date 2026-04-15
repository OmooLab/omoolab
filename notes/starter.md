1. 安装 Git
打开 windows powershell，运行
```powershell
winget install Git.Git
```

安装完毕后，所有终端我们都选择 Git Bash

设置本设备 git 的身份信息
```bash
git config --global user.name [your-name]
git config --global user.email  [your-email]
```

初始化 lfs 以获取对大文件的支持
```bash
git lfs install
```

2. 安装 VS Code
```bash
winget install vscode
```

4. 安装 Volta 
```bash
winget install Volta.Volta
```

重启终端，安装 node 

```bash
volta install node
```

5. 安装 claude code
```bash
volta install @anthropic-ai/claude-code
```

（可选）安装 cc-switch
https://github.com/farion1231/cc-switch/releases

（可选）安装 vscode claude 插件
https://code.claude.com/docs/zh-CN/vs-code

（可选）安装 obsidian claude 插件
https://github.com/YishenTu/claudian/releases