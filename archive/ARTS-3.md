# Tips

dependencyManagement



optional.orElse



final关键字



```
import java.util.concurrent.atomic.AtomicLong;
import com.codahale.metrics.annotation.Timed;
```



Resource classes are used by multiple threads concurrently. In general, we recommend that resources be stateless/immutable, but it’s important to keep the context in mind.



Fat jar

# Share

Before we can get into the nuts-and-bolts of our Hello World application, we need to stop and think about our API. Luckily, our application needs to conform to an industry standard, [RFC 1149](http://www.ietf.org/rfc/rfc1149.txt), which specifies the following JSON representation of a Hello World saying:

[RFC 1149](http://www.ietf.org/rfc/rfc1149.txt)