2020.6.15-2020.6.22 

# Algorithms

# Reviews
[Extra, Extra - Read All About It: Nearly All Binary Searches and Mergesorts are Broken](https://ai.googleblog.com/2006/06/extra-extra-read-all-about-it-nearly.html#:~:text=In%20Java%2C%20it%20throws%20ArrayIndexOutOfBoundsException,at%20Google%20and%20other%20places.)
[JDK-4839156 : java.util.Arrays.binarySearch does not work properly](https://bugs.java.com/bugdatabase/view_bug.do;jsessionid=136f32f18528913907cb4852eab28?bug_id=4839156)

 
#Tips
## Springboot auto restart 
[developer tools](https://docs.spring.io/spring-boot/docs/1.5.16.RELEASE/reference/html/using-boot-devtools.html)
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```
1. 加入以下依赖
2. 代码改完之后重新编译即可自动重启（mac 快捷键为 command + F9）。
3. auto restart 与 auto reload 之间的区别为 auto restart 会重新加载classpath 中改动的代码，但是auto reload 只会重新加载 static 中的静态文件。

## 301跳转与302跳转
# Share
POSIX
