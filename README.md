# 我的第一个仓库

一份 Git 基础教学笔记，帮助你理解从本地到 GitHub 的完整工作流。

---

## 一、Git 是什么？

Git 是一个**分布式版本控制系统**。它可以：

- 记录文件的每一次修改历史
- 随时回退到任意历史版本
- 多人协作时合并各自的修改

---

## 二、三个核心区域

理解这三个区域，就理解了 Git 的核心逻辑：

```
┌─────────────┐   git add   ┌─────────────┐   git commit  ┌─────────────┐
│  工作目录    │  ────────→  │   暂存区     │  ──────────→  │  本地仓库    │
│ Working Dir │             │ Staging Area│               │ Local Repo  │
└─────────────┘             └─────────────┘               └─────────────┘
      ↑                                                          │
      │                     git checkout / git restore           │
      └──────────────────────────────────────────────────────────┘
```


| 区域       | 说明         | 对应命令         |
| -------- | ---------- | ------------ |
| **工作目录** | 你实际编辑文件的地方 | 直接修改文件       |
| **暂存区**  | 即将被提交的快照   | `git add`    |
| **本地仓库** | 已保存的历史记录   | `git commit` |


---

## 三、新建仓库

### 方式一：本地初始化（你当前使用的方式）

```bash
# 1. 创建项目文件夹
mkdir my-first-repo
cd my-first-repo

# 2. 初始化 Git 仓库（会生成隐藏的 .git 目录）
git init

# 3. 创建第一个文件
echo "# 我的第一个仓库" > README.md

# 4. 第一次提交
git add README.md
git commit -m "初始提交"
```

### 方式二：从 GitHub 克隆已有仓库

```bash
git clone https://github.com/用户名/仓库名.git
cd 仓库名
```

---

## 四、配置 Remote（远程仓库）

本地仓库和 GitHub 之间通过 **remote** 连接。`origin` 是默认的远程仓库别名。

```bash
# 查看已配置的远程仓库
git remote -v

# 添加远程仓库（首次关联 GitHub 时使用）
git remote add origin https://github.com/用户名/仓库名.git

# 修改远程地址
git remote set-url origin https://github.com/新用户名/新仓库名.git

# 删除远程仓库
git remote remove origin
```

本仓库已配置的远程地址：

```
origin → https://github.com/Lysander-dog/my-first-repo.git
```

---

## 五、完整工作流

日常开发中最常用的流程：

```
修改文件 → git add → 暂存区 → git commit → 本地仓库 → git push → GitHub
```

### 第 1 步：修改文件（工作目录）

在编辑器中直接修改文件，例如编辑 `README.md`。

### 第 2 步：查看状态

```bash
git status
```

输出会告诉你哪些文件被修改了、哪些还没暂存。

### 第 3 步：添加到暂存区

```bash
# 暂存单个文件
git add README.md

# 暂存所有修改
git add .

# 暂存某个目录下的所有文件
git add src/
```

### 第 4 步：提交到本地仓库

```bash
git commit -m "描述这次修改做了什么"
```

提交信息要简洁明了，例如：

- `添加 Git 基础教学文档`
- `修复登录页面的样式问题`
- `更新 README`

### 第 5 步：推送到 GitHub

```bash
# 首次推送并设置上游分支
git push -u origin main

# 之后的推送
git push
```

---

## 六、常用命令速查

### 查看信息

```bash
git status          # 查看当前状态
git log             # 查看提交历史
git log --oneline   # 简洁版提交历史
git diff            # 查看未暂存的修改
git diff --staged   # 查看已暂存、未提交的修改
```

### 撤销操作

```bash
# 撤销工作目录的修改（危险：会丢失未保存的改动）
git restore 文件名

# 将文件从暂存区移出（保留工作目录的修改）
git restore --staged 文件名

# 修改最近一次提交信息（尚未 push 时）
git commit --amend -m "新的提交信息"
```

### 从远程拉取

```bash
git pull            # 拉取并合并远程最新代码
git fetch           # 只拉取，不自动合并
```

---

## 七、分支基础

分支让你可以在不影响主代码的情况下开发新功能。

```bash
git branch                  # 查看所有分支
git branch 新分支名          # 创建新分支
git checkout 新分支名        # 切换到该分支
git checkout -b 新分支名     # 创建并切换（常用）

# 合并分支到当前分支
git merge 新分支名

# 删除分支
git branch -d 新分支名
```

---

## 八、`.gitignore` 文件

告诉 Git 哪些文件**不需要**被追踪，例如：

```
# 依赖目录
node_modules/

# 环境变量（含敏感信息）
.env

# 系统文件
.DS_Store

# 编译产物
dist/
*.log
```

---

## 九、一次完整的练习

在本仓库中练习完整流程：

```bash
# 1. 确认当前状态
git status

# 2. 修改 README.md（你正在看的这个文件）

# 3. 暂存修改
git add README.md

# 4. 提交到本地仓库
git commit -m "添加 Git 基础教学文档"

# 5. 推送到 GitHub
git push
```

推送成功后，打开 [https://github.com/Lysander-dog/my-first-repo](https://github.com/Lysander-dog/my-first-repo) 即可在网页上看到最新内容。

---

## 十、概念对照表


| 术语  | 英文                | 含义                |
| --- | ----------------- | ----------------- |
| 仓库  | Repository / Repo | 项目的版本历史存储         |
| 提交  | Commit            | 一次快照，附带说明信息       |
| 分支  | Branch            | 独立的开发线            |
| 远程  | Remote            | 托管在 GitHub 等平台的仓库 |
| 克隆  | Clone             | 把远程仓库复制到本地        |
| 推送  | Push              | 把本地提交上传到远程        |
| 拉取  | Pull              | 把远程最新代码下载到本地      |
| 合并  | Merge             | 把两个分支的修改合在一起      |
| 冲突  | Conflict          | 两人改了同一处，需手动解决     |


---

## 参考资源

- [Git 官方文档（中文）](https://git-scm.com/book/zh/v2)
- [GitHub 官方指南](https://docs.github.com/zh/get-started)
- [Learn Git Branching（可视化练习）](https://learngitbranching.js.org/?locale=zh_CN)

