# Tips

## git

开发工作中每天都会接触到 `git`，以及使用 `git log` 查看提交日志，在github上学习到的方法<sup>[1]</sup>>可以使日志看起来更美观

`.gitconfig` 默认的位置一般在 `$HOME/.gitconfig`，平时要编辑时我们可以直接使用 `git config <param>` 来进行编辑，也可以使用下面的命令直接打开 .gitconfig 进行编辑，非常方便。

```bash
git config --global --edit
```

比较实用的 `git log` alisa:

```bash
[alias]
    lg1 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
    lg2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
    lg = !"git lg1"

```



## homebrew

homebrew用来在mac上安装软件非常方便，但是有个头疼的问题时每次 install时都要 update homebrew， 此时我们可以输入一下指令，观察升级时的日志

```bash
 brew update --debug --verbose
```

然后我们可以输入以下命令进行升级homebrew

```bash
brew update --force
```

根据观察，几乎每次都会在 `git fetch` 这一步耗时很久，这就又回到一个老问题，在大陆如何顺畅地使用github

给github加代理

```bash
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
```

## git config local 与git config global的区别

# Share

为什么用brew install xidel就可以，但是使用之前脚本的命令就不行，而且在官网上进行编译也不行，brew的原理是什么



太受打击了，我熬夜几个小时没搞定的问题，高手来了几秒就搞定了，，，，这差距不是一般的大啊

# Reference

1.[gitconfig and alisa](https://github.com/haoel/leetcode/blob/master/.gitconfig)