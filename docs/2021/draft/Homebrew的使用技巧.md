# Homebrew的使用技巧

## 安装

**一切软件的安装一定要以官方文档为准，如果官方文档看不明白再去看其他人写的博客！一般情况，网上的博客大多都是过时的内容，只会浪费时间！**

## 安装环境

macOS Big Sur

Version 11.2.2

### 配置环境变量

[官方文档](https://docs.brew.sh/Installation)

>  Git Remote Mirroring
>
> You can set `HOMEBREW_BREW_GIT_REMOTE` and/or `HOMEBREW_CORE_GIT_REMOTE` in your shell environment to use geolocalized Git mirrors to speed up Homebrew’s installation with this script and, after installation, `brew update`.

```shell
export HOMEBREW_BREW_GIT_REMOTE="..."  # put your Git mirror of Homebrew/brew here
export HOMEBREW_CORE_GIT_REMOTE="..."  # put your Git mirror of Homebrew/homebrew-core here
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

> The default Git remote will be used if the corresponding environment variable is unset.

在大陆使用brew推荐设置源，不然速度会很慢，这里推荐[清华大学的源](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)

### 执行安装脚本

在执行安装脚本时，可能会在如下命令卡住

> Downloading Command Line Tools for Xcode……

出现这种情况只需要执行 `xcode-select --install` 安装对应的工具即可，此过程可能会稍慢。配置清华的源后亲测速度在 400kb 左右，体验感已经好了很多。

## 设置代理

> ```shell
> # 手动设置
> git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
> git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
> git -C "$(brew --repo homebrew/cask-fonts)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-fonts.git
> git -C "$(brew --repo homebrew/cask-drivers)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-drivers.git
> git -C "$(brew --repo homebrew/cask-versions)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-versions.git
> ```

或者在 `.zprofile` 或 `.bash_profile` 中添加如下两行

```shell
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
```

设置源之后一定要记得执行一下命令重置 git 仓库 HEAd

```shell
brew update-reset
```

## 复原仓库上游

```shell
# brew 程序本身，Homebrew / Linuxbrew 相同
git -C "$(brew --repo)" remote set-url origin https://github.com/Homebrew/brew.git

# 以下针对 macOS 系统上的 Homebrew
BREW_TAPS="$(brew tap)"
for tap in core cask{,-fonts,-drivers,-versions}; do
    if echo "$BREW_TAPS" | grep -qE "^homebrew/${tap}\$"; then
        git -C "$(brew --repo homebrew/${tap})" remote set-url origin https://github.com/Homebrew/homebrew-${tap}.git
    fi
done

# 以下针对 Linux 系统上的 Linuxbrew
git -C "$(brew --repo homebrew/core)" remote set-url origin https://github.com/Homebrew/linuxbrew-core.git

# 重新设置 git 仓库 HEAD
brew update-reset
```



## 日常使用

```shell
brew search 
brew install
```

 

## Reference

[ 清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)

