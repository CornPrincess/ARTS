# Algorithm

#### [面试题62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

> 这个问题是以[弗拉维奥·约瑟夫](https://zh.wikipedia.org/wiki/弗拉維奧·約瑟夫斯)命名的，他是1世纪的一名犹太历史学家。他在自己的日记中写道，他和他的40个战友被罗马军队包围在洞中。他们讨论是自杀还是被俘，最终决定自杀，并以抽签的方式决定谁杀掉谁。约瑟夫斯和另外一个人是最后两个留下的人。约瑟夫斯说服了那个人，他们将向罗马军队投降，不再自杀。约瑟夫斯把他的存活归因于运气或天意，他不知道是哪一个。<sup>[1]</sup>

思路：

本题为约瑟夫环问题，可以有两种思路，一种时直接用单向循环链表进行模拟，另一种是根据leetcode中国的题解，使用 数学+递归（迭代）的方法，重点在于推到公式整个过程的理解。

## 解法一：模拟单向链表

```java
public int lastRemaining(int n, int m) {
        if (n == 1) {
            return 0;
        }

        ListNode head = generateLinkedList(n);
        ListNode pre = null;
        ListNode curr = head;

        while (curr.next != curr) {
            for (int i = 0; i < m - 1; i++) {
                pre = curr;
                curr = curr.next;
            }
            if (pre == null) {
                ListNode tmp = head;
                for (int j = 0; j < n - 1; j++) {
                    tmp = tmp.next;
                }
                return tmp.val;
            }
            pre.next = curr.next;
            curr.next = null;
            curr = pre.next;
            System.out.println("delete node: " + curr.val);
        }

        return curr.val;
    }

    private ListNode generateLinkedList(int n) {
        ListNode head = new ListNode(0);
        ListNode pre = head;
        for (int i = 1; i < n; i++) {
            pre.next = new ListNode(i);
            pre = pre.next;
        }
        pre.next = head;
        return head;
    }

    public class ListNode {
      int val;
      ListNode next;

      public ListNode(int val) {
          this.val = val;
      }
    
```

Time Complexity: O(n*m) 这种解法在leetcode会被判定超时

Space Complexity: O(n)



## 解法二： 数学倒推

思路：

![image-20200331002542673](/Users/zhoutianbin/Code/ARTS/assert/image-20200331002542673.png)

![image-20200331002624813](/Users/zhoutianbin/Code/ARTS/assert/image-20200331002624813.png)

![image-20200331002932099](/Users/zhoutianbin/Code/ARTS/assert/image-20200331002932099.png)

![image-20200331004011739](/Users/zhoutianbin/Code/ARTS/assert/image-20200331004011739.png)

>  图片均来自于leetcode中国网友题解<sup>[2]</sup>

```

```



# Reference

[1.约瑟夫斯问题](https://zh.wikipedia.org/zh-hans/%E7%BA%A6%E7%91%9F%E5%A4%AB%E6%96%AF%E9%97%AE%E9%A2%98)

2.[换个角度举例解决约瑟夫环](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/huan-ge-jiao-du-ju-li-jie-jue-yue-se-fu-huan-by-as/)