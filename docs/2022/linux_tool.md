1. sudo apt install tree
2. file 可执行查看文件类型
3. ldd 查看动态库依赖 ldd main
4. /etc/passwd 查看用户和用户组的id
5. /etc/group 查看用户组
6. useradd aa 添加用户
7. id ${user} 查看用户相关信息
8. ulimit -a 可以查看当前系统的一些限制值
9. ps -aux/ajx
10. memset C语言中的系统调用，可以清空数组
11. mkfifo 创建有名管道
12. ipcs可以查看进程间通信相关信息
13. echo $$ 查看当前终端的pid
14. ps -Lf pid  查看指定进程的LWP（light weight process）轻量级进程即线程