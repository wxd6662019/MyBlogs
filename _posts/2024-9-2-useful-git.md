---
title: useful-git
date: 2024-9-2

---

# 有用的命令

### 1. **基本操作**

- **初始化仓库**
  ```bash
  git init
  ```

- **克隆仓库**
  ```bash
  git clone <repository-url>
  ```
  
- **清楚git缓存**

  ```bash
  git credential-cache exit 
  ```

### 2. **查看状态**

- **查看当前状态**
  ```bash
  git status
  ```

- **查看提交历史**
  ```bash
  git log
  ```

### 3. **文件操作**

- **添加文件到暂存区**
  ```bash
  git add <file>
  ```
  添加所有文件：
  ```bash
  git add .
  ```

- **从暂存区移除文件**
  ```bash
  git reset <file>
  ```

- **查看文件差异**
  ```bash
  git diff
  ```

### 4. **提交更改**

- **提交更改**
  ```bash
  git commit -m "Commit message"
  ```

### 5. **分支管理**

- **查看分支**
  ```bash
  git branch
  ```

- **创建新分支**
  ```bash
  git branch <branch-name>
  ```

- **切换分支**
  ```bash
  git checkout <branch-name>
  ```

- **合并分支**
  ```bash
  git merge <branch-name>
  ```

### 6. **远程操作**

- **查看远程仓库**
  ```bash
  git remote -v
  ```

- **添加远程仓库**
  ```bash
  git remote add origin <repository-url>
  ```

- **推送到远程仓库**
  ```bash
  git push origin <branch-name>
  ```

- **拉取远程更新**
  
  ```bash
  git pull origin <branch-name>
  ```
  
- **重新设置远程仓库**

  ```bash
  git remote set-url origin https://github.com/你的用户名/新的仓库名.git
  ```

### 7. **其他实用命令**

- **撤销上一次提交（保留更改）**
  ```bash
  git reset --soft HEAD~1
  ```

- **强制推送**
  
  ```bash
  git push --force
  ```
  
- **查看已追踪的文件**
  ```bash
  git ls-files
  ```

### 8. **标签管理**

- **创建标签**
  ```bash
  git tag <tag-name>
  ```

- **推送标签到远程**
  ```bash
  git push origin <tag-name>
  ```
