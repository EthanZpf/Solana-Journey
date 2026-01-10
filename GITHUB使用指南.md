# GitHub 使用完整指南

## 📋 目录
1. [什么是 GitHub？](#什么是-github)
2. [初始设置](#初始设置)
3. [基本 Git 命令](#基本-git-命令)
4. [将项目上传到 GitHub](#将项目上传到-github)
5. [日常使用流程](#日常使用流程)
6. [常见问题解决](#常见问题解决)

---

## 什么是 GitHub？

GitHub 是一个代码托管平台，你可以：
- 保存你的代码在云端（永不丢失）
- 记录代码的每次修改历史
- 与他人协作开发
- 展示你的项目作品

---

## 初始设置

### 步骤 1：安装 Git

**macOS 用户**（你的系统）：
```bash
# 检查是否已安装 Git
git --version

# 如果未安装，使用 Homebrew 安装（推荐）
brew install git

# 或者下载官方安装包：https://git-scm.com/download/mac
```

### 步骤 2：配置 Git（只需要做一次）

打开终端（Terminal），执行以下命令：

```bash
# 设置你的用户名（替换为你的真实姓名或昵称）
git config --global user.name "你的名字"

# 设置你的邮箱（使用 GitHub 注册邮箱）
git config --global user.email "your-email@example.com"

# 查看配置是否成功
git config --global --list
```

### 步骤 3：创建 GitHub 账号

1. 访问 https://github.com
2. 点击右上角 "Sign up" 注册账号
3. 完成邮箱验证

### 步骤 4：创建 SSH 密钥（推荐）或使用 HTTPS

**方式 A：使用 HTTPS（简单，但每次推送需要输入密码）**

直接跳到下一步即可。

**方式 B：使用 SSH 密钥（推荐，更安全方便）**

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "your-email@example.com"

# 按回车接受默认路径
# 设置密码（可选，直接回车跳过）

# 复制公钥内容
cat ~/.ssh/id_ed25519.pub

# 将输出的内容复制，然后：
# 1. 登录 GitHub
# 2. 点击右上角头像 -> Settings
# 3. 左侧菜单选择 "SSH and GPG keys"
# 4. 点击 "New SSH key"
# 5. 粘贴公钥内容，保存
```

---

## 基本 Git 命令

### 初始化仓库（第一次使用）

在项目文件夹中执行：

```bash
# 初始化 Git 仓库
git init

# 查看当前状态
git status
```

### 三个基本区域

Git 有三个区域：
1. **工作区**：你正在编辑的文件
2. **暂存区**：准备提交的文件
3. **仓库区**：已保存的历史版本

### 常用命令

```bash
# 查看文件状态
git status

# 添加文件到暂存区
git add .              # 添加所有文件
git add README.md      # 添加单个文件

# 提交更改（保存到本地仓库）
git commit -m "描述这次更改的内容"

# 查看提交历史
git log

# 查看文件差异
git diff

# 撤销更改
git checkout -- 文件名  # 撤销工作区的修改
git reset HEAD 文件名   # 取消暂存
```

---

## 将项目上传到 GitHub

### 步骤 1：在 GitHub 上创建新仓库

1. 登录 GitHub
2. 点击右上角的 "+" 号 -> "New repository"
3. 填写仓库名称（例如：`Solana-Journey`）
4. **不要**勾选 "Initialize this repository with a README"（因为我们本地已有文件）
5. 点击 "Create repository"

### 步骤 2：连接本地仓库和 GitHub

GitHub 会显示一些命令，选择 **HTTPS** 或 **SSH** 方式：

**使用 HTTPS：**
```bash
# 添加远程仓库地址（替换 YOUR_USERNAME 和 YOUR_REPO_NAME）
git remote add origin https://github.com/YOUR_USERNAME/Solana-Journey.git

# 首次推送
git branch -M main
git push -u origin main
```

**使用 SSH：**
```bash
# 添加远程仓库地址（替换 YOUR_USERNAME 和 YOUR_REPO_NAME）
git remote add origin git@github.com:YOUR_USERNAME/Solana-Journey.git

# 首次推送
git branch -M main
git push -u origin main
```

如果提示输入密码或遇到错误，请查看 [常见问题解决](#常见问题解决) 部分。

---

## 日常使用流程

### 每次修改代码后的标准流程：

```bash
# 1. 查看修改了哪些文件
git status

# 2. 添加修改的文件到暂存区
git add .              # 或 git add 具体文件名

# 3. 提交更改（写清楚这次做了什么）
git commit -m "更新学习笔记：添加 Solana 基础概念"

# 4. 推送到 GitHub
git push
```

### 示例：添加一篇新的学习笔记

```bash
# 假设你创建了新文件：docs/day1-solana-basics.md

# 查看状态
git status
# 输出：新文件 docs/day1-solana-basics.md

# 添加到暂存区
git add docs/day1-solana-basics.md

# 提交
git commit -m "添加第一天学习笔记：Solana 基础概念"

# 推送到 GitHub
git push
```

### 提交信息规范

好的提交信息示例：
- ✅ `"添加学习笔记：智能合约开发基础"`
- ✅ `"修复 README 中的拼写错误"`
- ✅ `"更新项目结构，添加 examples 文件夹"`
- ❌ `"更新"`
- ❌ `"修改文件"`

---

## 常见问题解决

### 问题 1：首次 push 提示需要登录

**解决方案：**

如果使用 HTTPS，GitHub 已不再支持密码验证，需要使用 Personal Access Token：

1. GitHub 右上角头像 -> Settings
2. 左侧菜单选择 "Developer settings"
3. 选择 "Personal access tokens" -> "Tokens (classic)"
4. 点击 "Generate new token (classic)"
5. 勾选 `repo` 权限
6. 生成后复制 token（只显示一次！）
7. 使用 token 作为密码

**更推荐使用 SSH**，一次设置后无需每次输入密码。

### 问题 2：push 被拒绝（push rejected）

**原因：** 远程仓库有本地没有的更新

**解决方案：**

```bash
# 先拉取远程更新
git pull origin main

# 如果有冲突，解决冲突后再：
git add .
git commit -m "解决合并冲突"
git push
```

### 问题 3：忘记添加某个文件

```bash
# 添加遗漏的文件
git add 文件名

# 修改最后一次提交（不要修改已推送的提交）
git commit --amend --no-edit

# 强制推送（谨慎使用）
git push --force-with-lease
```

### 问题 4：想撤销最后一次提交

```bash
# 撤销提交但保留文件修改
git reset --soft HEAD~1

# 撤销提交并丢弃文件修改（谨慎！）
git reset --hard HEAD~1
```

### 问题 5：查看远程仓库地址

```bash
git remote -v
```

### 问题 6：修改远程仓库地址

```bash
# 修改为新的地址
git remote set-url origin 新的仓库地址
```

---

## 🎓 进阶学习

### 创建分支（用于实验新功能）

```bash
# 创建并切换到新分支
git checkout -b 新功能分支名

# 在新分支上工作...
git add .
git commit -m "新功能的改动"

# 切换回主分支
git checkout main

# 合并分支
git merge 新功能分支名
```

### 查看文件的历史版本

```bash
# 查看某个文件的所有修改历史
git log -- 文件名

# 查看某个文件在某个版本的完整内容
git show 提交ID:文件名
```

---

## 💡 实用技巧

1. **使用 `.gitignore` 文件**：忽略不需要版本控制的文件（如 node_modules、.env 等）

2. **经常提交**：小步快跑，经常提交小的改动

3. **写清晰的提交信息**：方便以后查找和理解历史

4. **定期推送到 GitHub**：避免本地文件丢失

5. **使用 GitHub Desktop**：如果你不熟悉命令行，可以使用图形界面工具
   - 下载：https://desktop.github.com/

---

## 📚 推荐资源

- [Git 官方文档](https://git-scm.com/doc)
- [GitHub 官方指南](https://guides.github.com/)
- [Git 教程 - 廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)
- [Learn Git Branching](https://learngitbranching.js.org/) - 互动式学习 Git

---

## ❓ 需要帮助？

如果遇到问题：
1. 查看错误信息，搜索解决方案
2. 访问 [GitHub 社区论坛](https://github.community/)
3. 查看 Stack Overflow

祝你学习愉快！🚀
