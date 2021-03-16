# MacOS常用命令

##  查看MacOS系统是否64位：

```shell
uname -a
// 或者这条命令
ioreg -l -p IODeviceTree | grep "firmware-abi" | sed -e 's/[^0-9A-Z]//g'
```

