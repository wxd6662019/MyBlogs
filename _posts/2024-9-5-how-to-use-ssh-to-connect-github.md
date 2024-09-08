---
title: how to use ssh to connect github
date: 2024-9-5

---

### 1. 检查 SSH 是否安装

确保你的系统上已经安装了 SSH 客户端。在大多数 Linux 和 macOS 系统中，SSH 客户端已经预装。Windows 用户可以使用 Git Bash 或 Windows Subsystem for Linux (WSL)。

检查您的系统中是否已生成 SSH 密钥

```c
ls -al ~/.ssh 
    //如果 id_rsa.pub 文件存在，说明您已经生成了 SSH 密钥。
```

### 2. 生成 SSH 密钥

如果你还没有 SSH 密钥，可以通过以下命令生成一个：

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
/**解析：
-t rsa ：指定密钥类型，rsa表示使用rsa算法生成密钥
-b 4096：指令密钥的位数，表示生成4096位的密钥
-C “”： 表示为密钥添加注释，方便识别密钥的用途或持有者
**/
```

- 按照提示，选择密钥保存的位置（默认是 `~/.ssh/id_rsa`），并设置一个密码（可选）。

### 3. 添加 SSH 密钥到 SSH 代理

启动 SSH 代理并添加你的 SSH 密钥：

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

​	`ssh-agent` 的主要作用是管理 SSH 密钥，以便在需要时提供身份验证。如果代理未运行，你将无法使用 `ssh-add` 添加新密钥。关闭 `ssh-agent` 后，你将无法使用它来管理密钥。如果你尝试建立新的 SSH 连接，系统将要求你手动输入密钥密码，或者使用 `-i` 参数指定密钥，貌似会默认找id_rsa这个私钥

### 4. 添加 SSH 密钥到 GitHub

1. **复制 SSH 密钥**：

   使用以下命令复制你的公钥到剪贴板：

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

   

2. **登录到 GitHub**：
   
   - 进入 [GitHub](https://github.com)，登录你的账户。
   
3. **添加 SSH 密钥**：
   - 点击右上角的个人头像，选择 **Settings**。
   - 在左侧菜单中选择 **SSH and GPG keys**。
   - 点击 **New SSH key**，粘贴复制的公钥，并给这个密钥命名。
   - 点击 **Add SSH key**。

### 5. 使用 SSH 进行 Git 操作

将你的 Git 仓库的远程 URL 更改为 SSH 格式。你可以通过以下命令查看当前远程 URL：

```bash
git remote -v
```

如果当前 URL 是 HTTPS 格式，你需要更改为 SSH 格式，使用以下命令：

```bash
git remote set-url origin git@github.com:username/repo.git
```

将 `username` 和 `repo` 替换为你的 GitHub 用户名和仓库名。

### 6. 验证 SSH 连接

使用以下命令验证 SSH 连接是否成功：

```bash
ssh -T git@github.com
```

如果连接成功，你应该看到一条欢迎信息。

### 7. 进行 `git push`

现在，你可以使用 `git push` 命令将更改推送到 GitHub：

```bash
git push origin main
```

将 `main` 替换为你的分支名称。

### ssh-keygen -R 47.94.20.51 ，重新连接的命令，删除KnownHosts文件里这个ip的记录
