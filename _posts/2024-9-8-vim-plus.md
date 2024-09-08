---
title: vim-plus
date: 2024-9-8

---



查看当前linux版本

- `cat /etc/os-release` 或 `cat /etc/*release`
- `lsb_release -a` 显示 Linux Standard Base（LSB）和发行版信息

安装vim-plus

1. 确保软件包索引是最新的 `yum update`

   - **获取最新版本**：软件包索引包含可用软件包的列表及其版本信息。保持索引更新可以确保你安装的是最新版本，包含了安全补丁和新功能。

   - **避免冲突**：如果索引过时，可能会导致安装旧版本的包，进而引发依赖性问题或软件冲突。

2. 安装 EPEL 仓库  `yum install epel-release`

   - **EPEL（Extra Packages for Enterprise Linux）** 是一个由 Fedora 社区维护的仓库
   - **额外软件包**：默认的仓库可能不包含所有你需要的软件包，EPEL 提供了更多选择，包括 `vim-plus`。
   - **稳定性和支持**：EPEL 提供的软件包经过测试，通常适用于生产环境，能提供更好的稳定性。

3. ### 安装 vim-plus `yum install vim-enhanced`

4. 验证安装 `vim --version`

5. 安装git

6. 安装插件管理器（需要git依赖）

   ```bash
   curl -fLo ~/.vim/autoload/plug.vim --create-dirs \    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
   
   附加命令，需进入.vimrc文件使用
   #:PlugUpgrade 更新vim-plug
   #:PlugUpdate 更新插件
   #:PlugClean 清理插件
   #:h plug 查看帮助文档
   ```

