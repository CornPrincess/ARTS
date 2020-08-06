最近几年知识付费，内容付费充斥了微博以及微信，到处都是他们的身影，但这些产品的本质都是青年的精神鸦片，让大家有一种我已经在努力学习学习的假象，回过头来看其实并没有在某一个方面有实足的长进，该焦虑的还是焦虑，很多目标与理想也只停留在想想的阶段。

以上最主要的原因便是很难坚持做某一件事情，坚持地实现自己的目标，左耳听风ARTS打卡活动之前坚持做了十几周，后来便没有坚持下去，学习的过程也便跟着中断了，今天重新开始每周输出一篇ARTS的挑战，希望可以养成自己的习惯。

简单说下ARTS打卡计划，次打卡计划是由 [@陈皓](https://zhuanlan.zhihu.com/people/ed1bff9f8d1dd80f45c88aa150795078) 在知乎提出对于程序员自我技术进阶的挑战，具体可看原回答

[极客时间《左耳听风》发起的ARTS挑战怎么参加](https://www.zhihu.com/question/301150832/answer/642524181)

> 每周完成一个 ARTS： Algorithm: 每周至少做一个 LeetCode 的算法题 Review: 阅读并点评至少一篇英文技术文章 Tips: 学习至少一个技术技巧 Share: 分享一篇有观点和思考的技术文章

# Algorithm

> [leetcode 225 Implement Stack using Queues(easy)](https://leetcode.com/problems/implement-stack-using-queues/)

## 解法一（push - O(1), pop - O(n)）

思路：利用两个队列进行栈数据的存储，以及一个int变量存储top的值。q1用来存储正常的列表数据，当pop时将0 - n-1 个数暂时存储到q2，然后将q1与q2替换。

```
class MyStack {

    private Queue<Integer> q1 = new LinkedList<>();
    private Queue<Integer> q2 = new LinkedList<>();
    private int top;

    /** Initialize your data structure here. */
    public MyStack() {

    }
    
    /** Push element x onto stack. */
    // Time complexity：O(1)
    // Space complexity: O(1)
    public void push(int x) {
        q1.add(x);
        top = x;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    // Time complexity：O(n)
    // Space complexity: O(1)
    public int pop() {
        while (q1.size() > 1) {
            top = q1.remove();
            q2.add(top);
        }
        int pop = q1.remove();
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
        return pop;
    }
    
    /** Get the top element. */
    public int top() {
        return top;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

## 解法二(push - O(n), pop - O(1))

队列q1通过q2的帮助，存储栈顺序的数值。

```
class MyStack {

    private Queue<Integer> q1 = new LinkedList<>();
    private Queue<Integer> q2 = new LinkedList<>();
    private int top;

    /** Initialize your data structure here. */
    public MyStack() {

    }
    
    /** Push element x onto stack. */
    // Time complexity：O(n)
    // Space complexity: O(1)
    public void push(int x) {
        q2.add(x);
        top = x;
        while (!q1.isEmpty()) {
            q2.add(q1.remove());
        }
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    // Time complexity：O(1)
    // Space complexity: O(1)
    public int pop() {
        int pop = q1.remove();
        if (!q1.isEmpty()) {
            top = q1.peek();
        }
        return pop;
    }
    
    /** Get the top element. */
    public int top() {
        return top;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

## 解法三(push - O(n), pop - O(1))

```
class MyStack {

    private Queue<Integer> q1 = new LinkedList<>();

    /** Initialize your data structure here. */
    public MyStack() {

    }
    
    /** Push element x onto stack. */
    // Time complexity：O(n)
    // Space complexity: O(1)
    public void push(int x) {
        q1.add(x);
        int sz = q1.size();
        while (sz > 1) {
            q1.add(q1.remove());
            sz--;
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return q1.remove();
    }
    
    /** Get the top element. */
    // Time complexity：O(1)
    // Space complexity: O(1)
    public int top() {
        return q1.peek();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

## # Review

## # Tips

之前一直在mac上使用Homebrew安装各种软件，如nginx，但是最近用Homebrew安装的nvm， npm， node在zsh中都无法使用（command not found），这里总结一下Homebrew的使用以及nvm， npm，node的相关命令。



## Homebrew

> Homebrew is written in the [Ruby programming language](https://en.wikipedia.org/wiki/Ruby_programming_language) and targets the version of Ruby that comes installed with the macOS operating system. It is by default installed into `/usr/local` and consists of a [git](https://en.wikipedia.org/wiki/Git_(software)) repository, allowing the user to update Homebrew by pulling an updated repository from GitHub.<sup>[1]</sup>

Homebrew是由Ruby语言开发的，它的版本与MacOs系统中的Ruby语言版本一致，下面简单总结一下Homebrew的一些常用指令，完整的[质量查询其官网](https://docs.brew.sh/Manpage)<sup>[2]</sup>

```bash
brew help (遇到指令问题可以先用这个命令查看)
brew -v
brew search nvm
brew install nvm
brew reinstall nvm
brew uninstall nvm
brew list
```

又是因为网络原因会出现安装失败的问题，这个时候有条件的程序员可以使用代理来下载<sup>[3]</sup>：

```
$ http_proxy=http://127.0.0.1:1080 brew install foo
$ http_proxy=socks://127.0.0.1:1080 brew install foo
$ http_proxy=socks5://127.0.0.1:1080 brew install foo
```



## NVM NODE NPM

 最近MacOs系统更新到10.15.3，terminal使用zsh后出现nvm不能使用的问题，通过brew reinstall 重新安装还是不行，此时考虑到可能这个版本的Homebrew不支持，这里可以参考Best way to install and use nvm on Mac<sup>[4]</sup>对nvm进行深度清理，之后重新使用 `nvm` 官方推荐方式安装<sup>[5]</sup>

### 手动卸载

To remove `nvm` manually, execute the following:

```bash
# to remove, delete, or uninstall nvm - just remove the `$NVM_DIR` folder (usually `~/.nvm`)
$ rm -rf "$NVM_DIR"
```

Edit `~/.bashrc` (or other shell resource config) and remove the lines below:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```



### 安装

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```



### 常用命令

```bash
nvm install node # "node" is an alias for the latest version
nvm install 6.14.4 # or 10.10.0, 8.9.1, etc
nvm ls-remote
nvm use node # use the lastest version node
nvm use <version> # switch to use specific version node
nvm which <version> # get the path of executable to where it is intalled
nvm install-latest-npm # get the latest support npm version on the current node version
nvm alias default node # set the latest version node alias "default"
```

> In place of a version pointer like "0.10" or "5.0" or "4.2.1", you can use the following special default aliases with `nvm install`, `nvm use`, `nvm run`, `nvm exec`, `nvm which`, etc:
>
> - `node`: this installs the latest version of [`node`](https://nodejs.org/en/)
> - `iojs`: this installs the latest version of [`io.js`](https://iojs.org/en/)
> - `stable`: this alias is deprecated, and only truly applies to `node` `v0.12` and earlier. Currently, this is an alias for `node`.
> - `unstable`: this alias points to `node` `v0.11` - the last "unstable" node release, since post-1.0, all node versions are stable. (in SemVer, versions communicate breakage, not stability).



### npm

```
npm login
npm whoami
```



## zsh bash

MacOs设置默认命令行

```bash
chsh -s /bin/zsh(bash)
```



## Share

复习npm相关指令时，看见官网有个[nodeschool](https://nodeschool.io/)，上面的课程设计都非常好，很值得一试。

# Reference

1.[Homebrew (package management software)](https://en.wikipedia.org/wiki/Homebrew_(package_management_software))

2.[Homebrew Documentation](https://docs.brew.sh/Manpage)

3.[Homebrew with proxy](http://flummox-engineering.blogspot.com/2017/10/homebrew-with-shadowsocks-socks5-proxy-vpn-curl-server-aborted-SSL-handshake.html)

4.[Best way to install and use nvm on Mac](https://medium.com/@isaacjoe/best-way-to-install-and-use-nvm-on-mac-e3a3f6bc494d)

4.[nvm](https://github.com/nvm-sh/nvm)