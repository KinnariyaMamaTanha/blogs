---
title: WSL2 重新安装配置记录
math: false
mermaid: false
date: 2024-10-01 11:06:08
tags:
    - WSL2
    - linux
categories:
    - OS
---

由于之前的 WSL2 文件过于杂乱，我又不想收拾整理，故重新配置了一遍，希望能够满足 Python、C++、C、markdown 等语言的编写，并记录下来方便日后参考。

## 准备工作

1. 导出备份
```bash
 wsl --export Ubuntu-22.04 D:\WSL\Ubuntu2204\Ubuntu2204.tar
```
2. 把一些必要的文件夹移到 D 盘，方便转移回来，包括但不限于 `.config` 等文件与文件夹
3. 卸载：
```bash
wsl --unregister Ubuntu-22.04
```
4. 重新安装：直接点击原有的 Ubuntu-22.04 图标，自动安装（或前往微软应用商店），按照提示输入用户名、密码。
5. 导入到 D 盘中，网上教程很多，随便搜一个靠谱的就行。这里是我的：
```bash
wsl --export Ubuntu-22.04 D:\WSL\Ubuntu2204\Ubuntu2204.new.tar
wsl --unregister Ubuntu-22.04
wsl --import Ubuntu-22.04 D:\WSL\Ubuntu2204 D:\WSL\Ubuntu2204\Ubuntu2204.new.tar
```
6. 设置默认用户为 kinnariya：
```bash
ubuntu2204 config --default-user kinnariya
```
7. 此时磁盘空间占用约 1G

## 正式开始配置

1. 换源：参照 [ubuntu | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)，或者 [Ubuntu24.04 更换源地址（新版源更换方式） - 陌路寒暄 (jlqwer.com)](https://www.jlqwer.com/posts/7930.html)
2. 升级 apt 包：`sudo apt update && sudo apt upgrade`
3. 装 zsh 进行美化，使用 oh-my-zsh 和 powerlevel10k 主题，可以参考 [zsh 安装与配置：9 步打造高效命令行 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/441676276)
4. 安装 [neovim](https://neovim.io/)，拉取我本人的配置，见 <https://github.com/KinnariyaMamaTanha/KinanVim>
5. 转移原有文件，此时磁盘空间占用约 4.57G
6. 安装 fzf, lazygit, yazi，在 github 上搜
7. 安装 miniconda，参照 [Miniconda — Anaconda documentation](https://docs.anaconda.com/free/miniconda/index.html)，换源并创建 dl 环境
8. 进入 dl 环境，安装 pytorch、matplotlib、ipython，参见官网指南，17.5G
9. 安装 cuda、cudnn 等，参考我在 aiTour 里面贴的两个链接，34.5G，或者直接用 conda 装 `conda install cuda cudnn` （这样挺好，可以隔绝不同版本的 cuda 和 cudnn，而且空间占用也更少），注意版本号对应
10. 安装 docker，参考官方 [Install Docker Engine on Ubuntu | Docker Docs](https://docs.docker.com/engine/install/ubuntu/)，35G
11. 安装 texlive，参考[这篇教程](https://www.cnblogs.com/eslzzyl/p/17358405.html)，清理之前所有步骤的安装缓存
12. 登入 vscode，安装插件
13. 删除 snap，可参考<https://linux.cn/article-14567-1.html>
14. 配置 github ssh key
15. 安装 tree, htop 或 btop(若没有)，neofetch 等软件
16. 赋予 `$HOME/bin` 中的脚本操作权限

结束，总共磁盘空间占用不到 30.0 G。
