# 数组

### [704. 二分查找](https://leetcode.cn/problems/binary-search/)

> 二分查找涉及的很多的边界条件，逻辑比较简单，但就是写不好。例如到底是 `while(left < right)` 还是 `while(left <= right)`，到底是`right = middle`呢，还是要`right = middle - 1`呢？
>
> 大家写二分法经常写乱，主要是因为**对区间的定义没有想清楚，区间的定义就是不变量**。要在二分查找的过程中，保持不变量，就是在while寻找中每一次边界的处理都要坚持根据区间的定义来操作，这就是**循环不变量**规则。
>
> 写二分法，区间的定义一般为两种，左闭右闭即[left, right]，或者左闭右开即[left, right)。

二刷还是三刷了, 竟然还是不能一次过, 原因是没有在循环中更新mid...

每次搜索区间都会变, 不更新mid可还行???? 不更新的话那不是妥妥的死循环吗?

### [35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

比普通的二分多了一点条件判断

### [27. 移除元素](https://leetcode.cn/problems/remove-element/)

思路一:

双指针 - 快慢指针

一个快指针, 遍历整个数组

一个慢指针, 指向下一个非排除元素即将放入的位置

> 直接秒了

其实搞清楚这两个指针的职责, 就ok了

思路二:

双指针 - 一左一右

目的是移除val, 那么左边找val, 右边找非val, 进行移除即可

最后循环结束的条件是左右相等, 此时有两种可能, 相等处为val, 或非val

### [977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

双指针, 一左一右即可, 左右主要是找出平方更大的那个, 然后填入新数组的对应位置即可

### [209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

暴力解法O(N^2)

滑动窗口: 滑动窗口和双指针很像, 也是两个指针去维护这个窗口, 只是这个窗口一向右移动的时候很像一个滑动窗口, 所以用滑动窗口来表示这种思路相比双指针更形象一些

滑动窗口的重点: 一个for循环, 那么这个索引表示窗口的起始还是终止? 这个很重要, 如果表示起始, 那么和暴力的思路是一样的, **所以滑动窗口一定是用for里的索引表示窗口的终止**, 而起始位置如何表示/维护, **如何移动滑动窗口的起始位置, 就是滑动窗口的重点所在了**

其实就是窗口右端用一个for来管理, 每次右移窗口都会变大, 只有当窗口大小满足条件时, 左端才右移, 此时窗口减小, 因为我们的目的是找出一个更小的窗口大小





好了, 现在说一个我的疑惑, 就是, 每次当滑动窗口内的数值满足条件时, 要进行while循环判断, 那么, 最终会导致滑动窗口内的数值不满足条件时才会结束, 然后滑动窗口右端右移, 那这样会有影响吗?

没有影响, 比如现在有10个元素, 窗口[0]比较大, 然后while的最后一次打破了条件, 此时右端右移, 之前考虑的是打破条件是否有影响, 起始没有, 比如如果我们让滑动窗口满足条件之后, 最后一次不打破, 右端右移, 此时, 滑动窗口大小加一, 加了一个值, 肯定更满足了, 那么左边右移, 其实有可能打破这个条件, 这时又有10个元素了, 可是不打破的话, 11一定比10大, 而我们期望找到最小的窗口大小, 所以, 右边不断右移, 左边一定要右移的, 

其实我害怕的无非是, 整体右移一个之后, 总大小变小了, 之前10个满足, 此时10个不满足了, 但是还是那句话, 我们期望的是找到更小的, 只要是10个不满足, 无所谓, 一直向右滑动即可, 明白了吗?   直到右边那个突然来了一个很大的, 让左边可以右移多次, 就找到更小的窗口了

所以其实整个的基础还是双指针, 只是用滑动窗口更形象罢了.

也就是说, 10个满足, 变9个, 不满足, 右边右移, 10个, 不满足了, 无所谓, 继续右移, 即使是11, 12, 13都不满足, 但是没事, 因为10已经记录下来了, 我们期望的是, 突然右边来了一个很大的, 然后左边右移很多, 窗口变得比10小了, 此时就有新的更小的窗口了, 明白了!!!!!

### [59. 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)

挺有意思, 维护好up down left right就好, 这个是边界, 有四个方向的for, 从左到右up++, 从上到下right--, 从右到左down--, 从下到上left++, 四个for是一个大循环, 每一次for都有一个边界变换

### [54. 螺旋矩阵](https://leetcode.cn/problems/spiral-matrix/)

妈的, 我就说之前见过哪个题 就是螺旋矩阵进行遍历吧, 果然螺旋矩阵Ⅱ我做过

这个的问题是, 我在m*n的进行螺旋遍历时, 怎么才能及时的退出呢? 很简单, **只要上>下, 左>右 就退出**

### [48. 旋转图像](https://leetcode.cn/problems/rotate-image/)

这个很简单把, 只要O(N)的空间复杂度即可, .... 只能原地旋转

1- 先按照左上到右下的对角线进行反转  2- 按照中间线进行反转

就OK了

### [240. 搜索二维矩阵 II](https://leetcode.cn/problems/search-a-2d-matrix-ii/)

关键: 从右上角看是一颗二叉搜索树

所以就有这样的性质, 每个元素的下方比它大, 左方比它小

.. 这种题, 只要做过就会了...

### [56. 合并区间](https://leetcode.cn/problems/merge-intervals/)

思路一: 可以先按照first进行排序一下, 然后再O(n)进行合并

具体每两个元素合并时可以分为三个情况, [0]相等, 可合并, [0]不相等, 可合并, [0]不相等, 不可以合并

并且i-1 和 i如果不可以合并, 则i-1和i+1....也不可能可以合并, 这也是可以这样做的关键

我好强啊~~~~

### [189. 轮转数组](https://leetcode.cn/problems/rotate-array/)

似曾相识....

1. 三次reverse即可
2. 暴力移动, O(N*K)
3. 借助额外空间, O(N), O(N)

### [238. 除自身以外数组的乘积](https://leetcode.cn/problems/product-of-array-except-self/)

本来没想到这个题怎么解

直到看到6个字 : 前缀积 & 后缀积

为什么我一开始没有想到呢?????

其实i位置的结果就是前面的积乘后面的积呀, 对吧, 为什么就想不到前缀积和后缀积呢??

### [41. 缺失的第一个正数](https://leetcode.cn/problems/first-missing-positive/)

限制: 时间O(N), 空间O(1)

如果不考虑这两个限制, 则先排序, 就很简单了  或者直接O(N)把他们放在一个set中, 也很简单

实现思路: N个数字的数组, 最多可能存储1-N, 也就是答案一定在1 ~ N+1的范围内

所以, 遍历数组, 如果当前位置该存储的元素与当前存储的元素不一致, 则把该元素交换到应当存储的位置, 且要循环进行. 然后逐个往后遍历处理

最终在遍历一遍, 找到某位置存储的元素与对应元素不一致的位置, 即可

这种题只能说, 没做过就不会, 做过了基本就会了

判断是否交换时 while 1. 该位置元素不对, 2. 该位置元素在范围之内  3. 对应位置的数字不对(如果对, 那么就死循环了), 则交换

# 链表

### [160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)

记录两个的长度, 然后走差值步, 然后同步走呗

= = 和下面这个一样

### [面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

没难度, 秒了

先求两个的长度, 然后求差值, 然后较长的先走差值步, 然后再一起走, 直到相等, 可能为空, 那就没有相交, 可能不为空, 那就相交

### [203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)

秒了, 直接搞一个哨兵节点会好做很多, 每次判断当前节点的next即可

### [707. 设计链表](https://leetcode.cn/problems/design-linked-list/)

浪费好长时间, 其实没什么问题, 主要是双向链表在初始化时, sentinel的next和prev要初始化为sentinel本身, 这样在链表为空时才好复用不为空时的头插和尾插代码

也算是对链表操作的回顾吧, 其实不难, 就那样

### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

三个指针, prev cur next往后遍历就行了

### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

依旧是搞一个哨兵节点

### [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

两个都有可能为空

搞一个哨兵结点, 然后两个cur遍历AB链表, 一个cur拼接新的链表

两个cur选出较小的, 然后拼接到新的链表上, 然后较小的cur变为next, 此时, 之前那个其实已经拼接到新链表上了, 且它之后的next也会被改变, 这是没事的, 因为它已经被遍历过了

### [2. 两数相加](https://leetcode.cn/problems/add-two-numbers/)

这B题, 根本不能把两个表示的数求出来, 然后相加, 然后再把结果搞到一个新的链表中

因为链表节点个数<=100, 100位longlong也存不下啊

ok了, 先让l1变成更长的, 然后每次都是相加, 记得加上上一位的进位, val更新为%10, 记录/10为下一位的进位

记得到l1的最后一个元素时, 可能需要再加一个新的元素到next中

其实逻辑很简单, 就是需要注意点细节了

### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

这题一看就是俩解法

1.计算总长度, 然后计算走几步可以到达第N个节点的前一个结点, 然后删除即可

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // 如果是先找总个数, 再走num - n - 1步, 找到要删除的结点的前一个
        // 就不太容易了, 因为这种仅限于不删除头结点的情况下
        // 若删除头结点, 则num=n
        // 则走-1步显然不合适, 其实就是要找出头结点的前一个
        // 所以, 如果非要采取这种方法, 设置哨兵结点是很合适的
        // 此时只需要从哨兵结点开始走nnum-n步即可找到要删除结点的前一个结点
        ListNode *sentinel = new ListNode(0, head);
        int num = 0;
        ListNode *cur = sentinel->next;
        while(cur) {
            ++num;
            cur = cur->next;
        }
        // num个
        // 走num - n - 1步, 从头结点开始
        // 从哨兵开始, 则num - n步
        num -= n;
        cur = sentinel;
        while(num--) {
            cur = cur->next;
        }
        cur->next = cur->next->next;  // 内存泄漏= =
        return sentinel->next;
    }
};
```

2.控制距离相等, 双指针

比如删除倒数第2个, 就要找到倒数第3个, 如果一共5个, 删除倒数第5个, 就要找到倒数第6个, 没有, 就设置哨兵呗

其实相比于第一种, 只是找前一个结点的方式变了

### [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)

虽然easy, 但是仍旧有一些细节需要注意

### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

- set可以去重
- 数学公式 - 不想搞
- 先求一个环形内的结点, 然后直接把该节点与next断开, 以next为头, 另一条以head为头, 转化为链表相交问题

### [234. 回文链表](https://leetcode.cn/problems/palindrome-linked-list/)

栈先进先出即可, 要判断一下链表长度是偶数还是奇数

另一种思路: 后半段链表进行逆置, 然后与前半段进行比较, 若一样, 则回文, 不一样则不回文.

### [138. 随机链表的复制](https://leetcode.cn/problems/copy-list-with-random-pointer/)

需要注意的无非就是random的处理

比如我可以记录原链表中random指向的结点到末尾的距离, 然后在新链表中也找到这样一个结点, 就可以了

思路2 : 用哈希表, 也过了

### [25. K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

第一反应是 : 如果是双向链表就好了

其次, 受排序链表中的非递归归并排序的影响, 我们可以直接算出需要进行几组反转

只用 `O(1)` 额外内存空间的算法

如果用一个vector存储就好了... 那这样其实和数组就没有区别了, 但是空间O(1)呀

....---

这不就是链表逆置嘛...    123456  654321...

----

整体思路: 若干组的链表逆置

注意点:

1. 有必要先存储好下一组的起始结点的, 虽然这一组处理完cur自动就是下一组的起始, 因为如果是最后一组之后还有不足K个结点, 则这一组的第一个需要指向下一组(不足K个)的起始
2. 其实这个题最麻烦的一个就是, 上一组的第一个, 也就是上一组逆置之后的最后一个, 需要指向下一组的逆置前的最后一个(逆置后的第一个)
   所以, 我们需要保存上一组的逆置前第一个, 然后在处理这一组的最后一个时, 让它指向这个最后一个
   并且需要创建两个, 一个bgein  一个 curBegin, 因为你不能在处理这一组的第一个时就把begin赋值了, 因为它会存储上一组的有效结点

```C++
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(k == 1) return head;
        ListNode *cur = head;
        int num = 0;
        while(cur) num++, cur = cur->next;
        num /= k;  // 进行几轮
        cur = head;
        ListNode *prevEnd = nullptr; // 上一组的最后一个
        int kNum = k;
        ListNode *ret = nullptr;
        bool first = true;
        ListNode *prev = nullptr;
        ListNode *thisFirst = nullptr;
        while(num--) {
            // 这k个进行处理
            thisFirst = cur;
            while(kNum--) {
                ListNode *next = cur->next;
                cur->next = prev;
                prev = cur;
                cur = next;
                if(first == false && kNum == 0) {
                    prevEnd->next = prev;  // 上一组的最后一个连接这一组的这个
                }
                if(first == true) {
                    ret = prev;
                }
            }
            // 此时cur是下一组的第一个, 
            first = false;
            kNum = k;
            prevEnd = thisFirst;
        }
        if(cur) {
            prevEnd->next = cur;
        }else {
            prevEnd->next = nullptr;
        }
        return ret;
    }
};
```



### [23. 合并 K 个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/)

如果是合并链表就好了,  如果是合并三个升序链表也不难

其实可以用vector<ListNode*> 存储K个首结点, 找出最小值, 然后添加到新的链表中, 可是这样肯定要超时

思路: 用小堆, 也就是优先级队列

先处理空结点, 然后把所有首结点入到小堆里面

每次找一个, 找到之后将它的next入堆(如果next不是空)

说真的, 这个优先级队列用的还是很不错的, 可以让它存储任何类型的数据

### [148. 排序链表](https://leetcode.cn/problems/sort-list/)

冒泡:

n-1趟冒泡, 第一趟: 共比较n-1次, 超时了

归并排序:

思想: 非常像二叉树的后序, 先处理左右子数组, 然后左右子树组有序了, 再处理整体

核心思想是递归, 然后二路归并, 二路归并的过程是O(N)的

缺点是空间复杂度是O(N), 也就是先左右有序, 再二路归并到新数组中, 再拷贝回去即可

对于链表, 若左右有序了, 然后合并到一个新的链表?

再拷贝回去????试试

---

我他妈归并排序, 都超时???

---

O(1)空间复杂度的归并排序

思路:  先求整体的个数, n, 然后先11归并, 再22归并, 归结为xx归并, 且每次归并时, x必须小于n, 比如10个, 最多88归并, 5个元素, 最多44归并, 且最后只能41归并

每次, 都是从左向右, 先求出两个x个数元素的起点, 但是问题是, 应该把归并后的结果放在哪里? 既然是O(1)空间复杂度, 所以就不能开辟n个元素的数组了, 或者再搞一个新的n元素的链表也不合适

我们直接搞一个虚拟哨兵节点, 然后从左至右xx归并时, 其实就是两组x个元素的链表进行合并, 2*x个, 每次选出一个, 让虚拟头结点的next指向这个, 再找出下一个, 让上一个指向这个, 也就是说, 归并时, 我们其实是在原链表进行的, 原链表的指向已经被改变了!!!!!!!
为什么数组就不能在原数组归并呢? 主要是因为链表中, 我们可以改变该元素的指向, 比如44归并, 选出某个元素之后, 找个元素就没有意义了, 我们可以改变它的指向, 因为后序的元素都存在, 但是数组中, 比如44元素归并, 某一个元素找出来, 放在这8个元素的空间的起始? 这就直接覆盖原元素了!!!

```C++
 // O(1)空间复杂度的归并
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        int n = 0;
        for(ListNode *cur = head; cur; cur = cur->next) n++;
        for(int i = 1; i < n; i *= 2) {
            // 进行ii归并
            int cnt = (n / (2 * i)) + (n % (2 * i) == 0 ? 0 : 1);  // 有cnt个ii需要归并
            ListNode *b1 = head;
            ListNode *sentinel = new ListNode(0), *cur = sentinel;
            // 虚拟头结点
            while(cnt--) {
                // b1是第一个i组的起始, 找第二个起始
                ListNode *b2 = b1;
                int num = i;
                while(num-- && b2) b2 = b2->next;  // 这是第二个起始, 这个b2是有可能不存在的, 但是b2一定存在
                int l = 0, r = 0;
                // 几种情况: 1. 两组都全 2. b2存在但是不足i个 3. b2不存在
                while(l < i && r < i && b1 && b2) {
                    if(b1->val <= b2->val) {
                        cur->next = b1;
                        cur = cur->next;
                        b1 = b1->next;
                        l++;
                    } else {
                        cur->next = b2;
                        cur = cur->next;
                        b2 = b2->next;
                        r++;
                    }
                }
                while(l < i && b1) {
                    cur->next = b1;
                    cur = cur->next;
                    b1 = b1->next;
                    l++;
                }
                while(r < i && b2) {
                    cur->next = b2;
                    cur = cur->next;
                    b2 = b2->next;
                    r++;
                }
                // 这个ii组完了, 找到下一组的开头
                // 这个仅限于当前这组是完整的, 否则当前这组就是最后一组
                b1 = b2;
            }
            cur->next = nullptr; // 不管怎样, ii归并结束, 为了避免成环, 就处理一下
            head = sentinel->next;
        }
        return head;
    }
};
```

老子终于过了, 妈的, 其实就是非递归版本的归并排序~

也算是对归并排序进行了复习了, emmmm, 其实归并并不难的, 如果是递归版本就是很像二叉树的后序遍历, 也就是先左右后根节点

非递归的话, 思路来说就是, 11归并, 22归并, 44归并, 也就是递归版是从上至下, 而非递归就是从下至上. 

具体来说非递归现在来看就是有两个方法, 一种是最初学习的那种, 每次ii归并, 把两个begin, 两个end维护好, 然后处理边界. 如果是这个链表排序这里的话, 就只维护两个begin, 具体的end, 由两个计数来处理即可, 当然还要处理两个begin为空的情况, 这其实就是说明此次的ii归并, 并不足2*i个元素

### [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)

LRU least recently used   最近最少使用, 也就是在容量有上限的情况下, 若插入了新的元素, 则需要将旧的元素移除, 此时移除的应当是最近最少使用的元素, 也就是使用频率最低的元素

而这个题就是让实现这样一个数据结构

put的要求: key value, 若key已存在, 则更新value, 若不存在则插入键值对, 若超出容量上限, 则根据LRU进行移除元素

get: 若key存在, 则返回value

这里是没有pop的, 也就是只有当容量满时, 才会自动根据LRU进行移除元素, 且put get都需要O(1)的时间复杂度

其实最主要的是怎么记录频率, 也就是得出最近最少使用的, 这样删除时才可以方便删除

---

使用链表: 且是双向循环链表, 规定, 靠近链表头部的是最近使用的, 靠近链表尾部的是最近最少使用的, 那么, put的时候, 就是链表头插, O(1), pop的时候就是链表尾删, O(1)(因为是双向的)

而get需要O(1), 又因为这里面的key是唯一的, 所以可以直接使用map, key : ListNode进行关联, 这样get key, 就可以直接找到对应的结点

且, 在put的时候, 若某key已存在, 不能只更新value, 还要将他从原链表删除, 再头插,  因为链表从头到尾的使用频率是逐渐降低的, 越到尾部越是最近最少使用

为什么队列也可以一端插入, 另一端删除呀? 为什么不能呢? 因为中间某节点的删除不是O(1)的, 线性数据结构中只有链表可以

---

ok了, 我没注意到的是: 如果get某一个key, 则这个key就会成为最近使用过的元素, 就应当将其位置调整到链表头部!!!!!

其实也是有道理的, 妈的

get: 直接map查, 有就更新一下, 返回value, 没有就返回-1

put: map查, 有就更新, 并更新value. 没有就新插入一个元素呗

上方指的更新指的是将其放置链表头部, 因为我的规定是, 链表尾部为最近最少使用的元素, 头部为最近最多使用的元素!!!

# 哈希表

### [242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)

最简单的哈希, 26个字母对应数组的每个下标, 然后哈希统计即可, key就是下标, value就是出现的次数

### [1002. 查找共用字符](https://leetcode.cn/problems/find-common-characters/)

第一思路: 统计每个字符串中26个字母的出现次数, 然后每个字母都取这些出现次数里面的最小值即可

这里可以维护n个vector, 每个vector, 26个元素, 初始化为0, 记录频率, n等于字符串的个数

最后求这n个, 里面每个字母的出现频率的最小值即可, 然后插入最小值次数个对应字母生成的string到ret中

```C++
            while(min--) ret.push_back(string(1, 'a' + i));
```

这是插入一个char组成的string的方法

### [349. 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/)

没难度, 用set / unordered_set都可以, 或者用原生数组也可以

### [第202题. 快乐数](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0202.快乐数.md#第202题-快乐数)

用set去重, 这个题的关键是, 无限循环, 那么用set就是最合适的

### [1. 两数之和](https://leetcode.cn/problems/two-sum/)

利用哈希

其实, 考虑的一个问题是, 如果有多个元素相等, 怎么办?

其实没问题的, 比如现在要找3, 且过往有多个3, 没事的, 因为我们的目标是找到一个3即可, map只存后来的3的下标

且这个题本身就说了只有一个正确答案

### [454. 四数相加 II](https://leetcode.cn/problems/4sum-ii/)

还是利用哈希, 两两一组, 思路直接就出来了

其实就是四数相加为0, 转化为两数相加为0, 两个数组组成一个数组, 一个数字在两个数组中可能不止一个频率, 比如两个数组里面的23 下标和46下标的和都是一样的, 那么就是2次一样的数

而如果剩下两个数组对应的值, 也有两次, 比如前两个数组的3出现2次, 后两个数组的-3出现2次, 那么3, -3组成的0 就一共出现4次

所以主要的哈希是: key值 : value频率

### [383. 赎金信](https://leetcode.cn/problems/ransom-note/)

没意思了, 典型的26个小写字母, 记录频率, key字母 : value频率

### [15. 三数之和](https://leetcode.cn/problems/3sum/)

二刷有点坎坷

先说思路: 三数之和等于0, 且三元组不能重复, 这里用的是双指针的思路: 先排序整个数组, 一个元素先遍历, 然后该元素右边的剩余元素为left 和 right的起始范围

外面一个for, 里面的每个a是固定的, 然后双指针开始while循环, 条件是left < right

每次循环: 如果小于0, 则应该增大, left++, 如果大于0, 则应该减小, right--

但是这里有个点很重要, 就是需要进行去重, a去重很简单, 每次for进入时即可去重, bc去重需要在while里面

如果大于0或者小于0, 此时left或right变化, 此时不需要考虑去重, 因为此时即使下一个重复, 依然会不等于0, 自动left或right移动

其实去重, 指的是最终的结果中, 相加为0的三元组不能重复, 所以只需要在相加等于0时, 进行bc的去重逻辑即可

当相加等于0, leftright都移动, 此时需要处理, 移动后bc仍不变的情况, 处理了这个情况, bc去重就处理好了

直接两个while就解决了: 先left++ right--, 然后两个while, 即可

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> ret;
        // -4 -4 -3 -2 -1 0 1 2 3 4 4 4 5 5 5
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] > 0) break;
            if(i != 0 && nums[i] == nums[i - 1]) continue;  // 去重a
            int left = i + 1;
            int right = nums.size() - 1;
            while(left < right) {
                int a = nums[i], b = nums[left], c = nums[right];
                if(a + b + c > 0) right--;
                else if(a + b + c < 0) left++;
                // 即使下一次相等, bc其中之一和之前的重复, 也没事
                else {
                    // 相加等于0, 找到了目标三元组
                    ret.push_back({a, b, c});
                    left++;
                    right--;
                    while(left < right && nums[left] == nums[left - 1]) left++;
                    while(left < right && nums[right] == nums[right + 1]) right--;
                }
            }
        }
        return ret;
    }
};
```

### [18. 四数之和](https://leetcode.cn/problems/4sum/)

是否可以借鉴上一题的经验?

先排序, 然后一个i遍历, j从i + 1开始遍历, 这是n^2了, 然后剩余元素进行双指针操作, 可以?

```C++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> ret;
        sort(nums.begin(), nums.end());
        for(int i = 0; i < nums.size(); ++i) {
            if(i != 0 && nums[i] == nums[i - 1]) continue;   // a去重
            for(int j = i + 1; j < nums.size(); ++j) {
                if(j != i + 1 && nums[j] == nums[j - 1]) continue;  // b去重
                int left = j + 1;
                int right = nums.size() - 1;
                while(left < right) {
                    int a = nums[i], b = nums[j], c = nums[left], d = nums[right];
                    if((long)a + b + c + d < target) {
                        left++;
                    } else if((long)a + b + c + d > target) {
                        right--;
                    } else {
                        // 找到了四元组
                        ret.push_back({a, b, c, d});
                        // 去重?
                        left++;
                        right--;
                        // 此时可能移动后的值依旧等于之前的值
                        while(left < right && nums[left] == nums[left - 1]) left++;
                        while(left < right && nums[right] == nums[right + 1]) right--;
                    }
                }
            }
        }
        return ret;
    }
};
```

 没错, 确实可以, 那么5数之和, 就是三个循环+双指针喽~

### [49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)

思路: 肯定要统计字符串的各个字母的个数, 然后组成一个vector<int\>, 但是, unordered_map的key可以是一个vector吗?

如果可以, 那么就很简单了, key : vector<int\> value : vector<string\>   key是对应的单词组成, value是对应所有的字符串

---

重点:

unordered_map本身并不支持vector<int\> 类型的key, 如果需要这样的key, 需要自己定义哈希函数

```C++
namespace std {
    template <>
    struct hash<std::vector<int>> {
        size_t operator()(const std::vector<int>& v) const {
            size_t hash = 0;
            for (int elem : v) {
                hash ^= std::hash<int>()(elem);
            }
            return hash;
        }
    };
}
```

在std命名空间中, 加一个这样的自定义的哈希函数即可

### [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)

这个题的解法很秀

也就是这若干个数字, 最后一定组成若干个序列, 序列数 <= 数字数

而我们可以找每一个序列的第一个元素, 若它是第一个元素, 则开始往后遍历这个序列, 求该序列的长度

做法是: 1. 先将所有元素放入set中 2. 逐个遍历, 若是某序列的首元素, 则开始计数该序列

这样一来, 即使N个元素N个序列, 也是O(N)的时间复杂度

---

哈希的体现:

1. set去重
2. 可以快速查出某个元素是否在集合中

# 字符串

### [344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

.

### [541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii/)

.

### 剑指offer替换空格

做不了

### [151. 反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string/)

思路: 处理空格, 整体reverse, 再reverse每个单词即可

> 事实证明, 刷题还是很有用的, 我这次做, 几乎每一个细节都和上一次一样, 说明留下了印象, 起到了作用

### [LCR 182. 动态口令](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

做不了, 没题

输入: s = "abcdefg", k = 2

思路: 反转整体, gfedcba 然后最后k个进行反转, 整体减最后k个, 进行反转

ok 过了

```C++
class Solution {
public:
    string dynamicPassword(string password, int target) {
        func(password, 0, password.size());
        int sub = password.size() - target;
        func(password, 0, sub);
        func(password, sub, password.size());
        return password;
    }
    void func(string &s, int begin, int end) {
        // 左闭右开
        for(int l = begin, r = end - 1; l < r; ++l, --r) {
            swap(s[l], s[r]);
        }
    }
};
```

看起来还挺美丽的

### [28. 实现 strStr()](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0028.实现strStr.md#28-实现-strstr)

?

### [459.重复的子字符串](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0459.重复的子字符串.md#459重复的子字符串)

?

### [560. 和为 K 的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)

**前缀和** + 哈希

> 前缀和: 从0下标到i下标的元素之和, 就是i下标的前缀和
>
> <img src="C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231031133642310.png" alt="image-20231031133642310" style="zoom:50%;" />
>
> 此时6下标的前缀和就是1-6个元素之和
>
> 且i下标前缀和   = i-1下标前缀和  + arr[i], 这个也是显而易见的

下面看这个题怎么用前缀和来解

假设和为K的子数组的第一个元素的下标为i, 末尾元素的下标为j, 则j下标前缀和 - i-1下标前缀和 = K

我们可以先用O(N)把整个数组的每个元素的前缀和求出, 然后O(N)遍历, 得到j位置的前缀和, K已知, 所以其实就是求, 是否有某个下标的前缀和  =  j前缀和  -  K

若有, 且对应下标 < j(因为子数组必须至少有一个元素), 则就有一个子数组为符合条件的

且注意, 符合条件的i-1可能不止一个

而如何用O(1)求出符合条件的i-1下标呢? 哈希即可, 将前缀和 : vector<int\> 用哈希组织起来 

整体复杂度为O(N)

还有一个注意点: 可能j前缀和  - K   = 0, 此时也就是求前缀和为0的子数组, 可能有子数组符合条件, 但是还要加一个空数组, 也就是0 - j的和就是K, 每一次都要注意这个情况, 可以直接m[0].push_back(-1), 表示空数组的前缀和也是0

### [76. 最小覆盖子串](https://leetcode.cn/problems/minimum-window-substring/)

解题方法: 滑动窗口, 核心思路: 我们可以找到所有覆盖目标子串的字符串(这里是极限, 也就是左右任意缩减都将不覆盖), 然后找出这些里面的最小长度即可

具体做法: 用双指针来维护这个窗口, right用于遍历, 当覆盖时, 此时可能并不是极限, 所以左端右移, 缩减到极限, 记录长度, 左端右移一个, 破坏极限, 然后右端再右移, 直到覆盖, 左端右移, 找到极限, 记录长度, 以此进行, 直到right遍历完为止

也就是每一次记录最短长度都意味着这次right元素的添加覆盖了子串, 然后left右移去寻找极限

---

这B题有大写字母, 有小写字母, 不能直接用int arr[26]

# 双指针

### [27. 移除元素](https://leetcode.cn/problems/remove-element/)

### [344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

### 剑指offer替换空格

### [151. 反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string/)

### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

### [面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

### [15. 三数之和](https://leetcode.cn/problems/3sum/)

### [18. 四数之和](https://leetcode.cn/problems/4sum/)

### [42. 接雨水](https://leetcode.cn/problems/trapping-rain-water/)

# 滑动窗口

### [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

之前做过滑动窗口的题

之前的题的核心在于, for循环要维护窗口的右端, 如果维护窗口的左端, 就一定会是更高的时间复杂度

而这个题, 直观来说, N^2完全可以解, 但是这就不是滑动窗口了

如果用for维护滑动窗口的右端

用一个set维护窗口内的当前无重复的所有字符

右端右移, 若新的元素, 不重复, 直接进入, 然后窗口扩大, 这是理所应当的

而若有重复, 则直接左端右移, 直到把当前这个重复的移除为止



用一个queue, 一个set来维护这个窗口会比较好

set用于判断新元素是否已经存在, queue用于出元素

----

有点坎坷, 逻辑问题:

- 若新元素不存在, 直接入窗口就行, 然后判断是否是更大的窗口
- 若新元素存在, 记得先不要set.insert, 因为会自动去重的. 应该先缩减窗口到没有这个新的元素, 再把新元素入窗口

### [438. 找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)

wc, 这个题不简单啊.... 莫非是我想的逻辑不太对吗

首先, set可以存储vector<int\>, ok, 比较适合用于判断当前窗口的子串是否符合条件

那么, 窗口右移, 新元素, 其实, 旧的窗口一定是没有满足条件的, 对吧

那么新的元素

1. 破坏了条件, 破坏条件一定是某个元素的数量过多了, 那么左端持续右移, 直到这个元素不过多为止

2. 没有破坏条件, 则看是否满足, 满足则ret.push_back, 然后呢?左端一个右移, 因为如果直接右端右移, 就一定会多一个元素, 那么就到了情况1, 我感觉可能也没问题
   如果不满足, 就继续呗

ok, 过了, 现在有个注意点是, 如果现在已经满足条件, 则窗口左端需要右移, 不能直接将逻辑交给下次的破坏条件上, 因为如果左端一个a, 新元素一个a, 就会进入破坏条件逻辑, 而这个整体右移一位的新的窗口本身也是符合条件的, 除非你在破坏条件逻辑中再加一个条件判断. 我的选择是不加, 也就是满足条件之后窗口左端右移!!!



---

上面两个题, 因为都是求子串的问题, 所以我都用到了队列这个结构, 一方面用vector来判断条件, 一方面用queue来记录子串, 这样其实这个queue也就是窗口, 也方便右移, 只需要pop即可, 因为队列先进先出

# 二分查找

### [35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

### [74. 搜索二维矩阵](https://leetcode.cn/problems/search-a-2d-matrix/)

两个思路: 1. 直接在二维矩阵中找   2. 把二维先搞成一维

过了. 每一行挨个二分就行

### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

常规二分然后找边界肯定是不行的

那么

比如找7, 我找6的最后一个和8的第一个, 可是这样... 不就又回去了

---

我操, 发现这个题其实和35很像

肯定是要而二分的, 可是, 怎么找左右边界?

其实左右边界的条件很清晰啊, 左i 左边小于target, i位置==target

右边界i位置 == target, 右边>target

**其实二分不仅限于找某个指定的值, 而是可以扩展为在有序数组中查找符合某个条件的值**

过了

记得找到目标值就break

### [33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

很简单啊

先找某个点, 这个点左边的值 > 这个点的值

然后两个分段内进行二分就行了

竟然过了... 怎么说呢

其实难点就在于怎么求这个点, 也就是左边的值 < 当前的值

```C++
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size(); // 左闭右开
        int pos = 0;
        while(left < right) {
            int mid = left + (right - left) / 2;
            if(mid == 0
            || (nums[mid - 1] > nums[mid])) {
                pos = mid;
                break;
            }
            else if(nums[mid] > nums.back()) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        int ret = bSearch(nums, 0, pos, target);
        if(ret != -1) return ret;
        ret = bSearch(nums, pos, nums.size(), target);
        return ret;
    }
```

1234567  有可能是这样的

5671234  有可能这样

其实, 在直接点的, 我直接判断front是否小于back不就行了, 针对第一种和第二种分开处理, 第一种情况还好处理呢

但是其实也没必要, 其实上面这个解法就直接涵盖这两种情况了

如果比back要大, 那么肯定mid在左半段中, left  = mid + 1

如果比back小, 则mid肯定在右半段中(可能不存在左半段, 无妨)   right = mid

### [153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)

上一个问题的子问题.....

### [4. 寻找两个正序数组的中位数](https://leetcode.cn/problems/median-of-two-sorted-arrays/)

O(log (m+n))

1. 中位数问题和第K大问题联系起来: 如果一共有N个, 且N为奇数, 则N/2 就是就是中位数的下标, 而它的值就是整个数组的第N/2 + 1大的元素. 若N为偶数, 则一个下标是N/2 一个是N/2 - 1, 则就是求第 N/2 + 1大的元素 以及 N/2大的元素

**所以, 现在问题就是如何求两个数组中的第K大的元素? 且是O(log m+n)的时间复杂度?**

> K 分为 K/2 和 k - k/2两部分, 比如4 就是分为22  5分为23
>
> 然后两个数组分别划分出这两个部分在数组的开端, 但是, 这两个部分的最大值不一定就是第K大的元素 
> 比如  13 5 7 9    1 11  13  如果第一个分出2个, 第二个分出3个, 则13并不是第5大的, **但是, 比较两个部分的结尾值, 较小的结尾值一定不是第K大的, 所以较小者的那部分数组都可以排除掉**, 比如可以直接排除1 3, 这两个都不可能是第5大的, 然后整体就变为了5 7 9    1 11 13找K-2大的, 也就是第3大, 再划分, 1 2两个部分   5   1 11  则5不可能是第三大, 且实际上11也不是第3大, 排除5, 找第2大, 7 9    1  11 13   此时直接比较即可

所以, 两个数组以O(log m+n)的复杂度找第K大的元素思路已经有了, 肯定要递归就很方便, 但是需要注意几个递归结束条件以及特殊情况

递归结束条件:

1. v1 为空, 或v2为空, 则O(1)求解即可
2. 此时两者都不为空, 则如果求第一大或者第二大, 则也可以O(1)求解

特殊情况考虑:

1. 如果分为n1 n2(23 56 67), 且个数较少的数组不足n1个, 则将n1调整为v1.size(), n2调整为K - v1.size(), 就ok了
2. 若分完组之后, 两部分的back()相等, 说明什么? 比如   13 5    25, 两部分, 则其实第5大, 就是这个相等的值, 直接返回, 不用递归~

---

分成n1 n2之后, 1. 两部分都足够  2. 某一个数组不足某一部分

1. 比较, 剔除, 递归

- 若    1 2 3 45    1 3 找第5大, 32分, 

# 栈与队列

### [232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/)

其实这种问题是很好思考的: 两个栈实现队列怎么实现? 栈的push, 先往一个栈里面入栈, 可是pop的时候, 要出栈低的, 无法直接出, 怎么办? 用另一个栈辅助呗: 把有元素的栈的所有元素入栈到另一个栈, 这时原本栈低的就在栈顶了

入栈只在s1入, 出栈在s2出, 直到出栈时s2的元素没有了, 就s1的重新入到s2里面进行出栈

### [225. 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/)

两个队列实现栈, 一个队列先入呗, 考虑出的时候, 要队尾的, 怎么办? 只能出队头的, 那就出到只剩一个不就行了

其实一个队列足矣, 也就是pop的时候, 把前面的n-1个元素都重新入到队尾即可喽. 两个队列就入到另一个队列中呗

### [20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)

我记得之前这个题踩过坑

过了... 很简单啊, 其实稍微需要注意的就是"((((({{{"这种情况

### [1047. 删除字符串中的所有相邻重复项](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)

easy, 典型的栈...

### [150. 逆波兰表达式求值](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)

east, 典型的栈...

### [239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

滑动窗口向右滑动, 取出滑动窗口的最大值.

单调队列: 队列首部(出口)维护的一定是当前滑动窗口内的最大值, 这样每次取出max时, 只需要获取front即可, 既然是单调队列, 则队列内部就是单调递减的

但是如何做到这个效果/目的呢?

push: 每次入队列: 如果队列尾部的元素比新元素小, 则直接弹出队列尾部的元素, 直到尾部元素 >= 新元素为止(单调队列底层使用deque实现, 并不是使用queue实现, 所以可以pop_back), 这样新元素进入时才能不破坏队列的单调性

pop: 如果要弹出的元素, 也就是滑动窗口右移之后不包含的元素, 不是front, 则说明其实要弹出的元素不是之前滑动窗口内的最大值, 自然也就不是front, 自然也就不在单调队列的内部了, 所以不用进行pop_front

(怎么理解这个呢? 为什么说要pop的元素, 也就是右移之后的元素如果不是front, 就一定不在队列内部呢? 那有没有可能在队列的后面? 不可能, 因为这个元素之后还有元素进入, 如果后面的元素大于这个元素, 则这个元素早就被弹出了, 队列内部的元素是有先后顺序的, 也就是新进先出!!!)

get_max: 获取当前滑动窗口最大值的操作直接获取front即可

每次如果新值是最小的, 直接入队列尾部即可, 因为之后窗口右移到以这个值为第一个值的时候, 它可能是最大的

### [347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)

前K个高频元素, map, 记录频率, 然后求前K个最高频的, 怎么求?其实可以排序一下呀好像, 那如果用优先级队列, 也就是堆, 好像也行

vector<pair<int, int>> 行不行? 感觉可以呀

那如果是堆呢? 求最大的K个, 则小根堆, 求最小的K个, 则大根堆

我他妈这个废物, priority_queue, 第三个参数, less大根堆, greater小根堆, 我为什么一直记不住????????????

---

1. 堆的知识: K个最大 小根堆, greater K个最小 大根堆, less
2. priority_queue没有迭代器, 不能范围for
3. 求K个, 怎么保证堆里面只有K个? 其实很简单, 一直push就行, 当size > K时pop即可, 因为是小根堆, 所以K+1个, pop一个, 一定pop最小的, 留下的就是K个最大的!!!!!!!!!
4. 大根堆的pop一定会pop最大的, 小根堆pop最小的, 这也是第一点的原因

### [215. 数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

要求时间复杂度 O(N), 其实第一时间还是会想到堆解决TopK, 但是时间复杂度好像不合格

首先先说, 第K大元素, 其实第一大就是nums[n - 1], 第K大就是nums[n - k], **所以就是求排序后nums.size() - K下标处的值**, 且是排序后的

但是使用快排等进行排序就不对了, 因为最快也是O(N * logN)

但是, 快排的思想是什么? 每一趟都是, 找出一个基准值, 这一趟之后, 左边小于它, 右边大于它, 那么, 如果基准值的下标就等于nums.size() - k, 则这个基准值处的值就是返回值, 如果不是, 则可以去左边区间 或 右边区间重复进行这样的过程

怎么写才能不创建新的数组呢? 也就是一直在一个数组中进行? 很简单, 设定left right即可

很简单, 循环里面用left right标定区间, 而每次循环结束时更新left或者right, 下次还是这个数组, 只是区间不同

快排: 单趟: 也就是递归快排核心: 右找小, 左找大, 交换, 交换

---

必须三数取中优化, 否则过不了 : 其实就是begin end mid三个地方的值, 取中间值, 让它作为枢纽值, 或者直接让他成为begin, 外面还是直接取begin

---

二刷: 三数取中需要写好

**重点: 快排的单趟排序中, left是左, right是右, 且必须是左闭右闭的!!!!!**

### [295. 数据流的中位数](https://leetcode.cn/problems/find-median-from-data-stream/)

美团二面, 字节二面, 快手, 中望一面....

---

一个大顶堆, 一个小顶堆, 大顶堆的top是最大的, 小堆的top是最小的, 比如N个, 若排序后的前N/2个, 放在大顶堆, top就是中位数的第一个, 后N/2个放在小顶堆, top就是中位数的第二个

若N为奇数, 则大堆和小堆相差一个, 多出的那一个就是中位数

如何达成这样的效果?

其实我们可以直接规定好, 若偶数, 则各取堆顶 / 2, 若奇数, 则大顶堆堆顶元素就是中位数

比如 12345, 大堆存储123, 堆顶是3, 小堆存储45, 堆顶是4

----

这样一来获取元素很方便, 但是add元素的时候需要细心一些

1. size == 0
2. size == 1
3. 若偶数, 123   567则期望最终大堆个数 - 小堆个数 = 1, 此时需要判断num 和 小堆堆顶的关系, 若<=, 直接加到大堆, 若>则处理一下
4. 若奇数, 1234 678则期望最终大堆个数 = 小堆个数, 此时判断num与大堆堆顶的关系, 若>=, 则直接加到小堆中, 若<则处理一下

其实就是期望加到哪个堆, 但是能不能直接加? 能就加, 不能就处理一下

### [155. 最小栈](https://leetcode.cn/problems/min-stack/)

8 6 4 3 1

8 6 4 3 1

1 1 3 3 4 4 7 7 0

1 1 1  1 1 1 1 1 0

easy

---

.... 为什么还是不会???

思路: stack存pair first是元素, second表示当该元素是栈顶元素, 即将pop时, 栈中的最小值

因此, push就很简单了, first固定, second只需要判断栈中已有的所有元素中的最小值和当前元素哪个小, 取较小值即可

pop很简单, top很简单, min也就依靠这个second实现了

对呀, 这个其实很简单的啊?? = == = = = = = =

### [394. 字符串解码](https://leetcode.cn/problems/decode-string/)

统计规律

- 一定要先搞一个原始的字符串, 也就是最终要返回的字符串
- 只要是一个int, 最后一定有一个[], 且中间有一个字符串, 最终要以个数倍加到前一个字符串中
- 也就是说, 并不是只要abc的a前面不是[, 我就

懂了

- 重点: 遇到数字时创建新的字符串, 而不是[a时创建, 因为可能存在3[2[abc]]

```C++
class Solution {
public:
    string decodeString(string s) {
        stack<int> int_st;
        stack<string> str_st;
        str_st.push(string());
        for(int i = 0; i < s.size(); ++i) {
            char ch = s[i];
            if(ch >= '0' && ch <= '9') {
                if(i != 0 && s[i - 1] >= '0' && s[i - 1] <= '9') {
                    // 该数字需要和前一个进行拼接
                    int_st.top() = int_st.top() * 10 + (ch - '0');
                }
                else {
                    int_st.push(ch - '0');
                    str_st.push(string());   // 这里添加新的字符串
                }
            }
            else if(ch >= 'a' && ch <= 'z'){
                // 字母
                str_st.top() += string(1, ch);
            } else if(ch == ']'){
                // 此时, 一定有一个字符串, 可能要乘以某个倍数, 可能不乘
                string s = str_st.top();
                str_st.pop();
                int num = int_st.top();
                int_st.pop();
                for(int i = 0; i < num; ++i) {
                    str_st.top() += s;
                }
            }
        }
        return str_st.top();
    }
};
```

其实还是分清楚各个情况, 怎么做, 什么时候加新的字符串

## 单调栈

### [739. 每日温度](https://leetcode.cn/problems/daily-temperatures/)

找右边第一个比它大的数字

---



<u>**单调栈: 用于求解当前元素左面或者右面第一个比他大或者第一个比他小的元素!!!!!!**</u>



---

针对这个题: 从左向右遍历, 遍历到i下标时, 并不知道它右边谁第一个比他大, 所以i下标的结果无法填入, 但是, 遍历到i时, 它可能是它左边某元素的右边第一个比它大的, 所以, 是可以填它左边的元素的结果的

单调栈: 顾名思义, 栈内的元素始终保持单调递增 / 单调递减, 对于找右边第一个大的, 就递增, 也就是当一个新元素到来时, 除非栈顶的元素>= 这个元素, 否则栈顶的元素就是小于这个新的元素的, **此时, 这个栈顶元素的右边第一个比它大的元素就是这个新元素, 因此栈顶元素就可以填结果了**

另外, 栈内是要填下标的, 而不是元素值, 否则通过元素值找下标还需要O(N)遍历

过了, 这个题逻辑过程并不难, 再缕一缕思路: 遍历到某元素时, 它左边的元素才有可能填值, 而如果左边的某些元素没有结果, 就一定在栈中, 如果你比它大, 就可以得出它的结果, 只要是它还在栈中, 就说明, 至此为止, 一直都没有比它大的出现, 而如果你满足条件, 就可以得出它的结果, 又因为这个栈是从栈顶到栈底递增的, 所以新元素可以得出所有比它小的元素的结果

![image-20231030125510511](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231030125510511.png)

左图用于找右边比它大的, 右图用于找右边比它小的

---

```C++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        stack<int> st;
        vector<int> ret(temperatures.size(), 0);
        for(int i = 0; i < temperatures.size(); ++i) {
            while(!st.empty() && temperatures[i] > temperatures[st.top()]) {
                // 栈不为空, 且栈顶元素 < 新元素
                // 栈顶元素的右边第一个比它大的找到了, 就是这个新元素
                ret[st.top()] = i - st.top();
                st.pop();
            }
            st.push(i);   // 此时要么栈为空, 要么栈顶元素 >= 新元素, 这就是单调递增栈
        }
        return ret;
    }
};
```

### [496. 下一个更大元素 I](https://leetcode.cn/problems/next-greater-element-i/)

这个题也没什么差别, 就是一个数组, 按照单调栈求值, 但是并不是所有元素的值都有用, 只有一部分有用

= =, 纯纯的单调递增栈问题, 也就是求每个元素的右边第一个比它大的元素, 不是求距离, 而是求第一个比它大的那个值, 没有区别

### [503. 下一个更大元素 II](https://leetcode.cn/problems/next-greater-element-ii/)

....没差别啊, 直接数组扩容二倍不就行了, 最后ret.resize(nums.size() / 2);

### [42. 接雨水](https://leetcode.cn/problems/trapping-rain-water/)

用单调栈的思路来解: 

其实本质上, 要想接雨水, 不仅要找出右边比它大的元素, 还要形成凹槽, 也就是左边还要有比它大的元素

这样一来, 使用单调递增栈即可实现, 比如元素 > 栈顶元素, 证明形成了凹槽的右边, 此时栈顶的下一个元素, 其实就会比栈顶元素大, 也就是形成了凹槽的左边, 这样一来就有凹槽可以接雨水了.

那如果只有凹槽的右边, 没有左边怎么办? 此时是不能接雨水的, 可以通过判断栈是否为空来判断是否有凹槽的左边

---

过了, 但是并不是完全明白, 其实基本都懂, 但是难道不需要考虑很多种情况吗?

<img src="C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231030154326953.png" alt="image-20231030154326953" style="zoom:67%;" />

比如这个, 一直小, 一直入栈, 也就是单调递增栈, 来了一个大于栈顶的, 若栈顶的下方有值, 一定比它大, 这就是凹槽, 此时接的雨水是1部分, 然后凹槽底部pop, while循环判断, 接2部分, while循环, 直到4部分完了, 因为栈只有一个, 就不能接了, 此时属于只有凹槽的右半段.

<img src="C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231030155106538.png" alt="image-20231030155106538" style="zoom: 67%;" />

如果这种情况, 其实e进栈的时候, 判断等于栈顶, 可以直接把d弹出, e进入, 这样最后算的就是1这个部分的雨水

而如果不弹出d, 也就是针对等于栈顶的情况不特殊处理, 则其实按照接雨水的规则, 此时接的雨水量为0, 因为de的高度差为0, 然后e弹出, 就轮到cdf来接1部分的雨水了, 所以这就是说, 等于栈顶的情况可以不处理



其实我总是会考虑, 如果这个凹槽的左右部分和凹槽底部不连续怎么办? 其实根本不用考虑这些

接雨水这个题要想过了, 直接用单调栈的逻辑来就行了, 找出大于的情况, 生成凹槽, 计算雨水量就完事了

记住, 用单调栈解这个题时, 是按照横向来接雨水的!!!!, 找到凹槽计算就完事了

---

双指针解法, 也就是说, 按照纵向取接雨水, 每次计算这一列可以接多少雨水, 这个逻辑是很简单的, 直接计算第i列的左右两边最高列, 然后取两者较小值, min - 第i列的高度, 就是第i列接的雨水, 因为宽度永远是1

所以, 现在问题转化为, 怎么求某一列的两端的最高列, 如果暴力就是O(n^2), 且第一列和最后一列是不接雨水的

ok, 暴力求左右最高很简单, 但是超时

如何优化?

其实第i位置的左右最高高度, 可以从i-1位置的左边最高高度求出, i位置左边最高高度 = i-1位置左边的最高高度和i-1位置的高度的较大值, 没错吧?

这样一来, O(N)求出每个位置的左右最大高度, 然后再O(N)求出结果, 不就O(N)了

```C++
class Solution {
public:
    int trap(vector<int>& height) {
        vector<int> maxLeft(height.size(), 0), maxRight(height.size(), 0);
        // 0, n-1两个位置不接雨水, 也就是两个位置不用求左右最大值, 所以
        maxLeft[0] = height[0];
        maxRight[height.size() - 1] = height.back();
        for(int i = 1; i < height.size() - 1; ++i) {
            maxLeft[i] = max(maxLeft[i - 1], height[i - 1]);
        }
        for(int i = height.size() - 2; i > 0; --i) {
            maxRight[i] = max(maxRight[i + 1], height[i + 1]);
        }
        int ret = 0;
        for(int i = 1; i < height.size() - 1; ++i) {
            int num = min(maxLeft[i], maxRight[i]);
            if(num > height[i]) ret += num - height[i];
        }
        return ret;
    }
};
```

接雨水就这?????

### [84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/)

思路:

接雨水的非单调栈解法是找左右最高的

而这个题的非单调栈解法是找左右比它低的

<img src="C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231030165732729.png" alt="image-20231030165732729" style="zoom:50%;" />

也就是, i下标的柱子, 尽量向左向右扩展, 直到有比它低的, 就不能扩展了, 如2不能扩展, 1可以一直扩展, 5可以扩展到6, 6不能, 2扩展到5623, 3不能

这样一来, 这里面的最大值, 其实就是最大的矩阵面积

暴力O(N^2), 就是左右找比它低的, 但是超时

双指针, 就是和接雨水的双指针一样, 先把左右比它低的处理好, 再O(N)求最终结果

但是, 问题是, 怎么不暴力来找出左右比它小的呢?

很简单(下方有代码), 比如 求i位置的值, 先看i-1, 若i-1不是小于i位置, 则不符合嘛, 此时i-1位置存的就是i-1处的左边第一个比i-1小的, 然后就看leftLess[i - 1]

那, 这样和暴力有什么区别呢?是有区别的, 暴力若没有遇到小的, 就挨个往左走

比如  5 6 7 8 9 10 3, 求3的时候, 效率和暴力一样, 但是    10 9 8 7 6 5 4的时候, 求4就会直接得到5下标处的-1, 也就是左边没有比它小的

或者     5   33 44  7 66 9   6    求6的时候, 就是找9, 找7, 找5, 不用遍历!!!!!

还有就是最终求结果时, 左右比它小的下标有了, 但是距离不好算, 需要细心一些~

```C++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        vector<int> leftLess(heights.size(), -1);  // 记录每一个柱子的左边第一个小于该柱子的下标
        vector<int> rightLess(heights.size(), -1);  // 记录每一个柱子的右边第一个小于该柱子的下标
        // 规定, 如果是-1, 则表示该方向没有比它小的
        int n = heights.size();
        for(int i = 1; i < n; ++i) {
            int pos = i - 1;
            while(pos >= 0 && heights[pos] >= heights[i]) pos = leftLess[pos];
            // 此时pos可能是-1, 若不是-1, 则就是左边第一个小于i处柱子的下标o
            leftLess[i] = pos;
        }
        for(int i = n - 2; i >= 0; --i) {
            // 找右边第一个小于的
            int pos = i + 1;
            while(pos >= 0 && pos < n && heights[pos] >= heights[i]) pos = rightLess[pos];
            rightLess[i] = pos;
        }
        int ret = 0;
        for(int i = 0; i < n; ++i) {
            int l = 0, r = 0;  // 左右两端可扩展的宽度
            if(leftLess[i] == -1) l = i - 0;
            else l = i - leftLess[i] - 1;
            if(rightLess[i] == -1) r = n - (i + 1);
            else r = rightLess[i] - i - 1;
            ret = max((l + r + 1) * heights[i], ret);
        }
        return ret;
    }
};
```

那, 用单调栈怎么解这个题?

其实目的还是找每个位置左右两端第一个比它小的, 这也就应对了单调栈的作用

找第一个大于的, 就是递增栈, 找第一个小于的就是递减栈

注意, 虽然是左右两端, 但是不需要进行两次, 一次即可

> 在题解42. 接雨水中我讲解了接雨水的单调栈从栈头（元素从栈头弹出）到栈底的顺序应该是从小到大的顺序。
>
> 那么因为本题是要找每个柱子左右两边第一个小于该柱子的柱子，所以从栈头（元素从栈头弹出）到栈底的顺序应该是从大到小的顺序！

单调递减栈

栈顶和栈顶的下一个元素以及要入栈的三个元素组成了我们要求最大面积的高度和宽度

```C++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        // 核心目的: 找左右两边第一个比它小的
        stack<int> st;
        heights.insert(heights.begin(), 0); // 数组头部加入元素0
        heights.push_back(0); // 数组尾部加入元素0
        st.push(0);
        int ret = 0;
        for(int i = 1; i < heights.size(); ++i) {
            // 数组头尾加了个0, 从第一个开始
            // 找左右第一个小于i的
            while(heights[i] < heights[st.top()]) {
                // st.top这里的元素找到了左右小于的
                int pos = st.top();
                st.pop();   // 这个元素处理完了
                int w = i - st.top() - 1;  // 宽度
                int h = heights[pos];
                ret = max(h * w, ret);
            }
            st.push(i);
        }
        return ret;
    }
};
```

有点晕炫= =

搞得我有点晕了, 妈的

# 二叉树

### [144. 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)

二叉树前序 - 递归就不说了,  说非递归

记住, 递归的模拟一定是用栈来模拟的

这里其实就是根处理完, 先入右再入左, 取出时就是先出左, 再出右只要左子树没遍历完, 右子树的根节点就会一直在栈底

### [145. 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)

后序: 左右中, 前序: 中左右, 所以后序非递归就是用前序的思路, 然后reverse一下即可~

### [94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

> 为了解释清楚，我说明一下 刚刚在迭代的过程中，其实我们有两个操作：
>
> 1. **处理：将元素放进result数组中**
> 2. **访问：遍历节点**
>
> 分析一下为什么刚刚写的前序遍历的代码，不能和中序遍历通用呢，因为前序遍历的顺序是中左右，先访问的元素是中间节点，要处理的元素也是中间节点，所以刚刚才能写出相对简洁的代码，**因为要访问的元素和要处理的元素顺序是一致的，都是中间节点。**
>
> 那么再看看中序遍历，中序遍历是左中右，先访问的是二叉树顶部的节点，然后一层一层向下访问，直到到达树左面的最底部，再开始处理节点（也就是在把节点的数值放进result数组中），这就造成了**处理顺序和访问顺序是不一致的。**
>
> 那么**在使用迭代法写中序遍历，就需要借用指针的遍历来帮助访问节点，栈则用来处理节点上的元素。**

中序的非递归呢?

中序: 左中右, 关键是我们处理结点的顺序和访问的顺序不一样, 前序访问到哪个, 直接处理即可, 而中序只能从根节点开始访问, 但是先处理的必须是左子树的最底部

> <u>**我就记得中序的非递归不简单来着= =, 这B东西今天做依旧不会....**</u>

![image-20231102151720104](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231102151720104.png)

怎么才能彻底记住呢...   核心思路就是: 遇到某根节点, 不能直接处理它, 而是沿着左子树一直遍历下去, 一直入栈, 最终后进先出, 最终出栈时的处理顺序才是正确的中序处理顺序

### [102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

2 : 现在再看已经了然于胸了, 很简单, 先入根, 这个就是第一层, 然后每次while(!que.empty()) 进入循环, 就看que中结点个数, 这个个数就是这一层的结点个数, 对于每个都是, 先入到这个层的vector中, 然后把非空的孩子结点入队列, 以供下次处理下一层

整体利用的就是队列的先进先出, 整体就是层序的顺序!!!

重点其实就是, 一层一层处理, 以que.size()获取这一层的节点个数, 每次while循环进入都是一层, 对应一个vector~

### [199. 二叉树的右视图](https://leetcode.cn/problems/binary-tree-right-side-view/)

层序

### [114. 二叉树展开为链表](https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/)

如果可以递归

```C++
class Solution {
public:
    TreeNode *prev = nullptr;
    void flatten(TreeNode* root) {
        if(root == nullptr) return;
        TreeNode *right = root->right;
        if(prev != nullptr) prev->left = nullptr, prev->right = root;
        prev = root;
        flatten(root->left);
        flatten(right);
    }
};
```

其实这个递归思路很简单, 都说了要前序的顺序构造, 所以就前序遍历呗, 到了前序的下一个就会改变上一个的左右结构, 比如根节点递归左之后, 其实它的左右就被改变了, 所以提前保存好右, 然后递归右, 整个处理顺序就是前序的顺序, 这个prev指针就很不错

如果不可以递归

```C++
class Solution {
public:
    void flatten(TreeNode* root) {
        while(root) {
            if(root->left) {
                TreeNode *left = root->left;
                while(left->right) {
                    left = left->right;
                }
                // 此时left为左子树的最右结点
                left->right = root->right;
                root->right = root->left;
                root->left = nullptr;
            }
            root = root->right;
        }
    }
};
```

这个有点难想到... 但是可以学习学习, 就是别忘了把左置空

### [226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

只需要遍历每个节点, 具体处理方式是swap左右孩子即可, 所以直接递归前序即可(后序, 层序都可以)

> 递归的中序不可以, 为什么呢?

### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

之前的问题是: 我可以做到判断当前根节点的左右子树的两个根节点是否符合条件, 但是我总不能递归左根节点的左右孩子 / 右根节点的左右孩子吧? 因为这根本不对啊, 我不要求左右孩子的左右孩子是符合条件的, 而是要求左孩子的右孩子与右孩子的左孩子符合条件, 哈哈, 那这样不就成了吗

2 : 实际上, 是要判断根节点的左右子树是否是对称的二叉树, 所以先判断两个子树的根节点, 然后如果两个子树要互相对称, 还要判断第一颗树的左子树与第二棵树的右子树是否互相对称, 第一棵树的右子树与第二棵树的左子树是否互相对称. 若这两对都对称, 才整体对称. 这才是整个题的递归逻辑

```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root == nullptr) return true;
        return isRight(root->left, root->right);
        // 当前根节点不为空, 判断左右子树是否是翻转的
    }
    bool isRight(TreeNode *left, TreeNode *right) {
        if((left && !right) || (right && !left)) return false;  // 不符合, 结束递归
        if(!left && !right) return true;    // 都为空, 结束递归
        if(left->val != right->val) return false;   // 不符合, 结束递归
        // 两颗子树的根节点都不为空, 且值相等
        // 要确定这两颗树互相反转, 除了这两棵树的根节点, 还要确保左子树的左子树与左子树的右子树互相反转
        // 左子树的右子树与右子树的左子树互相反转, 所以递归
        return isRight(left->left, right->right) && isRight(left->right, right->left);
    }
};
```

迭代的思想也值得学习, 利用队列的话很像层序, 但每一层并不是从左向右, 而是抽出这一层的两个节点进行判断, 并入队列这两个节点的下一层的四个(这两个不为空的情况下), 也不复杂, 其实重点还是两个节点: 左的左和右的右 右的左和左的右这一点很重要, 这也是对称的根本!

### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

> 区分深度和高度
>
> 二叉树的 **最大深度** 是指从根节点到最远叶子节点的最长路径上的节点数。   根节点
>
> 深度, 越往下越深：指从根节点到该节点的最长简单路径边的条数或者节点数  => 根节点 - 该节点  那么最大深度当然就是根节点到最远叶子节点了
>
> 高度, 越往上越高：指从该节点到叶子节点的最长简单路径边的条数或者节点数   => 该节点 - 叶子节点  (也就是下面的第一个后序解法)
>
> **而根节点的高度就是二叉树的最大深度**
>
> 前序求的就是深度，使用后序求的是高度。

前序

严格来说, 这里求的才是深度的, 也就是用max_depth记录最大的深度, 逐步向下前序递归, 遍历时处理方法很简单就是更新max_depth

而每个节点的深度用参数depth来记录, 向下递归时要+1, 回溯回来要减1

这个才是最好看的, 前序嘛

```C++
class Solution {
public:
    int max_depth = 0;
    int maxDepth(TreeNode* root) {
        func(root, 1);
        return max_depth;
    }
    void func(TreeNode *root, int depth) {
        if(root == nullptr) return;
        // depth表示该结点的深度
        if(depth > max_depth) max_depth = depth;
        // 前序, 根节点处理完了, 遍历左右子树
        func(root->left, depth + 1);
        func(root->right, depth + 1);
    }
};
```

下面这个写的真的丑陋

```C++
class Solution {
public:
    int max_depth;
    int maxDepth(TreeNode* root) {
        max_depth = 0;
        if(root == nullptr) return max_depth;
        func(root, 1);
        return max_depth;
    }
    void func(TreeNode *root, int depth) {
        // 比如第一次进入, 是根节点, 深度为1, 没毛病, 且不为空
        if(depth > max_depth) max_depth = depth;
        if(!root->left && !root->right)  return;  // 终止递归
        if(root->left) {
            depth++;  // 深度+1, 进入下一层
            func(root->left, depth);
            depth--;  // 回溯, 深度减1
        }
        if(root->right) {
            depth++;  // 深度+1, 进入下一层
            func(root->right, depth);
            depth--;  // 回溯, 深度-1
        }
        return;
    }
};
```

这是后序, 求的是高度

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root) return 0;
        int leftDepth = maxDepth(root->left);
        int rightDepth = maxDepth(root->right);
        return 1 + max(leftDepth, rightDepth);
        // 这里本质是后序, 也就是左右中, 而对中的操作其实就是结合左右的结果加一个1
    }
};
```

空结点返回0嘛, 叶子节点的高度: 距离叶子节点的节点个数, 其实就是1, 所以就返回1, 而根节点求的是左右孩子的高度中更高的那个, 加上自己, 其实就是自己到最远的那个叶子节点的距离, 也就是高度. 而根节点的最大高度就是整棵树的最大深度喽

层序

当然用层序也可以, 每经过一层depth++

> 后序是高度, 也就是从叶子节点到该节点的, 上面 高
>
> 前序是深度, 是从顶部开始计000.2算的, 从上往下, 也就是从根节点向下, 下面 深

### [111. 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)

这个当然可以按照层序的思想, 每一层遍历, 当某一层第一次出现左右孩子为空时, 直接返回这一层的层数即可, 这也就是遍历到这个节点所经过的最小深度~

但是我采用了递归的方式, 这里需要注意的是若左右孩子只有一个不为空时, 不能直接返回1 + min(min(minDepth(root->left), minDepth(root->right));) 因为为空的一方会直接返回0, 这样就大错特错了, 0一定比另一方小的, 且你某一孩子为空, 你还递归它干嘛, 这一定不符合条件啊, 所以只能递归不为空的那一方, 每一次返回都加一个1, 这样每经过一个节点都会加一个1, 最终也就是最小深度了

可以看出：**求二叉树的最小深度和求二叉树的最大深度的差别主要在于处理左右孩子不为空的逻辑。**

这里也是后序的思想, 也就是高度, 只是最小深度其实就是最小高度

```C++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == nullptr) return 0;
        int leftDepth = minDepth(root->left); // 左边深度, 可能为0, 也就是没有意义
        int rightDepth = minDepth(root->right); // 右边深度
        // 这里是为了体现出后序, 实际上这两个可能不使用, 也就是为空, 没意义
        if(root->left && root->right) {
            return 1 + min(leftDepth, rightDepth);
        }
        if(root->left) {
            return 1 + leftDepth;
        }
        else if(root->right) {
            return 1 + rightDepth;
        }
        return 1;
    }
};
```

其实逻辑就是 每经过一个节点加一个1, 但是需要注意的就是若左为空, 返回1 + 右递归

前序:

前序本质上才是深度, 也就是从根节点开始, 这里求的就是最小深度

```C++
class Solution {
public:
    int min_depth;
    int minDepth(TreeNode* root) {
        min_depth = INT_MAX;
        if(root == nullptr) return 0;
        func(root, 1);
        return min_depth;
    }
    void func(TreeNode *root, int depth) {
        // depth是当前深度
        if(root == nullptr) return;
        if(!root->left && !root->right) {
            // 叶子节点
            if(depth < min_depth) min_depth = depth;
        }
        // 有孩子
        func(root->left, depth+1);
        func(root->right, depth+1);
        // 这里可以不考虑直接递归, 是因为如果是空不做任何事就会返回
        // 但如果想减少递归次数, 则可以判断一下
    }
};
```

真的太清楚了, 明朗了很多

其实目的还是找一个叶子节点, 用min_depth记录就很方便, 前序就是先处理: 先判断嘛, 叶子节点就尝试更新

然后递归, 这里不用判断(可以判断)是否为空, 因为递归进入也不会更新为0或者不恰当的值!!!!!

### [222. 完全二叉树的节点个数](https://leetcode.cn/problems/count-complete-tree-nodes/)

这题就别想着递归遍历了, 时间复杂度不符合, 要利用完全二叉树的性质!

完全二叉树要么是满二叉树要么不是满二叉树

先判断这颗子树是不是满, 如果是, 则直接用公式求这颗子树的节点个数

若不是, 则返回1 + 递归左 + 递归右

每一次递归都是这样, 若满, 则直接求, 不满则递归, 最终当只有一个节点时, 就会符合满二叉树的性质~

满二叉树  n = 2^(depth) - 1

> 求深度可以从上到下去查 所以需要前序遍历（中左右），而高度只能从下到上去查，所以只能后序遍历（左右中）

### [257. 二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/)

> 新的感悟: 前序是从上到下的遍历, 而后序大体是从下到上的, 所以, 像这种题注定是要用前序的, 因为字符串要从上到下遍历的时候累加, 到了叶子节点或者空结点终止遍历

<img src="C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231008160007870.png" alt="image-20231008160007870" style="zoom:50%;" />

**回溯和递归是一一对应的，有一个递归，就要有一个回溯**

这是我自己写的, 其实很好理解, 也很精简, 那你说这里面有回溯嘛? 其实是有的, 但是隐藏了(看不懂就继续往下看)

```C++
class Solution {
public:
    vector<string> v;
    vector<string> binaryTreePaths(TreeNode* root) {
        func(root, "");
        return v;
    }
    void func(TreeNode *root, string s) {
        if(root == nullptr) return;    // 空结点直接return终止循环
        if(!root->left && !root->right) {
            // 叶子节点也要return终止循环
            s += to_string(root->val);
            v.push_back(s);
            return;
        }
        s += to_string(root->val);
        s += "->";
        func(root->left, s);   // 中左右, 前序递归
        func(root->right, s);
        // 这里不用判断return, 因为函数的开头就判断了
        // 当然判断一下也行, 这样函数第一行就可以去掉了
    }
};
```

```C++
class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<int> v;
        vector<string> result;
        func(root, v, result);
        return result;
    }
    void func(TreeNode *root, vector<int> &v, vector<string> &result) {
        // 可以确保root不为空
        v.push_back(root->val);
        if(!root->left && !root->right) {
            // 叶子节点, 终止递归
            // 12345
            string s;
            for(auto & i : v) {
                s += to_string(i);
                s += "->";
            }
            s.pop_back();
            s.pop_back();
            result.push_back(s);
        }
        // 非叶子节点, 有孩子
        if(root->left) {
            func(root->left, v, result);
            v.pop_back();  // 回溯的直接体现
        }
        if(root->right) {
            func(root->right, v, result);
            v.pop_back();  // 回溯的直接体现
        }
    }
};
```

比如有左右孩子的情况下, v中入了我自己这个节点, 很正常, 然后递归, 进入左这个节点的递归函数中, 左入了自己, 如果左是叶子, 则终止递归, 返回到上层, 此时v中是多了一个左节点的, 因为这里用的是vector\<int> &, 引用使得左孩子的递归中对v的改变影响了父节点这里, 所以它需要pop_back把左孩子去掉, 才能正确进入右孩子

可是难道我就不怕左孩子还有左孩子嘛? 这样左子树完了之后, 会不影响右孩子嘛? 

没事的, 因为左孩子的递归里面也会进行pop_back, 这样一个进入, 一个回溯, 是没问题的

就比如最上面这个图, 10的回溯只pop_back一次, 但是其实下面的每次递归都有一次回溯所以, 完全可以认为1只递归了一次, 10回溯一次即可

而我自己写的那里, s是值拷贝, 递归内部的修改不影响外部, 所以其实也回溯了, 但是没有需要做的回溯操作罢了

[leetcode-master/problems/0257.二叉树的所有路径.md at master · youngyangyang04/leetcode-master (github.com)](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0257.二叉树的所有路径.md)

写的真不错呀

### [404. 左叶子之和](https://leetcode.cn/problems/sum-of-left-leaves/)

没难度, 前序即可

> 这道题目要求左叶子之和，其实是比较绕的，因为不能判断本节点是不是左叶子节点。
>
> 此时就要通过节点的父节点来判断其左孩子是不是左叶子了。
>
> **平时我们解二叉树的题目时，已经习惯了通过节点的左右孩子判断本节点的属性，而本题我们要通过节点的父节点判断本节点的属性。**
>
> 希望通过这道题目，可以扩展大家对二叉树的解题思路。

### [513. 找树左下角的值](https://leetcode.cn/problems/find-bottom-left-tree-value/)

第一反应: 层序可以= =, 最后一层的第一个即可

递归:

目的: 找出最后一层(深度最深)的第一个节点

深度最深很简单, 直接维护一个全局的max_depth即可, 可是第一个怎么办? 如何防止右边的不重复更新, 其实也很简单, 只需要当深度大于max_depth时再更新就好了, 这样右边的就不会更新了~

两个版本, 一个详细回溯版, 一个简略版

核心就是一个前序即可, 之前就说过了前序求深度最合适

### [112. 路径总和](https://leetcode.cn/problems/path-sum/)

前序

先判个空

终止条件: 1. 自己是叶子 2. 值 == target

否则(没有满足条件), 则递归左右子树呗, 没啥难的

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        return func(root, 0, targetSum);
    }
    bool func(TreeNode *root, int sum, int targetSum) {
        if(root == nullptr) return false;
        sum += root->val;
        if(!root->left && !root->right && sum == targetSum) return true;
        // 继续递归
        bool b1 = func(root->left, sum, targetSum);
        bool b2 = func(root->right, sum, targetSum);
        return b1 || b2;
    }
};
```

### [437. 路径总和 III](https://leetcode.cn/problems/path-sum-iii/)

挺有意思

前序遍历, 比如根节点到某节点的路径为 12345  则vector记录 1+2+3+4 2+3+4 3+4 4, 到了5这里, 其实它可以组成的路径之和一共有5中可能, 它自己, 或者与前面的4总和, 与4与3, 与4与3与2, 与4与3与2与1, 判断这5种有几种 == target, 即可

也就是从根结点到某结点若一共有x个结点, 则包含该结点的路径总和共有x种可能, 用vector记录即可

### [105. 从前序与中序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

题目类型: 根据数组, 构造二叉树

根据前序第一个获取根节点, 然后划分中序序列为左右两个数组, 再根据中序的左右两个数组, 获取到前序的左右子树数组, 再递归呗

前序数组: 根节点, 左子树区间, 右子树区间

中序数组: 左子树区间, 根节点, 右子树区间

### [106. 从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

![image-20231008205858998](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231008205858998.png)

关键是搞清楚, 后序最后一个是根, 根在中序的左和右分别就是左子树对应的数组, 和右子树对应的数组, 而后序的前面一部分就是左子树, 后面一部分就是右子树, 且中序左数组和后序左数组大小相等, 对应的就是左子树, 中序的右数组和后序的右数组对应右子树, 完全可以递归处理, 因为本来这个函数的作用就是通过一个树的中序和后序数组构建一棵树!!!!!!!!

而当中序左或右数组分割成空, 后序的对应数组也会是空, 此时直接就会返回nullptr

如果只有一个, 则中序和后序的左右数组都是空, 也会进一步返回空的~

所以核心就是分割数组!!!!!!



> 其实还是递归的思路, 首先我可以把根节点构造出来, 那么这个函数的参数就是两个数组, 我再把左右子树的数组找出来, 就可以递归构建了

### [654. 最大二叉树](https://leetcode.cn/problems/maximum-binary-tree/)

输入是一个数组, 那么, 找到根之后构建根节点, 递归的思路很显然就可以想到, 找出左右子树的数组就可以递归了

最终的叶子节点的左右子树的数组为空, 这其实也是递归的终止条件嘛, 返回nullptr即可

每次递归都是 : 构建根节点, 递归左右子树, 就是这样的

说实话没啥难度, 只是可以再稍微优化一下, 不用构造新的数组, 直接在原数组中处理

> **注意类似用数组构造二叉树的题目，每次分隔尽量不要定义新的数组，而是通过下标索引直接在原数组上操作，这样可以节约时间和空间上的开销。**
>
> 一些同学也会疑惑，什么时候递归函数前面加if，什么时候不加if，这个问题我在最后也给出了解释。
>
> 其实就是不同代码风格的实现，**一般情况来说：如果让空节点（空指针）进入递归，就不加if，如果不让空节点进入递归，就加if限制一下， 终止条件也会相应的调整。**

### [617. 合并二叉树](https://leetcode.cn/problems/merge-two-binary-trees/)

如果一方为空, 一方不为空, 是直接返回这个不为空的, 还是自己再复制一个新的这个不为空的

如果后者, 就是完全构造一个新的二叉树出来~ 我都写了

### [700. 二叉搜索树中的搜索](https://leetcode.cn/problems/search-in-a-binary-search-tree/)

对于一般二叉树，递归过程中还有回溯的过程，例如走一个左方向的分支走到头了，那么要调头，在走右分支。

而**对于二叉搜索树，不需要回溯的过程，因为节点的有序性就帮我们确定了搜索的方向。**

例如要搜索元素为3的节点，**我们不需要搜索其他节点，也不需要做回溯，查找的路径已经规划好了。**

中间节点如果大于3就向左走，如果小于3就向右走



二叉搜索树的迭代不需要栈和队列, 因为二叉搜索树的搜索路径是确定的, 因为它本身的性质, 所以直接一路往下走即可

### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

```C++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        if(root == nullptr) return true;  // 终止
        if((root->left != nullptr && root->left->val >= root->val)
        || (root->right != nullptr && root->right->val <= root->val)) return false;  // 遍历操作
        bool b1 = isValidBST(root->left);
        bool b2 = isValidBST(root->right);
        return b1 && b2;
    }
};
```

大错特错, 典中典的错误, 因为你不能通过每个节点的左右孩子符合就判断出整棵树符合, 因为完全可能右孩子大于自己, 但是右孩子的左孩子不大于自己, 且小于右孩子, 这样就典型的错误了.

<img src="C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231009120557100.png" alt="image-20231009120557100" style="zoom:50%;" />

正确解法: 利用搜索树的中序有序

```C++
class Solution {
public:
    TreeNode *pre = nullptr;
    bool isValidBST(TreeNode* root) {
        if(root == nullptr) return true;
        bool b1 = isValidBST(root->left);
        if(pre != nullptr && root->val <= pre->val) return false;
        // 当前节点大于中序上一个, 则更新, 不管是第一个还是不是第一个都需要更新的
        pre = root;
        bool b2 = isValidBST(root->right);
        return b1 && b2;
    }
};
```

中序遍历, 记录上一个中序的非空节点, 判断当前节点是否>中序上一个, 若有一个不符合则错误, 若都符合则正确

2 : 对于每一棵子树, 一个根节点, 都是需要处理左, 自己, 右之后, 再将整体结果返回, 如果有任何一个不是升序, 也就是不满足搜索树的性质, 就最终会返回false, 这个是没问题的, 比如根节点来说, 左子树整体满足, 且根节点满足大于左子树的那个结点(中序的前一个), 且右子树整体满足, 且右子树的中序下一个大于根节点, 那么最终就会返回true

### [230. 二叉搜索树中第K小的元素](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/)

中序即可啦

![image-20231102183818106](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231102183818106.png)

可以看出, 哈哈, 左边是很久之前写的, 比较...原始

右边, 其实ret只会更新一次, 根节点最终中序遍历完一定会返回正确的ret, 其他的可能返回0, 可能返回正确的ret, 都无所谓

---

优化: 若自己就是第k个, 直接返回, 不用递归右子树

若左子树完了, 已经过了第k个, 直接返回, 不用递归右子树

### [530. 二叉搜索树的最小绝对差](https://leetcode.cn/problems/minimum-absolute-difference-in-bst/)

题目中要求在二叉搜索树上任意两节点的差的绝对值的最小值。

**注意是二叉搜索树**，二叉搜索树可是有序的。

遇到在二叉搜索树上求什么最值啊，差值之类的，就把它想成在一个有序数组上求最值，求差值，这样就简单多了。

**遇到在二叉搜索树上求什么最值，求差值之类的，都要思考一下二叉搜索树可是有序的，要利用好这一特点。**

同时要学会在递归遍历的过程中如何记录前后两个指针，这也是一个小技巧，学会了还是很受用的。

### [501. 二叉搜索树中的众数](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)

思路1 : 维护一个哈希表, 记录频率, 记录最大频率 但是需要额外空间

思路2: 中序有序

### [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)

遇到这个题目首先想的是要是能自底向上查找就好了，这样就可以找到公共祖先了。

那么二叉树如何可以自底向上查找呢？

回溯啊，二叉树回溯的过程就是从低到上。

后序遍历（左右中）就是天然的回溯过程，可以根据左右子树的返回值，来处理中节点的逻辑。

判断逻辑是 如果递归遍历遇到q，就将q返回，遇到p 就将p返回，那么如果 左右子树的返回值都不为空，说明此时的中节点，一定是q 和p 的最近祖先。

---

一个点很重要: 就是最近公共祖先的左子树(包括自己)有p/q 而右子树(包括自己)有q/p, 这是一定的,  且只有一个这样的节点存在, 但凡不是最近公共祖先, 都不会满足这个条件!!!!

下面这个是自己写的

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == nullptr) return nullptr;
        if((root == p && hasNode(root, q))
        || (root == q && hasNode(root, p))) {
            return root;
        }
        else if((hasNode(root->left, p) && hasNode(root->right, q))
        || (hasNode(root->left, q) && hasNode(root->right, p))) {
            return root;
        }
        // 该节点不是最近公共祖先
        TreeNode *r1 = lowestCommonAncestor(root->left, p, q);
        if(r1 != nullptr) return r1;
        TreeNode *r2 = lowestCommonAncestor(root->right, p, q);
        return r2;
    }
    bool hasNode(TreeNode *root, TreeNode *target) {
        // 判断root这颗树中是否有target
        if(root == nullptr) return false;
        if(root == target) return true;
        // 根节点不是
        // 前序
        bool b1 = hasNode(root->left, target);
        bool b2 = hasNode(root->right, target);
        return b1 || b2;
    }
};
```

这个是比较好理解的, 前序遍历每个, 对每个都进行判断, 时间复杂度可能会很高

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // 后序回溯法
        // 要么到了空结点, 要么自己就是目标节点
        if(root == nullptr || root == p || root == q) return root;
        // 没空, 且自己不是目标节点
        TreeNode *left = lowestCommonAncestor(root->left, p, q);
        TreeNode *right = lowestCommonAncestor(root->right, p, q);
        // 左找到了一个, 右找到了一个(不会重复), 则自己就是最近公共祖先
        if(left && right) return root;    
        // 左没找到, 右找到了, 返回右
        else if(!left && right) return right;
        // 反之亦然
        else if(left && !right) return left;
        // 左右都没找到, 返回空
        else return nullptr;
    }
};
```

这里是后序回溯法,  因为后序的回溯本身就是从下往上进行处理, 根据左右子树的返回情况, 来最终确定自己的返回值



具体来说

2 : 其实这个逻辑好好想一想 很简单

1. 先看自己是不是pq之一, 如果是, 直接返回自己
   当然可能自己就是最近公共祖先(另一方在自己的左右子树之中), 或者自己不是 都无所谓

以下情况基于自己不是pq之一, 肯定就要后序了, 根据左右子树返回值

2. 如果左右返回都不为空, 则自己就是最近公共祖先, 返回自己(那么, 自己的上方一系列其实就会返回自己)
3. 左右一方为空, 一方不为空, 则返回这个不为空的
   此返回情况可能是情况2演变而来的, 可能是情况1演变而来的
4. 双方都为空, 则直接返回nullptr, 说明自己这颗子树里面没有p以及q

其实这个每种情况之间都是有联系的, 总之, 最终根节点返回的一定是这个最近公共祖先, 这个过程想一想还挺有意思

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == nullptr) return nullptr;
        TreeNode *ret1 = lowestCommonAncestor(root->left, p, q);
        TreeNode *ret2 = lowestCommonAncestor(root->right, p, q);
        if(root == p || root == q) return root;
        else if(ret1 && ret2) return root;
        else if(ret1) return ret1;
        else if(ret2) return ret2;
        else return nullptr;
    }
};
```

---

这个还有一个思路: 就是, 直接求出pq的从根节点到它的路径, 存在一个vector里面, 然后相当于解决链表相交的问题

### [235. 二叉搜索树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/)

从根节点往下走的第一个符合中间值的节点一定是最近公共祖先

这个道理很简单啊, 为什么我最开始没有想到呢?

且根本不需要遍历左右子树, 因为可以判断往哪边走!

1. 自己最开始想到的, 其实没啥问题, 从上往下嘛, 第一个就是最近公共祖先, 但是问题是我没有意识到可能存在相等的情况哈哈
   其次是我没有利用二叉搜索树的性质简化递归过程

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == nullptr) return nullptr;
        if((root->val >= p->val && root->val <= q->val)
        || (root->val <= p->val && root->val >= q->val)) {
            return root;
        }
        auto ret = lowestCommonAncestor(root->left, p, q);
        if(ret) return ret;
        ret = lowestCommonAncestor(root->right, p, q);
        return ret;
    }
};
```

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == nullptr) return nullptr;
        if((root->val >= p->val && root->val <= q->val)
        || (root->val <= p->val && root->val >= q->val)) {
            return root;
        }
        if(root->val < p->val && root->val < q->val)
            return lowestCommonAncestor(root->right, p, q);
        if(root->val > p->val && root->val > q->val)
            return lowestCommonAncestor(root->left, p, q);
        return nullptr;  // bukeneng
    }
};
```

2. 迭代

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // 迭代法
        while(true) {
            if((root->val >= p->val && root->val <= q->val)
            || (root->val <= p->val && root->val >= q->val)) {
                return root;
            }  // 此时一定是最高的, 也就是最近的公共祖先
            // 比这个低的也可能符合条件, 但完全可能不是公共祖先
            if(root->val < p->val && root->val < q->val) {
                root = root->right;
            }
            if(root->val > p->val && root->val > q->val) {
                root = root->left;
            }
        }
    }
};
```

所以, 几乎搜索树的很多问题都可以利用搜索树的性质来决定下次去左子树还是右子树, 不需要像普通二叉树那样

> 对于二叉搜索树的最近祖先问题，其实要比[普通二叉树公共祖先问题](https://programmercarl.com/0236.二叉树的最近公共祖先.html)简单的多。
>
> 不用使用回溯，二叉搜索树自带方向性，可以方便的从上向下查找目标区间，遇到目标区间内的节点，直接返回。
>
> 最后给出了对应的迭代法，二叉搜索树的迭代法甚至比递归更容易理解，也是因为其有序性（自带方向性），按照目标区间找就行了。

### [124. 二叉树中的最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/)

> 虽然是困难, 但是真有思路...

后序, 回溯, 先左右再根据左右的结果处理根结点

每个结点都检查一下经过自己的最大路径和是否可以刷新存储的全局最大路径和, 那么最终的最大路径和总得经过一个结点吧吧?

每个结点经过自己的最大路径和有几种可能

1. 单独自己
2. 经过左孩子的最大路径和 + 自己(加上左子树的返回值)
3. 经过右孩子的最大路径和 + 自己(加上右子树的返回值)
4. 左右最大路径和 + 自己

而每个结点的都返回给父节点 : 经过自己的最大路径和, 但是要排除上方的情况4(原因略了), 所以就是返回123的最大值给父节点

其实逻辑很简单, 整棵树的最大路径和总得有一个结点吧? 那么必定所有结点都进行如上处理之后一定会包含最终答案

而整体其实就是后序遍历回溯罢了

这个题要开long long

```C++
class Solution {
public:
    long long ret = INT_MIN;
    int maxPathSum(TreeNode* root) {
        func(root);
        return ret;
    }
    long long func(TreeNode *root) {
        if(root == nullptr) return 0;
        long long left = func(root->left);
        long long right = func(root->right);
        int num1 = root->val, num2 = root->val + left, num3 = root->val + right,
            num4 = root->val + left + right;
        if(num1 > ret) ret = num1;
        if(num2 > ret) ret = num2;
        if(num3 > ret) ret = num3;
        if(num4 > ret) ret = num4;
        return num1 > (num2 > num3 ? num2 : num3) ? num1 : (num2 > num3 ? num2 : num3);
    }
};
```

### [701. 二叉搜索树中的插入操作](https://leetcode.cn/problems/insert-into-a-binary-search-tree/)

这完全就是搜索树的插入啊, 我之前实现过的, 但是竟然第一时间不会了= =

稍微想了一下, 就ok了, 其实我之前的问题是 , 这个点可以在很多地方, 但是方便起见, 直到找到一个目标位置为空的, 即可很方便的插入

迭代递归都有, 不难....

```C++
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == nullptr) return new TreeNode(val);
        insert(root, val);
        return root;
    }
    void insert(TreeNode *cur, int val) {
        if(val > cur->val && cur->right == nullptr) {
            cur->right = new TreeNode(val);
            return;
        } else if(val < cur->val && cur->left == nullptr) {
            cur->left = new TreeNode(val);
            return;
        }
        if(val > cur->val) insert(cur->right, val);
        else insert(cur->left, val);
    }
};
```

上面是自己写的

下面是另一种写法, 其实不如我自己写的好理解

```C++
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == nullptr) {
            return new TreeNode(val);
        }
        if(val > root->val) root->right = insertIntoBST(root->right, val);
        else root->left = insertIntoBST(root->left, val);
        return root;
    }
};
```

下面是双指针的迭代法, 其实也是我记得搜索树中最初实现的insert的写法

但是我感觉不如我最开始写的迭代法好理解, 因为这里需要维护cur 和 parent

```C++
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == nullptr) return new TreeNode(val);
        TreeNode *cur = root;
        TreeNode *parent = nullptr;
        while(cur) {
            parent = cur;
            if(val > cur->val) cur = cur->right;
            else cur = cur->left;
        }
        if(val > parent->val) parent->right = new TreeNode(val);
        else parent->left = new TreeNode(val);
        return root;
    }
};
```

### [450. 删除二叉搜索树中的节点](https://leetcode.cn/problems/delete-node-in-a-bst/)

两种, 一种迭代删除, 也是最原始的

一种carl的递归法

其实各有各的优势吧

第一种迭代必须得记录父节点, 并且还要区分要删除的是不是根节点

而递归法不需要记录父节点, 递归到要删除的节点时, 直接把当前这个root删掉, 然后返回应该返回的, 而具体返回什么就要看root的孩子的情况了~

### [669. 修剪二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree/)

思路:

肯定要先判断根节点嘛, 如果根节点不符合, 肯定也就有某个子树不符合了(搜索树的性质), 但是此时另一边是不能确定的

而如果根节点符合, 那此时也只有根节点符合, 左右子树是不确定的, 所以左右子树还需要递归处理

其实就是这样的

要想理解这个其实可以模拟一下过程, 若所有节点都是范围内的, 则每次递归除了空结点, 都是递归左右子树, 而最终叶子节点的左右子树递归返回nullptr, 其他节点返回自己给父节点, 父节点的左右递归没有改变

而如果根符合, 此时递归左, 可能左孩子不符合, 但是左孩子的右孩子符合, 此时, 左孩子递归, 发现自己不符合, 且小于low, 直接递归右, 最终肯定返回右, 假设右是一个符合的叶子节点, 右孩子再递归两次, 就返回自己, 而左孩子返回给父节点的就是递归完成的右孩子

把这两个过程一想就清楚很多了

### [108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)

2 : 思路还是递归, 我记得, **<u>很多根据数组来构造二叉树的题, 其实思路都一样, 先找出数组的中间值, 构造出根节点, 然后以中间值划分整个数组, 为两半, 递归处理</u>, 左半数组构造左子树, 右半数组构造右子树, 而递归的终止条件就是, 当数组为空, 返回nullptr, 也就是空结点, 而数组只有一个元素, 就直接构造一个结点返回**, 而我们可以搞一个新的函数, 比如func(vector<int\> v, int begin, int end); 这样整体都是一个数组来使用, 只是划分好起始和终止区间, 也可以用一个vector<int\> v的参数的函数, 因为取左右数组的时候, 直接可以构造出一个新的数组, 然后递归这个函数就ok

12 就是左一个孩子, 123就是左右都有一个, 1234就是左高度为2 右高度为1, 

12345 就是根节点的左右子树的高度为2, 且左右子树的左右高度差为1, 整体为0

1234567 就是深度为三的满二叉树= =

```C++
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if(nums.size() == 0) return nullptr;
        if(nums.size() == 1) return new TreeNode(nums[0]);
        // 只有nums.size() >= 2时, 这个数组才需要递归处理
        // 先找根节点, 若整体为奇数, 正好, 左右个数相等, 若偶数, 则左右个数差1
        int mid = nums.size() / 2;
        TreeNode *root = new TreeNode(nums[mid]);
        vector<int> v1(nums.begin(), nums.begin() + mid);
        vector<int> v2(nums.begin() + mid + 1, nums.end());
        root->left = sortedArrayToBST(v1);
        root->right = sortedArrayToBST(v2);
        return root;
    }
};
```

> 首先取数组中间元素的位置，不难写出`int mid = (left + right) / 2;`，**这么写其实有一个问题，就是数值越界，例如left和right都是最大int，这么操作就越界了，在[二分法](https://programmercarl.com/0035.搜索插入位置.html)中尤其需要注意！**
>
> 所以可以这么写：`int mid = left + ((right - left) / 2);`

上方内容指的是另外写一个函数进行递归处理 记得保持边界不变量, 左闭右闭 左闭右开, 要始终统一!

### [538. 把二叉搜索树转换为累加树](https://leetcode.cn/problems/convert-bst-to-greater-tree/)

反中序即可= =, 还有就是其实不用维护vector

### [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

这个题来说, 最先需要搞清楚的是直径怎么计算, 其实对于任何一个根节点来说, 经过此根节点的最长路径, 一定是左子树的最深节点到右子树的最深节点, 经过这个根节点的最长路径一定是这样的, 而对于整颗树来说, 最长路径可能并不经过根节点, 但是一定经过某颗子树的根节点!!!!



所以, 后序遍历, 每个根节点求出左子树的最长路径所经历的结点个数, 右子树的最深叶子节点到根节点的个数

而经过该根节点的最长路径的长度 = left + right + 1 - 1 第一个1是加上根节点, 第二个1是因为路径的边数 = 总节点个数 - 1

而最终返回给上一层的是 1 + max(left, right), 这里应当返回的是从该根节点到最远叶子节点所经过的结点个数

说真的, 对后序回溯越来越熟练了, 而这个题最好的解法就是从下往上处理, 而不是从上往下, 因为前序从上往下时, 到了一个根节点并不知道根节点的左右子树的情况, 而后序就很棒了

思考的时候可以思考叶子节点的后序是怎么一个过程, 也就是空结点返回0, 而叶子节点以及其他节点当然就要返回1(自己) + max(leftNum, rightNum)了, 这样给父节点的就是这颗子树的最长的路径中的节点的个数!!!!

```C++
class Solution {
public:
    int max = -1;
    int diameterOfBinaryTree(TreeNode* root) {
        func(root);
        return max;
    }
    int func(TreeNode *root) {
        if(root == nullptr) return 0;
        int leftDepth = func(root->left);  // 左子树中最长的有leftDepth个节点组成的路径(不包含自己)
        int rightDepth = func(root->right);  // 右子树中最长的有rightDepth个节点组成的路径(不包含自己)
        if(leftDepth + rightDepth > max) max = leftDepth + rightDepth;
        return 1 + std::max(leftDepth, rightDepth);
    }
    int func(TreeNode *root) {
        // 后序
        if(root == nullptr) return 0;
        int leftNum = func(root->left);    // 左子树的最长路径的结点个数(不包含root)
        int rightNum = func(root->right);  // 右子树的最长路径的结点个数(不包含root)
        if(leftNum + rightNum + 1 - 1 > ret) ret = leftNum + rightNum + 1 - 1;
        return 1 + max(leftNum, rightNum);
    }
};
```

# 动态规划

dp基本解题流程

- 状态表示: 先以一个一维数组或二维数组作为一个dp表, 然后将其填满, 而每个下标都有一个值嘛, 而这个值代表一个含义, 而这个含义就是一个状态表示

心得/技巧:

所以dp的核心就是状态表示, 状态转移方程, 状态标识其实就是dp数组的每个元素的含义, 你要这个dp数组存什么东西, 一般都由经验 + 题目来得出, 而状态表示可能正确可能错误, 我们要勇于去定义状态表示, 然后尝试推到状态转移方程, 如果定义对了, 皆大欢喜, 若错了, 就再来一次 , 就是要多定义, 多体会, 多总结~

一般难度下的题的状态表示都是很简单的

## 斐波那契数列模型

### [1137. 第 N 个泰波那契数](https://leetcode.cn/problems/n-th-tribonacci-number/)

推导状态转移方程:  

状态转移方程是什么? dp[i] = x  x就是状态转移方程!!!!  这道题而言: dp[i] 依赖于前三个状态, 而具体怎么依赖呢? 题目已经说的很清楚了, 就是相加. 所以 dp[i] = dp[i-1] + dp[i-2] + dp[i-3], 这个就是这道题的状态转移方程

### [面试题 08.01. 三步问题](https://leetcode.cn/problems/three-steps-problem-lcci/)

状态标识: dp[i]表示到达第i阶楼梯有多少种方式

状态转移方程: 考虑较高阶楼梯, 其实要么是i-1一步上来, i-2上来, i-3上来, 所以dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3];

```C++
class Solution {
public:
    int waysToStep(int n) {
        const int MOD = 1e9 + 7;
        if(n == 1) return 1;
        if(n == 2) return 2;
        if(n == 3) return 4;
        vector<int> dp(n + 1);
        // i下标代表第i个台阶
        dp[1] = 1, dp[2] = 2, dp[3] = 4;
        for(int i = 4; i <= n; ++i) {
            dp[i] = ((dp[i - 1] + dp[i - 2]) % MOD + dp[i - 3]) % MOD;
        }
        return dp.back();
    }
};
```

注意取模的方式  (a + b) % x = a % x + b % x?

### [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

n阶, 其实到达第n阶就可以了

dp[i] 表示有多少种方式到达第i阶楼梯 dp[i] = dp[i - 1] + dp[i - 2], 因为只能走一步 / 两步

### [746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)

求到达楼顶的最小花销, 那么状态表示有两种, 也对应着两种解题方法,  第一个: dp[i] 标识到达i位置的最小花销, 所以返回值也就是dp[n]了. 第二种: 从dp[i]到达楼顶的最小花销, 所以返回值也就是dp[0]和dp[1]的较小值了, 因为要从0或1号台阶开始嘛, 所以就是0或1台阶到达楼顶的最小花销~

### [91. 解码方法](https://leetcode.cn/problems/decode-ways/)

> 这个题相比于前几个入门题来说, 难度上就有了一个小的提升了
>
> 但是现在的总结很遗憾是我看了解析之后的, 并不是直接做出来的, 我觉得还是需要自己先思考思考

状态表示: dp[i]表示字符串解码到i下标字符时的解码方法个数, 所以返回值理所应当就是dp.back(), 也就是最后一个字符时的整个字符串的解码方法

状态转移方程, 其实到了s[i]的时候, 无非两种情况, 单独解码 或 i && i-1两个字符一起解码, 此时就需要具体考虑了

单独解码和两个字符一起解码都有可能失败, **若单独解码成功, 则单独解码贡献的字符串解码方式就是dp[i-1] 若失败, 则至i字符为止, 单独解码i字符的整个字符串的解码方式个数都是0**

**若两个字符一起解码, 也就是i && i-1, 则如果解码成功, 其实就是贡献了dp[i-2]个解码方式, 而若失败, 则0, 因为最后两个字符无法联合解码 则在此情况下, 整个字符串就无法解码, 所以其实就是这样的**

> 我们知道, 状态转移方程肯定是要结合最近一步或两步的结果的, 但是确实... 得思考思考这个方程怎么实现的
>
> 把情况分析清楚之后, 程序就很好写了. 分析这个题的重点在状态转移方程上, 而状态转移方程又需要对题有一定的理解,  也就是到了某个字符之后, 应该怎么解码, 有哪些情况....

## 路径问题

> 总的来说, 总是二维矩阵的模式, 然后每次走一步, 右或下, 求路径的相关问题

### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

> 虽然是第一道二维dp数组, 但是其实比较简单

状态表示: dp\[i][j] 表示到达i, j下标时的路径方法个数

而状态转移方程还是惯例 : 根据附近的状态表示求出, 也很简单, 根据题目, 到达ij只能从它的上或者左过来, 所以, 到达ij的路径方法个数 dp[i]\[j] = dp[i]\[j-1] + dp[i-1]\[j] 注意, 比如从它的左边走一步过来, 是路径走的步数+1, 而不是路径的方法加一, 到了这个地方的路径个数还是那个个数, 只是多了一步而已, 一步是不一个方法!

所以, 这个题只是dp数组变二维了, 其他没有很大的变化

### [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)

实践过了, mn初始化确实麻烦, 因为若第一行或第一列的某一个元素为1, 也就是为障碍物, 则直接影响后面的

而m+1n+1的话, 多的一行一列初始化不变, 而后面的直接进行一个判断即可

---

状态表示: dp[i]\[j] 表示 : 到达ij位置时, 一共有多少种不同的路径

状态转移方程: dp[i][j\] 分两个情况, 有障碍物, 则0, 无障碍物, dpij = dpi-1 j + dpi j-1

### [LCR 166. 珠宝的最高价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

> 原剑指offer - 礼物的最高价值, 没什么区别

其实题目来说还是二维矩阵, 每次往右或往下收集礼物, 然后求出最大价值

状态表示: dp[i][j\] 表示到达ij位置时的最大价值

状态转移方程: dp[i\][j\] 分两个情况, 从上面走和从左边走, 若上面则上面的最大价值 + 自己的价值 左边 则左边的最大价值+自己的价值, 而根据状态表示, 上面和左面的最大价值就是对应坐标的dp值, 因此, 取一个较大值

![image-20231012124126215](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231012124126215.png)

初始化 : 目的: 防止越界, 所以多一行多一列即可, 两个问题: 多出的空间存什么值: 0, 原因略了   下标映射问题, 很简单

而多一行一列就是为了在处理第一行和第一列时它的上&&左不越界嘛, 所以多一行多一列, 让原本的第一行&第一列成为第二行第二列

### [931. 下降路径最小和](https://leetcode.cn/problems/minimum-falling-path-sum/)

状态表示: 以某个位置为结尾 => 到达ij位置时的最小的下降路径

状态转移方程: 某位置的dp值, 也就是路径下降最小和的值 分三个情况, 也就是上一排的三个位置走过来, 所以应该是三者里面的最小值, 而每个的最小值又是它的下降路径最小值 + 自己的值, 而它的下降路径最小值根据状态表示 其实就是dp[对应位置] 因此

![image-20231012124924574](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231012124924574.png)

> 也就是说, 某一个位置的dp值, 取决于它的上一排的若干三个(可能两个), 那么这样层层依赖, 第一排的是固定的, 所以第二排就是固定的,  因此从上至下, 从左至右, 就可以把dp数组填满喽

初始化, 多加一行 两列即可, 且第一行初始化为0 两列初始化为+无穷, 还是两个问题, 填值以及映射问题, 很简单

n*n 则dp 为n+2 * n+2 dp[i]\[j] 表示到达ij下标时的下降路径最小和

那么返回值就是min(dp的倒数第二行的所有元素中的下降路径最小和) (最小值)    (最后一行没意义

其实也可以n+1 n+2 行上多一行, 列上多两列, 就可以解决边界问题了, 且第一行要初始化为0, 其余的多出的两列要初始化为INT_MAX

这样就没什么难度了, 就是边界需要稍微注意一下~

### [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

状态表示 : 以某个位置为结尾 xxxx  : dp[i][j\] 表示 到达ij位置时的最小路径和

状态转移方程: 依旧两个情况, 从上面来或者从左面来, 所以取两个情况的较小值, 而每个情况的值都是原始位置的最小路径和+自己位置的值, 而根据状态表示, 原始位置的最小路径和本身就是dp[x][y\]

![image-20231012130926657](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231012130926657.png)

典的不能再典了

### [174. 地下城游戏](https://leetcode.cn/problems/dungeon-game/)

> 有点难???? 二刷依旧不是彻底明白为什么要逆向dp

> 2 : 突然明白了一些, 和二叉树的前序与后序的选择是一样的, 前序就是根据父节点, 得出该结点, 后序就是左右孩子有了结果, 再求自己
>
> 而这个题从左上到右下 就类似前序, 从右下到坐上就类似后序
>
> 如果右边和下面的状态确定了, 那么ij位置就一定可以确定了, 道理就是这样的: 状态表示为从ij到达重点所需的最小血量, 根据右边和下面的dp值, 以及当前位置的值(加血or扣血), 就可以确定dp[i][j\]
>
> 而如果前序呢? 也就是知道上方和左方, 状态表示为从起始位置到这个位置所需的最小血量? 这个.....总之, 正向dp仔细想想总是怪怪的, 而反向dp总是更对的
>
> 实在不行就两个都想想, 都试试呗~

这道题的关键在于为什么要逆向dp而不是正向dp, 若正向, 则状态表示为: dp[i][j\]表示从起点出发, 到达ij位置所需要的最小健康值.  也就是为以什么什么为终点......   而逆向dp的状态表示为 : 从ij位置出发, 到达终点所需的最低健康点数

为什么正向不行? 因为仅记录mn的所需最低健康点数是不对的, 因为可能中间直接-1000 +1000, 也就是只能保证到达mn时健康值>0, 但是中间是有可能健康值<=0的, 所以还需要记录这个过程中所需的最低健康点数的最大值

逆向dp: 某位置的dp值等于下一个位置(右或下)所需的最低健康点数 - 当前值(负数), 比如下一个位置所需最低值为5, 当前为-6, 则就是12

## 简单多状态dp问题

### [面试题 17.16. 按摩师](https://leetcode.cn/problems/the-masseuse-lcci/)

> 每天都有两个状态(两种可能) : 选该天 / 不选该天

状态表示: 为什么说多状态呢? 因为每个地方的dp值都有两个状态, 也就是, 选还是不选, 选当前值时, 总的最大预约时长 , 不选当前值时, 总的最大预约时长

则每个下标都对应存储两个值, 选择该位置的情况下的最大预约时长, 不选该位置的情况下的最大预约时长

状态转移方程: 选的dp值 dp[i] = 不选上一个的最大预约时长 + 自己的值  不选的dp = 上一个的最大预约时长(两个状态的较大值) + 自己的值

所以返回值也就是最后一个位置的两个状态的最大预约时长的较大值~

> 关键在于, 其实如果前面一个位置的两个状态的dp值(最大值)确定了, 那么后面一个位置的也就确定了, 因为根据状态转移方程得知每个位置的选或不选的最大结果都只和前一个位置有关, 所以层层后移推导, 就会得出最终结果~

### [198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

> 每个房屋两个状态, 两个可能: 偷或不偷, 且dp[i] 只和前一个位置有关, 层层推进

和上一个一模一样=. =

> i位置偷的话, 则前一个和后一个就不能偷, 那, 状态转移方程中i位置只考虑前一个可以吗? 其实是可以的, 因为后一个的最大值到时候会考虑前一个的, 所以不需要每个值都考虑前后
>
> 你确实需要考虑前后, 但是你不用立刻考虑后, 因为后到时候会考虑你~

### [213. 打家劫舍 II](https://leetcode.cn/problems/house-robber-ii/)

和上一个太像了, 唯一不同就是首尾连接

思路是没想到的, 其实Ⅰ和Ⅱ的唯一区别就是, 比如0号偷, 那么尾是不受影响的, 只要n-2不偷, n-1就可以偷, 也就是0和n-1可以同时偷, 而打家劫舍Ⅱ中的首偷了, 则1和n-1都不能偷, 其实这就是唯一的区别的, 没有其他区别了!!!!  认识到这点很重要, 所以这个题可以转化为打家劫舍Ⅰ的问题

**所以, 0号偷, 则1 n-1不能偷, <u>中间的2 - n-2为线性问题</u>, 转化为打家劫舍Ⅰ   而0号不偷, 则首尾不需要再注意了, <u>所以1 - n-1为线性问题</u>**

这个思路确实牛, 没想到, 可以学习理解一下

### [740. 删除并获得点数](https://leetcode.cn/problems/delete-and-earn/)

这个题感觉描述的不是很到位, **其实本质就是: 选择x, 则获取所有x的点数, 但是x-1 与 x+1就不能选了, 计算怎么选择是最大的结果**

> **看清这个本质很重要!!!!!**

和打家劫舍Ⅰ很像, 因为首尾不相连, 并且有区别的是, 可能数组的相邻元素的值并不相邻

状态表示: 两个值: 选该元素的最大值, 不选该元素的最大值

状态转移方程: 选该元素的最大值 = 不选x-1的最大值 + 该元素 * 个数

不选该元素的最大值 = x-1选/不选的最大值的较大值

> 本质就是选x 则x-1 x+1就不能选, 且每个值可能有多个, 看最大的选择结果为多少, 神似打家劫舍Ⅰ, 因为首尾不相连, 且可能相邻元素可以都选, 因为可能并不是值相邻的关系 = =

### [LCR 091. 粉刷房子](https://leetcode.cn/problems/JEj789/)

> 每个房子都有三个状态, 也就是三个可能, 红蓝绿

状态表示: 以i位置为结尾, i位置涂为某颜色的最小开销(所有),  **而颜色有三种, 这就是多状态**, 所以用三个数组即可存储, 类似于之前的选/不选 

三个值, 分别为: 当前房子粉刷为红的所有房子的最低花销, 当前房子粉刷为蓝的所有房子的最低花销, 当前房子粉刷为绿的所有房子的最低花销

状态转移方程: f g h分别代表三个dp数组, g[i] = i-1不粉刷为当前颜色时的最小开销 + 当前开销 也就是 min(f[i-1], h[i-1]) + 当前花销(通过costs数组获取)

> 再次理解了 简单多状态dp
>
> 无非就是每个房子(元素)三个状态, 分别记录每个状态的最小花销, 最终返回三个的较小值即可
>
> 其实和打家劫舍很像, 那个是i选, i-1 i+1就不能选, 这个是i为某颜色, 则i-1 i+1就不能为该颜色, 所以基本都差不多的= =

```C++
class Solution {
public:
    int minCost(vector<vector<int>>& costs) {  // 红 蓝 绿
        int n = costs.size();  // n个房子
        vector<int> red(n);   // red[i]表示i号房子粉刷为红色时的最小所有开销
        vector<int> blue(n);  // blue[i]表示i号房子粉刷为蓝色时的最小所有开销
        vector<int> green(n);  // 同上
        red[0] = costs[0][0];
        blue[0] = costs[0][1];
        green[0] = costs[0][2];
        for(int i = 1; i < n; ++i) {
            red[i] = min(blue[i - 1], green[i - 1]) + costs[i][0];
            blue[i] = min(red[i - 1], green[i - 1]) + costs[i][1];
            green[i] = min(red[i - 1], blue[i - 1]) + costs[i][2];
        }
        return min(min(red.back(), blue.back()), green.back());
    }
};
```

这里是把dp数组按照状态分为了三个小的数组, 也就是红蓝绿

也可以直接搞一个dp二维数组

初始化: 保证不越界, i要访问i-1, 所以可以直接初始化0下标, 也可以加一个虚拟首元素, 直接初始化为0即可~~~~哈哈哈哈

### [309. 买卖股票的最佳时机含冷冻期](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

> 应该划分为哪几个状态呢????????????? 可恶啊  
>
> 看完解析之后的感受: 由于是第一个股票题, 所以状态划分有点不确定, 且状态之间的转移需要想想
>
> 也就是说, 我每天的0点, 进入了新的一天都可以立刻做一个事情/不做任何事情, 然后进入一个状态, 这个状态就是我今天的状态
>
> 持股: 当天买入 或者 之前买过
>
> 不持股: 要想不持股, 我当天卖了就明天进入冷冻期, 就是不持股, 或者我昨天冷冻期, 今天不买/不做任何事, 不就是不持股吗

所以, 大致为两个状态: (这里的状态都是指我今天立刻做了某件事/不做任何事, 然后我所处的状态, 其实主要就是根据我当天做了什么) 持有股票和不持有股票

1. 持股状态   :   昨天持股, 今天不做任何事情, 即持股     昨天4, 今天购买, 持股  昨天3, 今天购买, 持股
2. 不持股 - 即将进入冷冻期  :  昨天持股, 今天卖了, 即将进入冷冻期
3. 不持股 - 冷冻期   : 昨天即将进入, 今天冷冻
4. 不持股 - 非冷冻期, 不持股   : 昨天冷冻, 今天进入非冷冻, 只需要今天不购买, 那如果昨天冷冻, 今天购买, 自然就是持股了

状态机略了, 也就是状态转化图略了

状态转移方程:  根据状态机很容易得出, 因为之间的变化已经很清楚了

我自己是划分了4个状态, 而bite划分了3个, 说实话, 真不如我这个, 接下来实现代码

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(4));  // 持股, 不持股-即将冷冻, 不持股-冷冻, 不持股-非冷冻(可购买)
        dp[0][0] = -prices[0];
        dp[0][1] = dp[0][2] = dp[0][3] = 0;
        for(int i = 1; i < n; ++i) {
            dp[i][0] = max(max(dp[i - 1][0], dp[i - 1][2] - prices[i]), dp[i - 1][3] - prices[i]);      // 做天持股， 昨天冷冻， 昨天可交易
            dp[i][1] = max(max(dp[i - 1][0] + prices[i], dp[i - 1][2]), dp[i - 1][3]);    // 昨天持股，今天售出就即将冷冻了(或者今天买了立马卖也是即将冷冻，但是这样的话)
            dp[i][2] = dp[i - 1][1];   // 昨天即将冷冻， 今天冷冻
            dp[i][3] = max(dp[i - 1][2], dp[i - 1][3]);   // 昨天可购买，或者昨天冷冻
        }
        return max(max(max(dp.back()[0], dp.back()[1]), dp.back()[2]), dp.back()[3]);
    }
};
```

ok过了

### [714. 买卖股票的最佳时机含手续费](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

> 直观来说比上一个简单了一些

状态划分:

1. 持股 , 前一天不持股, 购买 或者前一天持股, 不做任何事, 就保持持股
2. 不持股, 前一天不持股, 今天不持股, 前一天持股, 今天售出

比较简单 = =

### [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

这个题, 也就是说只能买一次, 然后不同天卖一次, 所以,其实就是求数组的两个元素的最大差值的感觉, 但是如果用dp问题解决的话

每天俩状态: 持股 / 不持股

1. 持股  = 昨天持股 / 昨天不持股且可购买

2. 不持股 - 且可购买  =  昨天可购买

3. 不持股 - 且不可购买   =   昨天不可购买 / 昨天持股, 然后今天卖了就不可购买了

### [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

这个相比于上一个无非就是可以多次购买-售出

状态:

1. 持股状态 - 昨天持股  / 昨天不持股, 今天购买
2. 不持股 - 昨天不持股  / 昨天持股, 今天售出

这个和手续费那个唯一, 真的唯一的区别就是出售时要交手续费, 没有其他区别了

### [123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

这个就是限制只能购买售出两次, 也就是买卖两次

状态表示: dp[i] 为当天结束时的最大利润, 而具体来说, 每天都有不同的情况, 分为多个状态

大致分为 持股 / 不持股

1. 持股: 第一支
2. 持股: 第二支
3. 不持股: 什么都没买
4. 不持股: 第一支已卖
5. 不持股: 第二支已卖

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(5)); // 0-持股1 1-持股2 2-不持股0 3-不持股1 4-不持股2
        dp[0][0] = -prices[0];
        dp[0][1] = -prices[0];
        dp[0][2] = dp[0][3] = dp[0][4] = 0;
        for(int i = 1; i < n; ++i) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][2] - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][3] - prices[i]);
            dp[i][2] = dp[i - 1][2];
            dp[i][3] = max(dp[i - 1][3], dp[i - 1][0] + prices[i]);
            dp[i][4] = max(dp[i - 1][4], dp[i - 1][1] + prices[i]);
        }
        vector<int> &v = dp.back();
        return max(max(max(max(v[0], v[1]), v[2]), v[3]), v[4]);
    }
};
```

过了, 但是, 我还是想去想想这个是怎么做到的

> 首先第一天来说, 各个状态下的最大利润是可以确定的, 没错吧?
>
> 那么, 第二天基于第一天的各个确定好的状态下的最大利润, 它的最大利润也可以确定, 没错吧
>
> 举例: 第二天的持股1状态下, 有两种可能, 取两个的较大值, 其实就是该天在持股1状态下的最高利润
>
> 所以这样下来, 最后一天的各个状态的最大利润就可以确定, 然后取最大值, 不就是最后一天的最大利润嘛????~~~~

### [188. 买卖股票的最佳时机 IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)

上一题限制交易两次, 这个为k次, 也就是不确定

而交易两次的话, 有5个状态, 持股有两个, 不持股有2+1个

所以k次, 持股有k个, 不持股有k+1个分别为持1股, 2股, ... k股

而不持股为 已交易0股不持股, 已交易1股不持股, 已交易了2股不持股, 已交易k股不持股

所以, 持股的f数组, 不持股的g数组, 每一天都有2k+1个状态

fg数组都是二维的, 因为有两个因素: 哪一天, 具体哪个状态

状态表示: 第i天的最大利润, 且第i天可以细分为2k+1个状态, 所以每个状态都有一个最大利润, 然后求最大值即可

状态转移方程: 第i天的持j股 : 1. i-1天持j股   2. i-1天已交易j-1股, i天买一股即可

第i天的已交易j股, 不持股 :  1. i-1天已交易j股, 不持股  2. i-1天持j股, 第i天卖掉即可

> 所以, 其实并不难, 核心就是每天都有多个状态, 多个可能!!!!

## 子数组系列

**感受:**

**子数组系列, 基本都是, 从一个大的数组中, 寻找符合某条件的子数组的个数/长度/其它参数**

**而, 这样的子数组一定是连续的, 这个是关键, 所以基本状态表示都是, 以某元素为结尾的子数组........这样类似的状态表示**

整体来说都不难

### [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

![image-20231014202447618](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231014202447618.png)

> dp问题, 首先确定状态表示

状态表示: dp[i] 表示 以i位置元素为结尾的所有子数组里面的最大和  (这些子数组以i下标的元素为结尾)

所以 一共的情况其实就是上面的那几个

状态转移方程: 

这些子数组可以分为两类, 1. 只包含i自己  2. 包含其他元素, 最后一个元素为i

我们要找这些里面的最大和, 第一个的和已经知道了, 后面几个的最大和怎么求呢?

其实, 后面几个的子数组有一个共同点, 抛去最后一个i元素之后, 其实**求的就是以i-1元素结尾的所有子数组里面的最大和, 而这个最大和加上一个nums[i], 就是以i结尾的所有子数组的最大和**, 此时, 这个最大和再和Nums[i]比较一下,  也就是第一个子数组, 结果就是dp[i]应该存储的了

> 这个很牛逼啊, 能理解倒是能理解, 但是自己想出来是真想不出来

这样一来, dp[i]又和dp[i-1]联系起来了

这样一来 dp[i] = max(nums[i], dp[i-1] + nums[i]);  确实牛逼    

### [918. 环形子数组的最大和](https://leetcode.cn/problems/maximum-sum-circular-subarray/)



---

---

相比于最大子数组和的差别就是首尾可以相连, 所以可以直接分为以下两个情况

1. 最大和子数组不同时包含首尾两个元素
2. 最大和子数组包含首元素和尾元素且不是全部元素, 也就是数组前方有一段, 尾部有一段

> 情况1, 可以用上一题的解法来求最大值, 情况2, 首尾元素包含, 且不是全部元素(若全部元素就是情况1了), 也就是前面一段, 后面一段, 且这两段相加是最大子数组和, 那么, 中间剩余的就是最小子数组和, (min + max = sum), 所以, 求情况2的最大子数组和可以转化为求最小子数组和的问题

1的解法和最大子数组和一样, 2的解法: 当首尾两段的和是最大和时, 中间的子数组的和就是最小的和, 因为sum = max + min, 当max越大, min越小, max最大, min最小, 所以求解情况2, 可以转化为求解最小子数组和, 然后sum - min

特殊情况: 当最小子数组和 = sum时, 说明数组全部为负数, 最大子数组和为0, 也就是空的, 这是不对的, 此时不能通过sum - min 获取最大子数组和, 因为为空了, 所以此时只能取情况1的最大和

### [152. 乘积最大子数组](https://leetcode.cn/problems/maximum-product-subarray/)

hot100, 所以再做一次喽~

dp[i]表示以i元素为结尾的乘积最大子数组的积, 但是, 不能像最大子数组和那样, 因为负数乘负数等于正数, 负数乘正数等于负数

所以, 我们需要维护两个数组, 一个是乘积最大子数组, 一个是乘积最小子数组

若i为正数, 则max = 它自己, 它和前一个元素为结尾的最大子数组的积的积 min = min(它自己, 它和前一个元素为结尾的最小子数组的积的积),

负数同理

---

> hot100

> 首先, 是不是, 若x>0, 乘积越大, 结果越大, 乘积越小结果越小, x<0, 乘积越小结果越大, 乘积越大结果越小?
>
> 没错, 经过验证, 是这样的
>
> 所以我们可以根据判断nums[i]的值是否大于0, 来获取以i元素为结尾的子数组的最大乘积和最小乘积, 没错
>
> 而i+1位置是否大于0未知, 所以它需要的是i位置的最大乘积还是最小乘积也未知, 所以每个位置都需要求最大乘积和最小乘积
>
> 所以这个题也能归类为一个多状态dp问题 = =

所以, 这个题需要两个dp表, f数组的状态表示为: dp[i] 为 以i元素为结尾的所有子数组中的最大乘积, 另一个g数组dp表的状态表示为: dp[i] 为以i元素为结尾的所有子数组的最小乘积

### [1567. 乘积为正数的最长子数组长度](https://leetcode.cn/problems/maximum-length-of-subarray-with-positive-product/)

这个和上一个题很像

状态表示: dp[i] 表示以i元素为结尾的乘积为正数的最长子数组的长度

但是dp[i] 不能直接 = dp[i - 1] + 1, 因为确实dp[i-1]为以i-1元素为结尾的乘积为正数的最长子数组的长度, 但是nums[i] 如果大于0, 那没什么问题, 但是如果nums[i]为负的, 就错了

如果为负的, 其实dp[i]应该是 = i-1为结尾的乘积为负数的最长子数组的长度, 这样再乘一个负的 就是正的了

**所以需要维护两个dp表**

并且这里还有一些情况, 当维护f表和g表时, 比如如果nums[i] > 0, 则g[i] 应该是g[i-1] + 1, 但是不能直接这样, 因为如果g[i-1]为0, 则g[i]应该为0, 而不是1, <u>这个我也考虑到了</u>

### [413. 等差数列划分](https://leetcode.cn/problems/arithmetic-slices/)

状态表示: dp[i] 表示 以i元素为结尾的等差数列的个数

状态转移方程: 若nums[i] - nums[i - 1] == nums[i -  1] - nums[i - 2]; 则dp[i] = dp[i - 1] + 1;  (思考思考就好了~)

否则 dp[i] = 0;

没错, 就是这么简单, 其实很简单啊, 如果确实三个元素等差, 则至少有一个新的吧, 然后dp[i-1]为以i-1为结尾的所有等差数列的个数, 这些等差数列都可以加一个nums[i]嘛, 所以就都变成了一个新的等差数列, 再加上一个三元素的, 所以就是dp[i - 1] + 1了

即使dp[i - 1]=0, 也没事的, 如果条件成立就是一个新的呗

### [978. 最长湍流子数组](https://leetcode.cn/problems/longest-turbulent-subarray/)

> 首先明确什么是湍流子数组, 也就是元素之间的比较符号一直颠倒
>
> 若只有一个, 则一个也是
>
> 若两个, 且不相等, 就是2
>
> 若三个, 则必须相互颠倒了

状态表示: dp[i]表示以i元素为结尾的最长湍流子数组的长度

状态转移方程: 分情况

```C++
if(arr[i] == arr[i - 1]) dp[i] = 1;
else if((arr[i] > arr[i - 1] && arr[i - 1] < arr[i - 2])
    || (arr[i] < arr[i - 1] && arr[i - 1] > arr[i - 2])) dp[i] = dp[i - 1] + 1;
else dp[i] = 2;
```

1. 当nums[i] == nums[i - 1] 则dp[i] = 1; 不用考虑

下面的就是nums[i]与nums[i - 1]不相等的情况:

2. 若最后三个满足湍流 则 dp[i] = dp[i - 1] + 1;

3. 否则就是要么大小顺序一致, dp[i] = 2, 要么就是nums[i - 1] == nums[i - 2], 则dp[i] = 2 归类为最后一个else

### [139. 单词拆分](https://leetcode.cn/problems/word-break/)

> hot100

状态表示: dp[i] 表示以i字符结尾的前沿整体字符串能否拼接成功, 自然最终就是返回dp.back();

状态转移方程: 在求dp[i]时, 遍历j 从 i 到 0, 记end为i + 1, 然后也就是dp[j - 1] && s.substr(j, end - j)在字典中存在, 则代表dp[i]为true, 其实很简单, 就是前半部分字符串可以拼接成功, 且后半部分字符串在字典中, 则整体就可以拼接成功, 而到了i下标时, 需要逐渐前移遍历, 也就是后半部分字符串不断增大, 前半部分不断减小, 只要某一处两半部分都可以拼接成功, 则dp[i]为true

当遍历到0位置时, 就是求i位置前沿全部字符串是否在字典中, 此时dp[j - 1]不存在, 需要注意

简单来说, 求dp[i]时, 就是前半部分字符串, 后半部分字符串, 后半部分逐渐变大, 前半部分逐渐减小, 前半部分可以直接通过dp值获取, 后半部分通过字典查询

```C++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> dict;
        for(string & s : wordDict) dict.insert(s);
        vector<bool> dp(s.size(), false);
        dp[0] = dict.find(s.substr(0, 1)) == dict.end() ? false : true;
        for(int i = 1; i < s.size(); ++i) {
            int end = i + 1;  // 要查找的字符串的终止下标(左闭右开)
            for(int j = i; j >= 0; --j) {
                if(j == 0) {
                    dp[i] = dict.find(s.substr(0, end - 0)) != dict.end();
                } else {
                    if(dp[j - 1] && dict.find(s.substr(j, end - j)) != dict.end()) {
                        // 前面可以组成, 且剩余部分存在
                        dp[i] = true;
                        break;
                    }
                }
            }
        }
        return dp.back();
    }
};
```

> 这个如果加一个虚拟首元素, 则可能会稍微方便一点, 只是初始化的方式不同而已

![image-20231015150852302](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231015150852302.png)

### [467. 环绕字符串中唯一的子字符串](https://leetcode.cn/problems/unique-substrings-in-wraparound-string/)

> 感觉和978最长湍流子数组很像

状态表示: dp[i]表示以i字符结尾的不同非空子串在base中出现的次数

状态转移方程: 

任意一个字符, 单个字符组成的子串肯定在base中, 这个是1

abc d  

若i字符和i-1字符相衔接, 则包含i-1字符和i字符组成的子串的个数为dp[i - 1], 因为只是每种情况多了一个字符而已, 所以就是dp[i - 1]个情况  所以, dp[i] = 1 + dp[i - 1];

**但是问题是, 最终结果不能是dp数组全部的和, 因为完全可能有重复的 = =**

如果有两个d 且在不同的位置怎么办????   比如一个d的dp值为4, 一个d的dp值为3, 则4的情况一定包含3????

没错的, 所以要保存一个所有字符结尾的最大值即可

> 吗的, 我好棒啊, 这都直接做出来了?????

> **这本来就很简单好不好, 弱智一样你**

```C++
        for(int i = 1; i < s.size(); ++i) {
            dp[i] = 1;
            if((s[i] == 'a' && s[i - 1] == 'z')
            || s[i] - s[i - 1] == 1) {
                // 相连
                dp[i] += dp[i - 1];
            }
            if(dp[i] > arr[s[i] - 'a']) arr[s[i] - 'a'] = dp[i];
        }
```

这里的逻辑要搞清楚= =

## 子序列问题

子序列, 因为子序列的元素可以在原数组中不连续, 因此基本上都不像子数组一样: dp[i]表示以i元素为结尾的某子数组.....基本子数组是O(N)的, 而子序列处理dp[i]时, 需要遍历0 - i-1, 所以基本就是O(N^2)了, 而有些题因为比较复杂, 所以必须二维dp, 存储j, i元素为结尾的子序列...... 具体还要看具体题目

### [300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)

> hot100

> 直接dp干就行了
>
> 碰壁了, 因为这个和过往的子数组系列的题的最大差别是子序列可以不连续
>
> **那, 这个其实n^2肯定是能解的, 但是... 就有点没意思了**
>
> = = 就n^2吧, dp的话只能这样

> <u>非常非常经典???</u>

状态表示: dp[i]表示以i元素结尾的最长严格递增子序列的长度

状态转移方程: 求dp[i]时, 并不只需要dp[i - 1], 而是需要遍历0 - i-1, 当nums[i] > nums[j]时, 更新dp[i] = max(dp[j] + 1, dp[i])

![image-20231015195857289](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231015195857289.png)

### [376. 摆动序列](https://leetcode.cn/problems/wiggle-subsequence/)

> **2 : 其实很简单, 对比上一个, 这个无非就是, dp数组或者说你不能只记录每个位置的以该元素为结尾的最长摆动子序列的长度, 还需要记录该元素与最长摆动子序列的上一个元素的大小关系, 这样才方便后序元素判断, 仅此而已**

> 这个和最长湍流子数组很像, 只是这个是子序列, 也就是元素之间可以不连续
>
> 像湍流子数组就很简单, 因为dp[i]只需要看nums[i] nums[i - 1] nums[i - 2]之间的关系即可, 不用考虑其他的
>
> 但是这个就不一样了, 这个和上一题一样, 子序列问题需要向前遍历

状态表示: 以某个位置元素为结尾, 然后分析问题

dp[i]是一个pair, first表示以i下标元素为结尾的最长摆动子序列的长度, 而second是一个int, 表示该元素与摆动序列中上一个元素的大小关系

状态转移方程:

> 我怎么感觉这个dp表不能只存长度啊, 还需要存该元素与摆动数组中上一个元素之间的大小关系, 不然怎么搞...
>
> 没错, 直接过了, **没压力, 我太聪明了**

和上一个题一样, 序列问题到i元素时都需要遍历0 - i-1, 当摆动条件符合(借助dp[i].second)时更新dp[i]的first和second

这个second挺妙的

### [673. 最长递增子序列的个数](https://leetcode.cn/problems/number-of-longest-increasing-subsequence/)

好爽, 这些题基本都是一看就有思路了, 没难度啊= =

过了...懒得看下面

---

> 2 : 这个题关键在于, 最长递增子序列多个时, 有可能都是以某一个元素为结尾, 有可能是以多个元素为结尾

状态表示:

**pair, first存储以i元素为结尾的最长递增子序列的长度, second存储对应的最长递增子序列的个数**

状态转移方程

依旧是遍历i-1 到 0

若nums[i] > nums[j]

则试着更新最长递增子序列的长度, 若可以更新, 同时还要更新个数

若没有更长的, 但是有同样长的, 要加上个数

全局维护一个max_len记录全局最长的递增子序列的长度, max_len记录对应的个数

每处理完一个元素的dp值, 都要尝试更新全局的个数和长度, 或者新增全局的个数

### [646. 最长数对链](https://leetcode.cn/problems/maximum-length-of-pair-chain/)

> 这个题和传统的子数组 / 子序列的问题的区别是: 传统的子数组和子序列, 在到i元素时, 可能的前一个目标值一定在i的左边, 而这个题的i的前一个目标值可能在i的右边的, 因为数组的并不是以v[0]进行排序的!!!!!
>
> 所以, 如果进行一个预处理, 就会好很多, 按照v[0]进行排序, 这样一来, 到i元素时, 可能的前一个目标值一定在0 - i-1范围内, 而不在i的右边
>
> 这样就可以像处理子序列问题来处理这个问题了

预处理: 先按照v[0]进行排序

状态表示: dp[i] 表示以i元素为结尾的最长数对链的长度!!!!

状态转移方程: 直接遍历0 - i-1, 若符合条件, 则更新

现在考虑一个问题: 也就是 在找到第一个合理的值之后, 要不要结束

<u>**比如 现在处理的dp[i]的数对是  10  12 而前面有  3 9   3 6   2 3 这样的数对, 是否first越大, dp值一定越大呢? 是的,  那first一样, dp值一定一样吗? 是的,  那这样的话, 是不是就不用继续往前遍历了呢??? 是的**</u>

> 这里挺牛逼~~~

**结论: 找到第一个符合要求的直接结束即可**

所以这题和最长递增子序列几乎没什么差别的, 只是判断条件稍微改变了一下,  并且需要预处理一下

> 既然他都说了你组成的数对链可以顺序随意, 不用按照原本数组顺序, 那... 我为什么不把数组改为对自己有益的格式呢?

### [1218. 最长定差子序列](https://leetcode.cn/problems/longest-arithmetic-subsequence-of-given-difference/)

> 这个相对简单点, 直接dp

状态表示: dp[i] 表示 以i元素为结尾的最长定差子序列的长度

状态转移方程: 求解dp[i]时, 肯定是要遍历前面的所有的0 ~ i-1, 也就是n^2复杂度

然后保存一个最大值(最长的定差子序列的长度)~

> 逐步的优化:
>
> 1. 不用遍历前面全部的, 因为diff已经知道了, 所以前面的目标值也就知道了, 且只要遇到一个目标值就可以, 因为最后一个目标值的dp值一定>=前面的目标值的dp值 比如  12356734  diff = 1, 则这两个3的dp值一样都是3喽
> 2. 如果按照第一点来, 我们还是需要遍历0 - i-1, 但是更优化的是 : 直接使用哈希表进行动态规划, 也就是key为元素值, value为dp值, 也就是目前最长定差子序列, 这样就是O(N)了

所以, 用哈希表做dp能成功主要是因为这里的diff已经给了!!!!! diff有了, 你要找的目标值就有了, 因为你所组成的定差子序列的前一个元素是已知的

![image-20231015215143501](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231015215143501.png)

## 子序列问题 - 二维dp

### [873. 最长的斐波那契子序列的长度](https://leetcode.cn/problems/length-of-longest-fibonacci-subsequence/)

有趣, 还不错, 这个题确实有趣

O(N^3)利用哈希表优化为O(N^2)也很有趣

这个初始化为2, 也挺关键的

---

状态表示:

dp[i] 表示以i下标元素为结尾的最长的斐波那契子序列的长度

状态转移方程:

> 因为是子序列问题嘛, 所以如果dp的话肯定是n^2复杂度的, 主要是因为子序列问题的序列的元素组成可以不连续, 所以需要遍历0 - i-1
>
> 但是dp表中的关键是 不能只存储长度, 还要存储该最长斐波那契子序列的上一个元素的值, 这样才好判断i元素是否符合条件
>
> 其实之前也见过这样的题, 也就是除了dp值外, 还要存一些用于判断条件是否成立的值, 这是子序列问题的常见问题和套路

> **按照上面的解法, 也是不对的, 因为任意一个元素都不能只存一个前一个元素,** 
>
> **这个题一维dp解不了, 需要二维dp**

**状态表示: dp[i][j\] 表示以ij元素为末尾的最长斐波那契子序列的长度**



![image-20231016114225692](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231016114225692.png)

二维dp\[i][j\]表示以ij元素为结尾的最长的斐波那契子序列的长度, 为什么这样可以? 因为ij知道, 前一个元素就知道了, 这样直接在0 - i-1范围内查找这个目标元素即可, 这是固定的!!!! 这样, dp\[i][j] = dp[k][i\] + 1

![image-20231016141537601](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231016141537601.png)

j逐步向后, i在0 - j-1范围内逐步向前, 这就已经是O(N^2)了, 目标元素已知, 就需要在0 - i-1范围内查找, 但是这样是可以优化的, 因为目标元素已知, 且元素值和下标一一对应, 所以直接用哈希就可以O(1)求出k的值为多少, 此时dp[k][j\]就直接得出了

注意这里的i 永远 < j, 所以二维dp数组的横坐标永远小于纵坐标, 

![image-20231016142027723](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231016142027723.png)

求解dp\[i][j\] 时需要dp[k\][i], k < i i < j  所以dp数组的求值顺序是从上到下, 从左到右

dp[i][j\] dp[j\][i\]   其实无非就是这个矩阵的左下方还是右上方喽, 都一样, 逻辑对了就行~

```C++
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& arr) {
        int n = arr.size();
        unordered_map<int, int> hash;
        for(int i = 0; i < n; ++i) hash[arr[i]] = i;  // 数值 : 下标
        vector<vector<int>> dp(n, vector<int>(n, 2));  // n*n
        int ret = 2;
        for(int j = 2; j < n; ++j) {
            for(int i = j - 1; i >= 0; --i) {
                // 现在最后两个元素确定了, 则倒数第三个(目标值)就确定了
                int num = arr[j] - arr[i];
                if(hash.find(num) != hash.end()
                && num < arr[i]) {
                    // 此时以ij为结尾至少可以组成一个斐波那契数列
                    dp[i][j] = max(dp[hash[num]][i] + 1, dp[i][j]);
                }
                if(dp[i][j] > ret) ret = dp[i][j];
            }
        }
        return ret == 2 ? 0 : ret;
    }
};
```

> hash表只是在找k的时候方便一点, 查找也就是arr[j] - arr[i] 的结果在0 - i-1这个范围内的哪个下标中存储着时快速一点

### [1027. 最长等差数列](https://leetcode.cn/problems/longest-arithmetic-subsequence/)

这个和上一个斐波那契感觉很像, 主要是状态表示不能是以i元素为结尾的最长等差数列的长度, 这是不对的, 因为i需要遍历0 - i-1, 你到了j之后, j这里只有这一个长度信息, 是完全不够的

所以直接二维dp, dp[i][j\]表示以j, i元素为结尾的最长等差数列的长度, 这样的话, **任意一个元素都可以和多个元素搭配成等差数列, 而不仅限于一维dp的只能存储一个值**

![image-20231204141940868](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231204141940868.png)

目前为止, i外层, j内层, 然后找target在j的左边, 且越靠近j的越符合(注意, 和上图略有差别)

而找target, 如果是遍历找, 就N^3会超时

可以把元素 : 下标数组 预处理在哈希表中, 但是如果给的用例很恶心的话, 还是O(N^3)

最佳解法: 我们遍历i, 遍历j, 时, 可以存储i的左边的第一个某元素的下标, 而后面i右移, 需要用到j的左边的第一个某元素的下标时, 这时候就已经预处理好了

如果是二维矩阵, 我们依旧是从上往下, 从左往右

其实没必要从左到右, 因为用的永远是上一行的, 用不到这一行左边的, 因此从上到下就行

注意这里的target, 不是nums[i] - nums[j\], 这他妈是等差数列?    1 4 5 不是等差数列

## 回文串问题

1. 回文串且子串的问题中, 典型的是二维dp把每个子串是否是回文串记录下来, 其实就是遍历所有子串, O(N^2)

2. <u>**要么就是二维dp, 一维表示子串起始, 一维表示子串的终止**</u>

3. 要么就是和其它的结合一下, 比较特殊 : 二维dp记录每个子串  +  一维dp  我记得是132题 和 单词拆分这个题很像

12常见

### [647. 回文子串](https://leetcode.cn/problems/palindromic-substrings/)

用到下一行, 没问题, 可是处理最后一行时, 难道不会越界吗?

其实最后一行只有一个元素要填, 且用不到下一行, 所以不会越界

一个矩阵, 反向斜对角线其实不用下一行, 且右边这一条斜的也不会用, 其余的会用但是不会越界, 这种还是要画个图比较好

---

三种解法, 此处只学习dp解法, 且这个解法虽说并不是这个问题的最佳解法, 但是它是可以解决回文问题的, 甚至有时候可以把hard -> easy

(注 : 这个题中, 即使子串的内容相同, 只要开始和结尾不同, 那么就是不同的子串, 所以, **需要判断所有的子串**)

dp解法核心思想:

用一个dp表, 将所有子串是否是回文的信息, 保存在dp表中

这样一来, 两层for即可, 外层for表示子串的起始, 内层for表示子串的结尾, 也就是一个二维dp表, 横坐标表示i, 纵坐标表示j, dp[i][j\]表示s[i, j\]这个子串是否是回文的, 且左闭右闭, 所以i <= j    j >= i

![image-20231106142540027](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106142540027.png)

状态转移方程:

依旧, dpij肯定是要和其他的dp值联系起来的

![image-20231106142701562](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106142701562.png)

初始化: 无需初始化, 因为不会越界, 因为特殊情况已经处理过了

填表顺序: 除了特殊情况, 那么, ij需要用到i+1, j-1, 所以在二维dp表中也就是用到左下方的值, 所以我们需要在dp表中从下往上, 而左右不需要考虑, 因为ij 只会用到下一行的左边那个, 只要下一行有值即可

所以, dp表从下往上填表, 横坐标 - i代表起始, 也就是字符串起始位置要从右往左

![image-20231106144555744](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106144555744.png)

### [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/)

> hot100

**dp解回文子串问题: 可以用一个二维dp表, 将所有子串是否是回文串的信息保存在dp表中**, (那这样的话, 其实直接搞一个pair, 就能同时存储是否是回文子串, 还能存储长度了...) 那对于这个要求最长回文子串的长度话, 直接记录一个max不就行了

其他细节看上一题~

### [1745. 分割回文串 IV](https://leetcode.cn/problems/palindrome-partitioning-iv/)

dp解回文子串问题: 可以用一个二维dp表, 将所有子串是否是回文串的信息保存在dp表中

现在问题是, 要判断是否有三个连续子串都是回文串

起始可以暴力求解, 直接用i表示中间子串的起始, j表示中间子串的结尾, 这样第一个子串和第三个子串的起始结尾也就知道了

这个双层for该怎么写? 其实也不难: 0, i-1   i, j    j+1, n-1   三个区间都是左闭右闭, 但是双层for怎么写???

0<=i-1  i>=1      i<=j  j+1<=n-1    j<=n-2  所以, i<=n-2

所以,    1 <= i <= n-2      i <= j <= n-2

```C++
        for(int i = 1; i <= n - 2; ++i) {
            for(int j = i; j <= n - 2; ++j) {
                if(dp[0][i - 1] && dp[i][j] && dp[j + 1][n - 1]) return true;
            }
        }
```

### [132. 分割回文串 II](https://leetcode.cn/problems/palindrome-partitioning-ii/)

dp解回文子串问题: 可以用一个二维dp表, 将所有子串是否是回文串的信息保存在dp表中

> 然后, 分割0次: 判断整体是否是回文串
>
> 分割1次: 遍历?分割2次: 遍历?(上一题)分割3次: 遍历????这显然不现实
>

状态表示: dp[i]表示s[0, i]这个字符串最小的分割次数

状态转移方程:   (起始就是单词拆分问题)

**此时可以用j从0到i遍历, 若子串 j i是回文, 则此时此方案下的0, i子串的拆分次数为dp[j - 1] + 1, 也就是ji为回文, 0, j-1这个子串的最小拆分次数已经用dp表保存起来了**

这个题和[139. 单词拆分](https://leetcode.cn/problems/word-break/)题是非常像的

为了方便判断某子串是否是回文串, 可以用二维dp表预先记录好每个子串是否是回文串

### [516. 最长回文子序列](https://leetcode.cn/problems/longest-palindromic-subsequence/)

> 这种题, 如果仅用文字描述, 是很难的, banshu记录的很清晰

最开始的想法: dp[i]表示以i元素为结尾的所有回文子序列中的最长长度, 但是这样一来, dp[i]求值时, 肯定是要前面的dp值的, 但是此时前面只记录了最长长度, 根本没法判断是否是回文子序列, 所以不成立, 即使每个dp值再记录一个这个最长子序列的第一个元素的值, 也是很麻烦的, 外层一个i, 内层一个j, j记录了序列的第一个元素, 但是同样长度的可能不止一个, 并且还要遍历0 到 j, 整体来说根本不行

**二维dp, 仍然是横坐标为某子串的起始位置, 纵坐标为某子串的终止位置, dp[i][j\]记录这个子串内部的所有回文子序列中的最长长度**

> 说实话, 这个真的nb

这样一来, 就和回文子串有点像了

![image-20231106180106747](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106180106747.png)

若ij元素相同, 则dp[i][j\], 排除前两种, 此时就等于dp[i+1\][j-1\]的值+2了, 因为dp[i+1\][j-1\]就是内层这段区间的最长回文子序列的长度

i j元素相同的情况很好判断, 若不相同, 则这段区间的最长回文子序列的长度为多少呢? **此时不能直接等于i + 1,  j-1, 因为i j-1  i+1 j是可能相同的, 所以直接等于这两段区间的dp值的较大值即可**

![image-20231106180400083](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106180400083.png)

填表顺序: ij可能用到左下, 下, 左, 所以整体来说, 必须从下往上, 每一行从左往右进行处理

初始化越界问题: 00 n-1n-1可能越界, 但是这是一个元素的情况, 直接特殊处理一下就不会越界了

---

**二维dp, 一维表示区间的起始, 一维表示区间的终止, 状态表示为该区间内所有的回文子序列的最大长度**

这样状态转移方程才能推出来

### [1312. 让字符串成为回文串的最少插入次数](https://leetcode.cn/problems/minimum-insertion-steps-to-make-a-string-palindrome/)

如果一维dp, dpi表示以i元素为结尾的字符串成为回文串的最少插入次数, 发现状态转移方程根本推出不来, 其实就是dp[i]和dp[i - 1]等元素很难联系起来

二维dp: i表示字符串起始, j表示字符串结尾, dp[i][j\]表示该字符串成为回文串的最少插入次数

i元素 == j元素, 若i == j 则0    i + 1 == j则0, 否则就是dp[i+1][j-1\] ( 这个比较简单, 起始就是中间字符串成为回文串, 然后两边加俩相同字符)

> i元素 != j元素, 则dp[i][j\] = dp[i + 1\][j - 1\] + 2,  其实你可以想象中间已经是回文串了, 然后两边不同, 此时咋办? 只能插入两次啊	
>
> **不对**, ij元素不同时的答案错了, 如果x aaaaaa a  x不等于a, 此时就不是中间dp值+2了, 而是+1, 这个仅限于这个情况吗???? 不知道.....但是这样总归是对的

上面两行纯在梦游, 其实和上一题基本一样

---

用到左下, 左, 下

所以初始化顺序: 下到上, 左到右   i从右到左(纵坐标下到上), j从左到右

![image-20231106184448441](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106184448441.png)



----

> 1. 回文串且子串的问题中, 典型的是二维dp把每个子串是否是回文串记录下来, 其实就是遍历所有子串, O(N^2)
>
> 2. <u>**要么就是二维dp, 一维表示子串起始, 一维表示子串的终止**</u>
>
> 3. 要么就是和其它的结合一下, 比较特殊 : 二维dp记录每个子串  +  一维dp  我记得是132题 和 单词拆分这个题很像
>
> 12常见

## 两个数组的dp问题

> 总结: 套路都一样, 二维dp, 一维代表一个数组, 另一维代表另一个数组
>
> 其实也就那两个困难题稍微困难点, 但是也就那样, 空串 || 匹配一个然后保留呗
>
> 其实道理都很简单的

### [1143. 最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/)

> hot100

状态表示 : 二维dp, dp[i][j\] 表示第一个字符串的0 - i的子串与第二个字符串的0 - j的子串的最长公共子序列的长度

状态转移方程: 

最后一个元素相等  dp = dp i-1 j-1 + 1

不相等 dp = max(dp i-1 j, dp i j-1)

用到了左上, 左, 上 所以从上往下, 从左往右

所以多一行多一列防止越界, 第一行表示第一个字符串为空串, 第一列表示第二个字符串为空串

所以都初始化为0即可  过了= =

---

dp[i][j\] 表示 第一个数组0 到 i区间 以及 第二个数组0到j区间内的最长公共子序列的长度  (注意, 这个公共子序列并不一定以最后这个ij元素为结尾)

状态转移方程:

![image-20231106204734580](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106204734580.png)

以两个数组的ij位置元素的比较情况来区分具体情况

1. ij元素相同, 此时很好理解, dp i j = dp i-1 j-1 + 1  相当于是前面的最长公共子序列 + 一个新的元素嘛
2. 若ij元素不同, 则确实就是 i j-1    &   i-1 j两个处的dp值的较大值, 就是这两个情况下, 两区间的最长公共子序列的最大值的较大值

越界与初始化顺序 : ij用到上, 左, 左上

所以, 从上往下, 从左往右进行遍历

**注意, 这里的ij之间并没有固定的大小关系, 也就是第一列也都需要赋值, 那么, 第一行第一列都有可能越界, 所以, 可以通过加一行加一列的方式来避免初始化问题**

![image-20231106205336829](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106205336829.png)

横坐标代表第一个字符串中从 0 到 i的范围, 纵坐标代表第二个字符串中从0到j的范围, 那么按理来说, 应该是i>=0 j>=0, (左闭右闭), 我们可以用多出的一行一列代表空串的情况

第一行为第一个字符串的空串时两个区间的最长公共子序列的长度, 第一列为第二个字符串为空串时两个区间的最长公共子序列的长度

---

这个题

![image-20231106210817524](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106210817524.png)

其实把这个过程, 以及二维dp表 和 这这两个字符串联系起来, 就比较好理解了

两个下标同步往后走, 遇到相同的才加一

### [1035. 不相交的线](https://leetcode.cn/problems/uncrossed-lines/)

最长公共子序列

### [115. 不同的子序列](https://leetcode.cn/problems/distinct-subsequences/)

**如果还以最长公共子序列那种二维dp来做**

状态表示 : dp[i][j\] 表示 第一个字符串的0 到 i区间的所有子序列中 等于 第二个字符串的0 到 j字符串的个数

状态转移方程: 

**0 到 j的所有子序列中, 分成两类, 一类的最后一个元素是s[j] 另一类的最后一个元素不是s[j\]    (注意, 这里说的是最后一个元素是不是, 而不是相等不相等)**

第二类: 其实就是dp[j - 1][i\]

第一类: 若t[i] 和 s[j]相同, 则贡献的个数为dp[i - 1][j - 1\]

其实, 第二类是一定有的, 因为这是过去已经求好的, 很好理解, 那么第一类的话, 如果确实条件符合, 也好理解

两类相加, 第一类需要判断

---

需要用到左上, 以及左边

所以, 从上往下, 从左往右进行初始化

![image-20231106214053842](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231106214053842.png)

多一行多一列的初始化问题:

横坐标越大, 已有字符串越大, 这样第一行就是已有字符串为空串

纵坐标越大, 目标字符串越大, 第一列就是目标字符串为空串, 所以第一列都需要初始化为1

---

**<u>上面三个的状态表示都可以视为是两个数组的dp问题的常规思路</u>**



### [97. 交错字符串](https://leetcode.cn/problems/interleaving-string/)

**依旧常规思路**

---

状态表示

dp[i][j\] 表示s1的0到i区间的子字符串与s2的0到j区间的子字符串能否拼接完成s3的0到i+j区间的子字符串

其实这里ij分别标识s1 s2两个字符串, 如果两个已有字符串可以交错拼接成功, 则交错拼接而成的字符串的长度是已知的

状态转移方程:

![image-20231107190639608](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231107190639608.png)

这个其实并不难

初始化问题: 用到上和左, 所以, 从上往下, 从左往右进行填表

第一行第一列可能会越界, 所以加一行加一列, 分别标识s1为空串以及s2为空串的情况

```C++
        for(int i = 1; i <= m; ++i) {
            for(int j = 1; j <= n; ++j) {
                // i-1 j-1  i-1+1 + j-1+1
                int len = i - 1 + 1 + j - 1 + 1;
                int pos = len - 1;  // s3对应的下标
                dp[i][j] = (s1[i - 1] == s3[pos] && dp[i - 1][j])
                        || (s2[j - 1] == s3[pos] && dp[i][j - 1]);
            }
        }
这个对ok
    for(int i = 1; i <= m; ++i) {
            for(int j = 1; j <= n; ++j) {
                // i-1 j-1  i-1+1 + j-1+1
                int len = i - 1 + 1 + j - 1 + 1;
                int pos = len - 1;  // s3对应的下标
                if(s1[i - 1] == s3[pos]) dp[i][j] = dp[i - 1][j];
                else if(s2[j - 1] == s3[pos]) dp[i][j] = dp[i][j - 1];
            }
        }
为什么这个不对????
```

这个判断逻辑真的有问题, 还是要谨慎点

### [712. 两个字符串的最小ASCII删除和](https://leetcode.cn/problems/minimum-ascii-delete-sum-for-two-strings/)

**状态表示: dp i j 表示 s1的0到i区间 与 s2的0到j的区间使相等所需的最小ASCII删除和**   (常规)

状态转移方程:

若 i j 元素相等, 则dp i j = dp i - 1 j - 1

若 i j 元素不相等, 则 min( i 元素ASCII + dp i - 1 j     j元素ASCII + dp i j-1)  其实就是删i元素, 或者删j元素, 使剩下两个子串相等

用到左上, 左 上, 所以从上往下, 从左往右

多一行多一列

第一行表示s1为空串 第一列表示s2为空串

### [718. 最长重复子数组](https://leetcode.cn/problems/maximum-length-of-repeated-subarray/)

成功了但没完全成功

1. 首先这个题的状态表示不能是   s1 0到i的所有子数组与s2 0到j的所有子数组的最长重复子数组的长度了
   因为很简单, 子数组必须连续, 求dpij时 这两个元素必须和前面的子数组相连续, 如果不连续, 就有问题了, 这个我考虑到了
2. **正确的状态表示: dp i j 表示s1以i元素为结尾的所有子数组 和 s2以j元素为结尾的所有子数组 中最长重复子数组的长度**
3. 问题出在了状态转移方程中, 如果ij元素相同, 那状态转移方程很好求
4. 如果ij元素不同呢?  `else dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);`   还是  `else dp[i][j] = 0;`  ?
   其实正确的应该是第二种, 因为如果ij元素不同, **<u>则回顾状态表示</u>: dp ij 存储的必须是s1以i元素结尾的子数组与s2以j元素结尾的子数组 中最长重复子数组的长度, 也就是结果的末尾元素必须是i元素  以及 j元素, 所以如果ij元素不同, 此时直接存储0就行了**
5. 返回值肯定就是dp表里的最大值了

![image-20231108122651703](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231108122651703.png)

**子数组必须连续**

### [72. 编辑距离](https://leetcode.cn/problems/edit-distance/)

> hot100

状态表示: dp i j 表示第一个单词的0 到 i区间 转换为 第二个单词0 到 j区间所需的最小操作数

状态转移方程:

1. i == j dp i j = dp i-1 j-1
2. i != j
   替换: dp i-1 j-1    + 1
   删除: dp i-1 j    + 1
   插入: dp i j-1    + 1 **(这个最先没想到...)**

用到左上, 左, 上

多一行多一列: 第一行表示word1为空串(目标字符串)  第一列表示words2为空串(源字符串)

## 两个数组的dp问题 - 空串||匹配一个然后保留

### [44. 通配符匹配](https://leetcode.cn/problems/wildcard-matching/)

> **依旧是两个数组的dp, 和之前的一样, 二维dp表, 一个坐标代表一个数组**

用p字符串去匹配s字符串

状态表示: dp i j 表示p字符串的0到i区间的字符串能否匹配s字符串的0到j区间内的字符串

所以, 如果以横坐标表示i, 纵坐标表示j, 则i越大, 越往下, 已有字符串越多, 越往右, 目标字符串越多

状态转移方程: 依旧是以ij位置的字符来具体讨论分析

1.  若i位置字符为普通字符(注意, j位置字符一定为普通字符), 
   若ij位置元素相同, 则dp ij  = dp i-1 j-1
   若不同, 则无法匹配
2. 若i位置为?
   则, dp ij  = dp i-1 j-1,  且这里不需要ij位置元素相同, 就是因为?元素的特性~
3. 若i位置为*
   则, 其实i位置*元素可以匹配s字符串的从末尾开始的任意长度的字符串
   所以, dp ij = dp i-1 j || dp i-1j-1 || dp i-1 j-2 || ... || dp i-1 0 || dp i-1 -1
   其实简单来说就是这个\*匹配一个空字符串还是一个字符还是两个还是三个还是... 还是目前为止全部的t(此时就是0 到i-1要匹配空串了, 也就是全部都为\*)

**其实整体来说也不难, 12很好分析, 3也好分析, 但是3的时间复杂度又是N, 整体就是N^3**

**这里的关键是第三种情况可以进行优化, 而数学法的优化比较容易理解**

![image-20231107184140068](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231107184140068.png)

而另一种方法的优化是:

![image-20231107184615775](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231107184615775.png)

> 这个匹配一个但是不舍去的情况是比较难理解的
>
> 也就是*匹配一个, 但是不舍去, 尝试匹配下一个?

**我理解你妈, 记住这里是空串  || 匹配一个(然后保留) 就行了**

**要么匹配空串, 要么匹配一个!!**

---

初始化问题: 左上, 上一排的左边全部

所以从上往下

多一行多一列

此时第一列表示目标字符串为为空串(已有字符串逐渐增加), 第一行为已有字符串为空串(只有第一个为true)

所以第一列, 第一个肯定为true, 因为空可以匹配空, 但是后面需要判断是否全为*

---

**整体来说, 也不复杂, 这里也就是常规的两个数组dp的状态表示, 只是这里的优化可能不是很好想, 并且, 防止越界的初始化问题也不复杂其实....**

### [10. 正则表达式匹配](https://leetcode.cn/problems/regular-expression-matching/)

空串  || 匹配一个然后保留

记住就行了

---

依旧是用p去匹配s   注意, 这里的x*是以整体的形式来看待的, 也就是x\*可以匹配任意个x, 而不是这个\*可以匹配任意个x

状态表示:

**dp i j 表示p字符串的0到i范围的子串能否匹配s的0到j范围的子串**    (依旧两个数组dp常规思路)

状态转移方程

1. 若i位置元素不是.不是*, 则若ij元素相同, 则dp ij = dp i-1 j-1(因为i元素必须匹配一个)
2. 若i元素是.  则dpij = dpi-1j-1
3. 若i元素是*, 判断i-1是. 还是普通字符

![image-20231204204155640](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231204204155640.png)

![image-20231204205350990](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231204205350990.png)

初始化问题:

左上,  上, 左 所以从上往下, 从左往右

多一行, 多一列:

第一行表示已有字符串为空串, 目标字符串逐渐增加

第一列表示目标字符串为空串, 已有字符串逐渐增加   .\*.\*.*  这样的才可以



----

## 背包问题

> **真 · 关键点:**
>
> **01背包: `dp[i][j] = 不选: dp[i - 1][j] 选: dp[i - 1][j - v[i]] + w[i]`**
>
> **完全背包: `dp[i][j] = 不选: dp[i - 1][j] 选: dp[i][j - v[i]] + w[i]`**
>
> **具体加不加w[i], 也就是第i个元素的价值要看具体问题, 且选和不选是取max min 还是相加, 都要看具体问题**
>
> **这样记忆: 01背包相比于完全背包简单一点, 所以选和不选之间的差别就小一些, 这样才更容易记忆嘛**

### 01背包 - 真

若干个物品, 一个背包, 背包有容量上限, 物品有价值 + 体积, 问怎么选择物品可以获取最大价值, 这里分为两个情况, 1. 背包必须装满, 2. 背包不必装满

01背包就是每个物品只有一个, 完全背包就是每个物品有无数个, 可以任意挑选多少个

状态表示: 如果dp[i] 表示到i元素为止, 所有选法的最大价值, 是不行的, 因为这里根本没有涉及到体积这个因素, **体积才是关键因素**, 否则的话就是每个元素都要选喽

**正确的状态表示: 二维, 一维是物品  一维是体积**

**dp[i][j\] 表示 从前i个物品中挑选, 体积不超过j的所有选法中的最大价值**

也就是说, 到了i物品时, 比如背包体积是50, 则j最大就是50, 会记录到i元素时, 体积不超过1 2 3 4 5... 47 48 49 50的多种选法里面的最大价值

状态转移方程:

i物品, 要么选, 要么不选, 此时还需要结果的体积不能超过j

![image-20231108154156809](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231108154156809.png)

**也就是说, 到了每个元素的每个体积情况都需要考虑**

> **我发现状态表示是真的需要透彻理解, 因为它是状态转移方程的基础**

---

如果是完全背包: 其实和上面的差别不是很大

**状态表示: dp i j 表示到i物品为止, 所有选法中, 体积恰好等于j的选法的最大价值**

此时, dp i j 可能没有选法, 也就是无法恰好凑成j体积, 则记作-1

状态转移方程:

每个dp i j, 分两个情况, i元素选 / 不选

不选 i 元素, 则dp i j = dp i - 1 j 也就是i-1个元素的所有选法体积等于j的最大价值, 如果是-1, 则dp ij 也是-1

选 i 元素, 则dp i j = dp i-1 j-v[i]  其实就是i-1元素为止的所有选法中体积等于( j - i元素体积 )的最大价值, 也很好理解... 就是不好写...



还有就是第一行第一列的初始化问题, 也好理解, 略了

#### [416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/)

> hot100

二刷: 也就是, 选出子序列, 使和为x

其实也就是每个元素选/不选, 可以理解为背包体积必须装满, 且价值已知(等于体积啦), 其实这里没必要牵扯到价格, 因为我可以是前i个元素中选择, 体积等于j是否可以做到?

状态表示: dp[i][j]表示从前i个元素中选, 使其体积等于j的选法是否存在

dp[i][j\] 不选 / 选

max(dp i-1 j, dp i-1 j-nums[i])

只用到上一行, 所以整体从上往下进行处理

多一行多一列, 没有元素, 凑的目标和为0?

第一行没有元素, 第一列目标和为0?

---



记总和为sum  其实就是选出一个子集, 和为sum / 2

所以, 其实就是, N个物品, 每个只有一个, 价值已知, 背包有容量限制, 必须装满, 是否可以?

> 注意, 这里其实是子序列, 不是子数组

状态表示: dp i j 表示到i元素为止 所有选择中, 体积恰好等于j的选法是否存在

> 横坐标: i 元素  纵坐标 : j 价值

状态转移方程:  i元素 选 / 不选

选 : i-1 选出j - value[i] 是否为true  dp i-1 j-value[i] 

不选: i-1选出j是否为true  dp i-1 j

用到上, 所以多一行多一列, 且从上往下

第一行, 没有元素   第一列, 价值为0

![image-20231108184549952](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231108184549952.png)

注意, 有元素/没元素, 不选就是0, 所以第一列都是true

---

过了, 纯背包问题...

每个元素选 / 不选  且必须填满背包, 没有价值规定

```C++
        for(int i = 1; i < n + 1; ++i) {
            for(int j = 1; j < sum + 1; ++j) {
                dp[i][j] = dp[i - 1][j];  // 不选
                if(dp[i][j]) continue;
                if(j - nums[i - 1] >= 0) dp[i][j] = dp[i - 1][j - nums[i - 1]];  // 选, 从i-1里面选一个目标和
            }
        }
```

#### [494. 目标和](https://leetcode.cn/problems/target-sum/) (target+sum) / 2

![image-20231108192155952](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231108192155952.png)

> 这他妈我能想到?

这样就是01背包问题了, 若干物品, 价值>=0, 背包必须填满, 不需要记录最大价值, 需要记录填满的选法的个数

**dp i j 在0, i元素区间中, 所有选法的空间大小等于j的选法的<u>个数</u>**

状态转移方程: 

i元素 选 / 不选来具体分类, 很简单

多一行: 没有元素, 

多一列: 目标和为0, 但是因为nums[i]可能为0, 所以这里还需要计算

![image-20231108200247035](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231108200247035.png)

**所以, 第一列的剩余元素不需要初始化, 可以和11以后的一起初始化, 因为不会越界的**

那 如果初始化呢? 比如3个0, 和为0的选法有几种, ...有点难算

---

> 注意事项:  其实就是典型的01背包问题
>
> 1. 怎么把原始的问题转换为01背包, 最开始的数学证明有点麻烦, 且很难想到
> 2. 第一列的初始化问题

```C++
        for(int i = 1; i <= m; ++i) {
            for(int j = 0; j <= n; ++j) {
                dp[i][j] = dp[i - 1][j];  // 不选
                if(j - nums[i - 1] >= 0) dp[i][j] += dp[i - 1][j - nums[i - 1]];
            }
        }
```

#### [1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii/) sum/2

![image-20231108203716333](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231108203716333.png)

![image-20231108202404022](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231108202404022.png)

> 这尼玛我能想到怎么转换到这个的????

![image-20231108202542617](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231108202542617.png)

首先, 不必纠结于差值是正还是负, 因为差值永远可以是>=0的

那么, 也就是所有的数加减之后一个结果, 这个结果需要是最小的, 所以就转换为我们需要找出若干数的和, 这个和最接近与sum / 2, 如果确实等于, 则最后就是0呗, 如果是sum / 2 - 1, 则最后差值就是2呗

**所以就转换为了**

**有若干物品, 背包容量已知(sum/2), 可以不装满, 此时物品的价值和体积都是已知的(且相等), 现在要求物品价值的最大值(同时容量也会逼近于最大)**

> 5 就是23,  4就是22, 所以直接sum/2即可

纯01背包

状态表示: dp[i][j\] 表示到i元素为止, 所有选法的体积<=j时, 所选的最大价值

状态转移方程:

i元素选 / 不选

两者求较大值即可

第一行: 没有元素, 第一列: 和为0

```C++
        for(int i = 1; i <= m; ++i) {
            for(int j = 1; j <= n; ++j) {
                dp[i][j] = dp[i - 1][j];  // 不选
                if(j - stones[i - 1] >= 0)
                    dp[i][j] = max(dp[i][j], dp[i - 1][j - stones[i - 1]] + stones[i - 1]);
            }
        }
```

其实最后这个判断多余, 因为sum=5时, dp[m][n\]最大也是2, 不会是3

---

虽说传统的01背包问题的状态表示是背包装满/不装满时的所有物品的最大价值, 但是这个只是个模板, 实际上还要看具体的问题, 比如上面三个, 第一个是能否装满? 第二个是装满的选法的个数, 第三个是装满时的最大价值(传统的), 所以01背包主要就是元素只有一个, 体积价值已知(没有价值也行), 然后装满或者不用装满时的各种情况的统计/判断

### 完全背包 - 纯完全背包

关键: 状态转移方程: 第i个元素选0 1 2 3 4 5... 选0个的状态转移方程很简单, 1 2 3 4 5 可以合并

---

01背包: 背包容量V, 若干物品, 有每个物品的价值和体积, **每个物品只有一个, 所以对于每个物品来说, 只有选 / 不选**

具体可以分为两个问题: 背包不必装满的最大价值, 背包必须装满的最大价值

完全背包: 背包容量V, 若干物品, 有每个物品的价值和体积, **每个物品有无限个, 对于每个物品来说, 可以选0, 1, 2, 3...个**

具体可以分为两个问题: 背包不必装满的最大价值, 背包必须装满的最大价值

---

1. 先看背包不必装满的场景

状态表示: dp [i][j\] 表示前i个物品/元素中选择, 所有选法中, 体积不超过j的最大价值

状态转移方程: 

![image-20231109140658477](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109140658477.png)

这个说实话很好理解... 就是选1.2.3...需要循环, 又是一个O(N), 如何用有限的状态替换呢?

**其实就是选1个的时候的i-1换成i就行了**

![image-20231109140853297](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109140853297.png)

**最终就是下面的这个, dp i-1 j代表第i个元素不选的情况, 后面那个是选1.2.3.....个的最大值, 需要判断j - v[i]是否>=0, 若不是, 则该状态不存在**

其实中间无非就是数学转换, 我们需要记住这个表达式....

`dp[i][j] = max(dp[i - 1][j], dp[i][j - v[i]] + w[i]`  i和j各自变一下呗

2. 再看背包必须装满的场景

状态表示: dp [i][j\] 表示前i个物品/元素中选择, 所有选法中, 体积等于j的**最大价值**

状态转移方程:

![image-20231109141058199](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109141058199.png)

<u>这里其实和上面的情况很像, 但是.. 因为这里的限制条件是必须装满, 所以, 若装不满, 我们可以规定dp值为-1, 所以这里不仅要判断j - v[i]>=0, 还要判断dp值是否等于-1, 因为-1 + w[i]可能大于dp[i-1][j\], 且不选的情况也有可能是为-1的, 所以需要多几个判断</u>



---

初始化问题:

![image-20231109141439208](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109141439208.png)

紫色是不必装满, 绿色是必须装满

且第一列的其他元素不需要初始化

![image-20231109141613865](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109141613865.png)

返回值和填表顺序

#### [322. 零钱兑换](https://leetcode.cn/problems/coin-change/)

> hot100

> 二刷 : 背包容量已知, 必须装满, 每个物品有无限的, 不要求最高价值, 而是选的物品最少

`dp[i][j]` 第i个元素选多少个, 最终其实就是那个状态表示`dp[i][j] = max(dp[i - 1][j], dp[i][j - v[i]] + w[i]`

-1表示无法选出, 若不为-1则为最少个数

其实这里最关键的是 **如何从最初的最高价值的状态转移方程转化为求最少物品数量的状态转移方程**

`dp[i][j] = max(dp[i - 1][j], dp[i][j - v[i]] + w[i]` dp值肯定是最少个数, 可是第二个表达式如何转换?

`dp[i][j] = min(dp[i - 1][j], dp[i][j - v[i]] + 1)`

第一: `j - v[i]`是否合法, 第二点, 两个dp值是否为-1, 若是-1则第二个直接无效, 不用加1

**所以, 其实就是最典型的完全背包问题罢了**

---

若干物品, 体积和价值相等, 必须装满, 每个物品有无限个, 这里不需要求装满时的最大价值, 而是要求装满时所使用的物品是最少的, 求最小数量

状态表示:

dp[i][j\] 标识从前i个元素中选择,  体积恰好等于j时所需的物品的最小个数

状态转移方程:

参考... 上方...

```C++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int m = coins.size(), n = amount;
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, -1));  // -1表示没有
        // 只初始化第一行即可, 没有元素, 体积等于0 1 2...
        dp[0][0] = 0;
        for(int i = 1; i <= m; ++i) {
            for(int j = 0; j <= n; ++j) {
                dp[i][j] = dp[i - 1][j];  // 不选
                if(j - coins[i - 1] >= 0 && dp[i][j - coins[i - 1]] != -1) {
                    if(dp[i][j] == -1) dp[i][j] = dp[i][j - coins[i - 1]] + 1;
                    else dp[i][j] = min(dp[i][j], dp[i][j - coins[i - 1]] + 1);
                }
            }
        }
        return dp[m][n];
    }
};
```

把模板理解透彻了就是这么简单.....~~~

**有略微差别, 模板的dp值是最大价值, 而这里是最少的使用物品的数量**

若不选,  dp = dp[i - 1][j\]   这个毋庸置疑

若选呢? 选1个需要多少, 2个多少, 3个多少, 然后若干状态的最小值

之前是dp[i\][j - v[i\]] + w[i], 这个代表着若干的状态, 而现在其实就是dp[i][j - v[i\]\] + 1

并且是选 / 不选里面求较小值, 也就是min, 而不是max

![image-20231109154955120](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109154955120.png)

明白了吗????个数!!!!!

> ![image-20231109155314922](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109155314922.png)
>
> 其实-1也可以, 多判断一下而已

#### [279. 完全平方数](https://leetcode.cn/problems/perfect-squares/)

> 不能说完全一样, 只能说一模一样...

物品若干, 体积和价值相等, 背包容量已知, 必须装满, 不求装满时的最大价值, 而是最少的使用物品的数量... (这他妈和上一题有什么区别?)

> 归根结底, 它们的共同点就是若干物品, 选出来放入背包, 必须装满, 此时最少的物品数量是多少
>
> 这样找见共同点, 再归纳总结就太棒了, 这样可以做到解决一个题, 就可以解决类似的三个题

> dp i j-v[i]  + value[i]      这个得记住, 也就是选1 2 3..... 若干个值的归纳值
>
> 先判断下标是否合理, 其次是如果是装满的话, 可能值是-1, 需要判断

![image-20231109160127614](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109160127614.png)

#### [518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-ii/)

物品若干, 价值和体积相等, 每个物品都有无限个, 也就是不是01背包, 而是完全背包. 背包容量已知, 必须装满, **这里不是求最大价值, 也不是求最少的使用物品的数量, 而是装满时的一共有多少种组合**

状态表示: dp[i][j\] 表示在前i个元素中选择, 恰好体积为j时, 一共有多少种选法

---

其他都无所谓  但是.. 不选的时候, 很简单, 选1 2 3 4 5....到底状态转移方程是什么?

比如, 第i个元素选1个, 则i-1个里面需要选够 `j - v[i]` 的体积, 那么, 如果 `dp[i-1][j - v[i]]` 不是0, 也就是有若干个选法, 则其实就是每个选法最后再加一个i元素, 所以总的选法个数不变, 所以, 选一个时, `dp[i][j] = dp[i - 1][j - v[i]]` 所以总的状态转移方程就是
`dp[i][j] = dp[i - 1][j] + dp[i][j - v[i]]`  (两个可能都是0)

> **完全背包的模板那里, 是求最大价值, 也就是i元素选若干个, 是要加上i元素的价值的**
>
> **而这里是要求选法的个数, 如果i元素选3个(举例), 那么i-1要选出剩余的空间, 那么, dp[i-1][j - v[i\]\]存储的其实是选法个数, 每个选法最后再选3个i元素, 最终选法个数没变, 所以针对选3个, 是不加w[i\](i元素的价值)的, 所以, 针对选若干个, 其实最终都没有这个附加项** 

----

稍微一分析就过了, 所以这里到底是怎么状态转移, 还要从最开始的那个模板开始进行推导

```C++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int m = coins.size(), n = amount;
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));  // 0表示没有任何组合可选
        // 第一行: 没有元素, 体积为0.1.2.3....
        dp[0][0] = 1;  // 必须是1
        for(int i = 1; i <= m; ++i) {
            for(int j = 0; j <= n; ++j) {
                // 选/不选
                dp[i][j] += dp[i - 1][j];  // i元素不选, 前i-1个元素选出j
                if(j - coins[i  -1] >= 0 && dp[i][j - coins[i - 1]] != 0) {  // 第二个条件可有可无
                    dp[i][j] += dp[i][j - coins[i - 1]];
                }
            }
        }
        return dp[m][n];
    }
};
```

注意这里, 没有元素/物品, 要凑成体积为0, 此时的选法有几个? 其实只能不选, 所以dp[0][0\] 要初始化为1!!!!!!

![image-20231109155720708](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109155720708.png)

### 二维费用的背包问题 - 纯二维费用背包

#### [474. 一和零](https://leetcode.cn/problems/ones-and-zeroes/)

若背包有两个限制, 那么就是二维费用的背包问题

之前只有体积限制, 也就是元素的总体积必须<=背包容量 或者 必须等于背包容量

而这里就是两个限制了

同样分为   二维费用的01背包问题 / 二维费用的完全背包问题

这个题是选 / 不选, 所以具体来说是二维费用的01背包问题

----

怎么解决?

> 完全背包, 二维费用背包 都是以01背包为基础的

01背包状态表示: dp[i][j\] 表示从前i个元素中选, 总体积不超过j/恰好等于j, 此时所有选法中的最大价值

二维费用背包状态表示: dp[i][j\][k\] 表示从前i个元素中选, 总体积不超过j, 总重量不超过k的所有选法中的最大价值

那么, 针对这个题就是: dp[i][j\][k\] 表示从前i个元素中选, 0的个数不超过j, 1的个数不超过k的所有选法中的最大选择的元素的个数

---

状态转移方程:

第i个选 / 不选

不选: dp i-1 j k

选: dp i-1 (j - n1) (k - n2) + 1  同时判断j - n1>=0 k - n2>=0

![image-20231109170411482](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109170411482.png)

**总结: 没区别, 多一个条件, 多一个维度**

但是, 初始化问题呢?

**依旧是, jk不会越界, 所以只需要处理i为0的时候的情况即可  (其实之前的二维dp表也是, i等于0那一行处理即可)**

i等于0, 没有元素, 问满足0的个数不大于0 1 2 3 4 5 1的个数不大于0 1 2 3 4 5的选择元素的最大值????那肯定是0

```C++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int n, int p) {   // n0 p1
        int m = strs.size();
        vector<vector<vector<int>>> dp(m + 1, vector<vector<int>>(n + 1, vector<int>(p + 1, 0)));
        // 初始化i=0时, 都初始化为0即可
        for(int i = 1; i <= m; ++i) {
            for(int j = 0; j <= n; ++j) {
                for(int k = 0; k <= p; ++k) {
                    // 第i个选或者不选呗
                    dp[i][j][k] = dp[i - 1][j][k];  // 不选
                    string &s = strs[i - 1];
                    int a = 0, b = 0;  // a0 b1
                    for(auto & i : s) if(i == '0') a++; else b++;
                    if(n - a >= 0 && p - b >= 0) dp[i][j][k] = max(dp[i][j][k], dp[i - 1][n - a][p - b] + 1);
                }
            }
        }
        return dp[m][n][p];
    }
};
```

问题

1. 其实在第一层for进入时, 就可以求这个字符串的10数量了 之后两层的循环中针对的都是一个字符串
2. **最大的最致命的问题: 在最内层循环内部, 指的是求dp值, dp值是前i个元素中选择, 0的个数不超过j, 1的个数不超过k**
   **所以最后一个判断应该是, j - a >= 0 && k - b >= 0, 内部是用不到n, 和p的, 只有当最后一次循环时, jk才会等于np**

```C++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int n, int p) {   // n0 p1
        int m = strs.size();
        vector<vector<vector<int>>> dp(m + 1, vector<vector<int>>(n + 1, vector<int>(p + 1, 0)));
        // 初始化i=0时, 都初始化为0即可
        for(int i = 1; i <= m; ++i) {
            string &s = strs[i - 1];
            int a = 0, b = 0;  // a0 b1
            for(auto & i : s) if(i == '0') a++; else b++;
            for(int j = 0; j <= n; ++j) {
                for(int k = 0; k <= p; ++k) {
                    // 第i个选或者不选呗
                    dp[i][j][k] = dp[i - 1][j][k];  // 不选
                    if(j - a >= 0 && k - b >= 0) dp[i][j][k] = max(dp[i][j][k], dp[i - 1][j - a][k - b] + 1);
                }
            }
        }
        return dp[m][n][p];
    }
};
```

> **其实背包问题的核心特征还是:**
>
> **若干东西/物品/元素/数值, 基本都是选/不选, 而具体根据只能选一个和选无限个, 可以分为01背包和完全背包**
>
> **又有限制条件, 比如背包容量, 具体到每个题中, 限制条件的具体展现形式又都不一样**
>
> **如果有两个限制条件, 就是二维费用的背包问题了**
>
> **核心还是选/不选**

#### [879. 盈利计划](https://leetcode.cn/problems/profitable-schemes/)

> 题意:
>
> 若干员工, 有若干工作, 每个工作产生的利润以及需要的员工数量是已知的, 每个员工只能参与其中一种工作
>
> 关键是这个minProfit, 也就是需要选出这些工作的一部分子集, 它们产生的利润>=minProfit
>
> 当然需要员工不超过啦

---

所以, 物品就是工作, 选/不选, 01背包, 限制条件: 利润>=minProfit, 同时员工数量需要足够也就是<=n

> 有点不一样的是, 这里的一个限制条件是>=, 而不是之前的<= 或者=, 但是我感觉都是一个道理

---

状态表示:

dp i j k 表示在前i个工作中选择, 所有选法中, 利润>=j 且员工数量<=k的**选法的个数**

状态转移方程:

根据第i个工作选 / 不选

不选: 很简单

选: 所需剩余利润变小, 员工变少

![image-20231206151119417](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231206151119417.png)

注意点: 

1. 员工方面, n - 第i个工作所需员工数之后<0, 这个要处理, 说明员工根本不够选第i个工作

2. 那, 利润呢? profit - 第i工作的利润 <0, 说明第i个工作就足够产生目标利润了, i-1之前的工作选出利润>=0即可

初始化问题:

依旧是只需要处理, i=0 也就是没有工作的时候的那些dp值

产生的利润一定为0, 所需的员工数一定为0, 要求选法

所以, i=0, 利润为0, 员工随意, 都为1, 表示一种选法, 其余的所有都是0, 因为利润不达标

### 似包非包

似包非包不是说半像包, 而是看起来是背包问题, 实际不是背包问题

#### [377. 组合总和 Ⅳ](https://leetcode.cn/problems/combination-sum-iv/)

![image-20231109184923748](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109184923748.png)

严格来说, 背包问题解决是, **组合问题**, 也就是选/不选

这个题严格来说/本质来说, 是一个**排列问题**

所以不能用完全背包来解= =

---

![image-20231109192425268](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109192425268.png)

![image-20231109192758329](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231109192758329.png)

核心思路: 就拿第一个位置来说, abcd任何一个数组中的元素都可以, 若某一个元素, 就是求凑成target - x一共有多少种方法

### 卡特兰数

#### [96. 不同的二叉搜索树](https://leetcode.cn/problems/unique-binary-search-trees/)

> 左子树<根节点, 右子树>根节点
>
> 我怎么感觉要二维dp, 范围dp, 也就是由i到j区间的结点组成的二叉搜索树的个数

状态表示: dp[i][j\] 表示由从i到j的结点组成的二叉搜索树的个数

状态转移方程: ... 略

比如 dp 1 5 用到了 dp 11 12  13 14

25 35 45 55

用到了左边, 和上面

所以从上往下, 从左往右

第一行: 从0到0 从0到1

```C++
class Solution {
public:
    int numTrees(int n) {
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0)); // 下标从0到n
        for(int i = 1; i <= n; ++i) {
            for(int j = i; j <= n; ++j) {
                // dp[i][j] 表示从i到j的结点构成二叉搜索树的个数
                if(i == j) dp[i][j] = 1;
                else {
                    int sum = 0;
                    for(int k = i; k <= j; ++k) {
                        // k做根节点  比如求dp[1][5]  3做根节点
                        if(k == i) sum += dp[k + 1][j];
                        else if(k == j) sum += dp[i][k - 1];
                        else sum += dp[i][k - 1] * dp[k + 1][j];
                    }
                }
            }
        }
        return dp[1][n];
    }
};
```

不行啊妈的, 第一行第一列没法初始化

----

![image-20231109201754634](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109201754634.png)

这类问题: 难想出, 但是想出之后就很容易, 总之很巧

这里并没有说到底是根节点是几, dp[i]没有说根节点具体是几, 而是整棵树的结点的个数, 真的很巧

比如总共为5个, 根节点是3, 左子树12 右子树45, **但是其实12 45都是两个结点组成的BST的种数**

如果根节点是4, 左子树3个, 右子树1个

根节点是5, 左子树4个, 就是4个结点构成的BST的种类数

![image-20231109203002933](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231109203002933.png)

**这个核心在于, 123  和 567组成的BST的种类数其实是一样的!!!!!!!!!!!!!!**

**只要是N个连续的结点组成的BST的种类数就是一样的,  比如1234 6789**

**只需要记录这棵树有几个结点就可以了, 默认它们的结点值是连续的**



## 不确定

### [650. 只有两个键的键盘](https://leetcode.cn/problems/2-keys-keyboard/)

状态表示: dp[i]表示获取i个A的最少操作次数

> 纯纯的小丑妈的, 好好想想, 认真读题行吗????

状态转移方程: 6个: 复制3, 粘贴一次, 复制3, 再粘贴一次, +4

7个: 34, 复制3, 粘贴一次, 复制4, 粘贴一次, 也就是+4,

这一定是最优解吗? 比如, 复制1粘贴一次, 复制6粘贴一次, 是否会更小呢?

maybe

# 技巧

### [136. 只出现一次的数字](https://leetcode.cn/problems/single-number/)

按位与 ^=   5^5 = 0   n^n = 0

### [169. 多数元素](https://leetcode.cn/problems/majority-element/)

摩尔投票法

也就是一一抵消, 最终留下的元素就是这个个数 > n / 2的元素

### [287. 寻找重复数](https://leetcode.cn/problems/find-the-duplicate-number/)

包含N+1个数, 下标就是0-N, 值存储的是1-N, 所以nums[i]一定不会越界

所以, 每个nums[i]的值当作结点的值, 它的next指向就是值对应的数组下标对应的元素

![image-20231110211056868](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231110211056868.png)

有环链表找环的入口: 快慢指针 快走两步, 慢走一步, 相遇, 然后快归到原处, 慢一步, 快一步, 这次的相遇点就是环的入口

这里其实是, 若干结点, 第一个结点的值就是1, 指向1下标处3, 3指向2 2指向4, 4指向2, 2指向4

每次快慢指针的值应该是1-4, 也就是1-N里面的值, 最终就会成环

### [75. 颜色分类](https://leetcode.cn/problems/sort-colors/)

两次扫描:

第一次把0交换归为, 第二次把1交换归位

一次扫描:

荷兰国旗?

l是0, m是1, h是2

```C++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int l = 0, m = 0, h = nums.size() - 1;
        while(m <= h) {
            if(nums[m] == 1) {
            } else if(nums[m] == 0) {
                swap(nums[m], nums[l]);
                l++;
                if(nums[m] == 2) swap(nums[m], nums[h]), h--;
            } else {
                swap(nums[m], nums[h]);
                h--;
                if(nums[m] == 0) swap(nums[m], nums[l]), l++;
            }
            m++;
        }
    }
};
```

### [31. 下一个排列](https://leetcode.cn/problems/next-permutation/)

逆序找第一个 nums[i] < nums[i+1]的这个i元素  比如 476532, 4的下标就是i

i右边一定是降序的, 找出大于nums[i]里面最小的那个, 这里就是5

交换45, 就是576432, 然后reversei后面的区间, 就是523457这个就是结果

如果一直没有找到i, 说明整个数组是单调递减的, 比如   99877654

这样的话, 本身nums就是字典序最大的, 那么下一个排列就是整体reverse, 也就是字典序最小的

```C++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        for(int i = nums.size() - 1; i >= 0; --i) {
            if(i != nums.size() - 1 && nums[i] < nums[i + 1]) {
                // 此时找i后面比它大的最小的数
                int j = i + 1;
                while(j != nums.size() - 1 && nums[j + 1] > nums[i]) {
                    j++;
                }
                swap(nums[i], nums[j]);
                reverse(nums.begin() + i + 1, nums.end());
                return ;
            }
        }
        reverse(nums.begin(), nums.end());
        return ;
    }
};
```

# 回溯(递归+搜索)

递归 > 搜索 > 回溯

前言:

![image-20231111150330816](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231111150330816.png)

**这两点很有意思, 23点极其重要, 我已经有点领悟到了**

![image-20231111151203968](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231111151203968.png)

NB

![image-20231111151654258](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231111151654258.png)

![image-20231111152024153](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231111152024153.png)

![image-20231111152745531](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231111152745531.png)

![image-20231111153530628](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231111153530628.png)

## 递归

其实核心还是在于, 一整个大问题, 分为若干步, 而每一步的解决都是一样的, 这就是重复子问题

而这个递归函数, 就可以解决这个重复子问题

这个过程到什么时候会终止并结束递归? 就是递归的终止条件了

### [面试题 08.06. 汉诺塔问题](https://leetcode.cn/problems/hanota-lcci/)

重复子问题: 每个递归都要解决一个子问题

主要就是, n-1个在a上的, 借助c, 转移到b, 然后把最后这个转移到c, 再把b上的n-1个借助a转移到c   这一整套下来, 最终目标就达成了

而n-1个要想全部移动到另一个柱子上, 其实也是这个过程, 这就是重复子问题: **将某些盘子, 借助某柱子, 移动到另一个柱子上**

这个就是重复子问题, 我们要相信自己写的递归函数可以完成这个任务

而递归的终止条件就是当只有一个盘子时, 不再需要执行上方子问题, 而是可以直接转移

### [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

相信这个函数, 传入两个有序链表的头结点, 它就可以返回合并之后的新的头结点

### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

先发现重复子问题是什么...

这个子问题决定了递归函数的函数头

而解决这个子问题决定了递归函数的函数体

> **相信这个函数, 可以做到传入一个链表的头结点, 返回逆置后的新的头结点**

![image-20231111175000202](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231111175000202.png)

![image-20231111175014076](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231111175014076.png)

一个全新的视角: 把链表看作是一个树!!!!!

### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

子问题: 先把后序的链表进行处理, 然后前两个进行逆置, 返回即可

每个递归都是这样, 终止条件就是空结点或一个结点, 就终止

> **相信这个函数, 你传入一个链表的头结点, 他就可以返回处理之后的新的头结点**
>
> NB

### [50. Pow(x, n)](https://leetcode.cn/problems/powx-n/)

**相信这个函数可以返回x的n次幂**

![image-20231111182718603](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231111182718603.png)

![image-20231111183534433](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231111183534433.png)

## 二叉树的深度优先搜索(深度优先遍历)

### [2331. 计算布尔二叉树的值](https://leetcode.cn/problems/evaluate-boolean-binary-tree/)

> 深搜就是深度优先遍历时的目标是搜索

宏观的视角来看, 我们相信, dfs这个函数传给它一个根节点, 它就可以计算某树的值, 所以, 在求root的时候, 先计算出左右子树的值, 才能计算出根节点的值. 也就是把dfs看作一个黑盒, 并相信它可以完成这个任务

---

对于原始的思路, 也就是从过程 / 细节的角度来说: 必须先知道左右子树的值, 才能算根节点的值, 所以一定是从下往上的, 所以就是后序遍历

### [129. 求根节点到叶节点数字之和](https://leetcode.cn/problems/sum-root-to-leaf-numbers/)

之前的视角: 前序遍历, 每过一个结点就在vector里面记录一下, 到了叶子节点再最终计算值, 加到全局的一个ret中, 这样一来其实就是真正的前序遍历一遍罢了

这个过程是前序的

```C++
class Solution {
public:
    int ret = 0;
    int sumNumbers(TreeNode* root) {
        vector<int> v;
        dfs(root, v);
        return ret;
    }
    void dfs(TreeNode *root, vector<int> v) {
        if(root == nullptr) return;
        v.push_back(root->val);
        if(root->left == nullptr && root->right == nullptr) {
            // 4 9 5
            int num = 0;
            for(auto & i : v) num = num * 10 + i;
            ret += num;
            return ;
        }
        dfs(root->left, v);
        dfs(root->right, v);
    }
};
```

---

宏观视角: 除了叶子节点, 其实每一个非叶子结点都是这样的操作: 下图的1234, 1是计算一下, 23是递归, 获取到左右子树的所有叶子节点的返回值之后, 4是返回给父节点的值, 代表这颗子树的返回值

其实也是前序

![image-20231112153030770](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112153030770.png)

```C++
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        return dfs(root, 0);
    }
    int dfs(TreeNode *root, int prevSum) {
        if(root == nullptr) return 0;  // 终止情况1
        prevSum = prevSum * 10 + root->val;
        if(!root->left && !root->right) return prevSum;
        int left = dfs(root->left, prevSum);
        int right = dfs(root->right, prevSum);
        return left + right;
    }
};
```

### [814. 二叉树剪枝](https://leetcode.cn/problems/binary-tree-pruning/)

> 剪枝 : 如果一颗子树 所有的结点值都是0, 则删除这颗子树

前序的话: 中左右, 这时候左右的情况都不知道, 怎么处理中呢? 所以前序不可行

所以, 后序, 左右中, 左右都处理完, 根据左右的处理结果才能进一步地处理根节点, 所以一定后序

---

宏观视角

把这个函数看作一个黑盒, 它的作用就是如果这个子树只有0没有1, 就会去除它, 并返回处理完成之后的这个数的结果

所以, 对某颗子树进行处理时, 先对左右孩子子树进行剪枝处理, 然后根据左右剪枝的结果, 以及val的值, 进行处理这颗子树, 只有左右处理完返回的是空, 且根节点val == 0时才会返回nullptr, 也就代表着这颗子树处理完结果是nullptr

![image-20231112155547379](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112155547379.png)

**所以要加返回值**  动作统一 每一个都要有返回值, 就很方便的获取左右子树结果, 并更新左右子树

----

通过模拟这个过程, 就可以想出这个题怎么解

### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

核心: 利用二叉搜索树的中序有序性, 以及全局变量存储中序的上一个值来判断

宏观来说, 这个函数就是接收一个根节点, 返回这个子树是否是二叉搜索树

整体肯定是要中序的, 先判断左, 判断自己是否符合, 判断右, 最终返回左&&自己&&右

剪枝就是: 当左子树返回false, 证明左子树中有元素不符合二叉搜索树的定义了, 这时候直接返回false即可, 后序的自己以及右子树都不需要进行

### [230. 二叉搜索树中第K小的元素](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/)

> 又做过

中序有序 + 两个全局变量即可

可以剪枝的时候要剪枝, 也就是比如左子树完了, 第K小元素已经有了, 那么自己, 右子树都不需要再处理, 直接返回

### [257. 二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/)

> 又做过.. 前序即可~

**借机学习一下回溯 + 恢复现场      +   剪枝**

> **简单题不用全局变量, 很多时候的DFS的参数已经自动恢复现场了, 所以不明显**
>
> **难题一定要用到全局变量, 此时的恢复现场十分重要**

回溯+恢复现场  :  因为递归之后会改变全局变量, 这样递归结束回溯的时候, 这个全局变量被改变了, 此时需要恢复现场!

![image-20231112171345169](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112171345169.png)

1. 这个题用全局的path确实麻烦, 但是可以体现出恢复现场. 而如果用参数的话, 自动恢复现场, 我们只能学到前序DFS
   其实如果参数里的string path是引用的话, 也需要手动恢复现场
2. 之前有过这样的情况: 判断左不为空才递归左, 右不为空才递归右, 这个操作其实就是一个剪枝, 也就是把空孩子剪掉了
   而如果这个情况不剪枝, 就在函数最开始处理一下空树, 直接返回, 其实就是函数终止条件/情况之一

```C++
class Solution {
public:
    vector<string> ret;
    vector<string> binaryTreePaths(TreeNode* root) {
        string s = to_string(root->val);
        dfs(root->left, s);
        dfs(root->right, s);
        if(ret.empty()) ret.push_back(s);
        return ret;
    }
    void dfs(TreeNode *root, string s) {
        if(root == nullptr) return;
        s += "->";
        s += to_string(root->val);
        if(root->left == nullptr && root->right == nullptr) {
            ret.push_back(s);
            return;
        }
        dfs(root->left, s);
        // 自动恢复现场
        dfs(root->right, s);
    }
};
```

**这个自动恢复现场很重要!!!    因为传过去的s不影响我这里的s, 所以递归结束, 回溯时不需要恢复现场**

## 穷举vs暴搜vs深搜vs回溯vs剪枝

### [46. 全排列](https://leetcode.cn/problems/permutations/)

穷举类的题

1. 画出决策树, 也就是所有的情况, 都列举出来 - 越详细越好    决策树只要能不重不漏的举出所有情况即可, 没有规定必须长什么样

这个题来说, 如果用数的DFS来做的话, 有点类似于求二叉树的所有路径, 这里完全可以用一个vector来记录, 过程中必然涉及到递归与回溯

这里的关键是, 比如第一个位置选了1, 那么后面的就不能再选1, 如何排除呢

这里采用了一个set或者一个数组来记录你用过了哪些元素, 也就是说, 每次递归都要把所有元素遍历一遍的, 选出第一个没有用过的即可

所以这里记录数据的path和记录使用情况的check数组要同步递归 + 恢复现场

![image-20231112180101148](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112180101148.png)

![image-20231112180725581](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112180725581.png)

```C++
class Solution {
public:
    vector<vector<int>> ret;  // 返回值
    vector<int> path; // 记录该路径的数据
    set<int> check;   // 记录该路径使用过的元素
    vector<vector<int>> permute(vector<int>& nums) {
        dfs(nums);
        return ret;
    }
    void dfs(vector<int> &nums) {
        // 选出第一个没有使用过的元素, 并递归
        // if(nums.size() == path.size()) {
        //     ret.push_back(path);
        // }
        for(int & i : nums) {
            if(check.find(i) == check.end()) {
                path.push_back(i);
                check.insert(i);
                if(nums.size() == path.size()) {
                    ret.push_back(path);
                    // 其实这一轮, nums中只有一个被选了, 选好之后, 这个for就结束了
                    // 但是在返回上一层之前必须恢复现场
                    path.pop_back();
                    check.erase(i);
                    return ;
                }
                dfs(nums);
                // 回溯 : 恢复现场
                path.pop_back();
                check.erase(i);
            }
        }
    }
};
```

这里其实就是, 如何记录我之前已经用过哪些元素了? 用个set / unordered_set就不错

这里分两种终止递归的方式, 一种是填满时直接终止, 一种是交给下一层递归, 这一层不加新元素

### [78. 子集](https://leetcode.cn/problems/subsets/)

第一步是想出一种策略, 把所有情况不重不漏地枚举出来, 这个其实就是决策树嘛

再把决策树转化为代码即可

----

主要问题是 12选了之后, 21如何避免?  可以用一个unordered_set<vector<int\>\>  解决 

![image-20231112195827335](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112195827335.png)

1. 这个决策树完全没想到: 其实就是对数组的每个元素进行选 / 不选, 而这两个情况都需要递归, 只有递归到最后一个元素时才会终止递归

下一步就是这个树转化为代码即可

2. 怎么记录我目前处理到第几个元素了? 搞一个参数i即可, 并且这个形参i不需要恢复现场, 很爽

其实恢复现场很简单, 就是恢复到递归之前即可~

> 这个相比之下更简单, 每个元素都是选 / 不选进行递归, 到最后一个元素时终止递归, 类似于树的叶子节点/空结点

![image-20231112202635792](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231112202635792.png)

这他妈, 怎么做到选了2, 之后不选1?  答案: 只选比上一个选择的数大的数

可以看绿色和下面选择的关系, 1后面选23, 2后面选3, 3后面没有

其实就是 我选了下标为1, 之后这个path只能选 2 / 3 / 4...

## 综合练习

### [1863. 找出所有子集的异或总和再求和](https://leetcode.cn/problems/sum-of-all-subset-xor-totals/)

按位与 & 按位或 | 且 && 或 || 非 ! 按位异或 ^

其实就是上一题求出所有的子集的同时求一个每个子集的按位异或的和即可

能不能不用path, 直接用一个int来记录这个子集的目前为止所有元素的异或值 ?  可是回溯应该怎么回溯呢?  也就是异或i的反操作是什么? 不会, 所以回溯就不会... 所以还是每次到了终止递归时处理一下整个path数组即可

新 : 异或x, 再异或一次x, 就会抵消

> 0选 / 不选, 1选 / 不选  nums.size() - 1选 / 不选

其实就和之前的子集那个题很像

### [47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)

> 先回顾一下全排列Ⅰ, 其实就是 1 2 3, 第一个位置选了1, 第二个位置就不能选1, 23都可以, 第二个位置选了2, 第三个位置就只能选3, 第二个位置选了3, 第三个位置就只能选2   123 132
>
> 所以需要记录, 目前为止选了哪些元素, 用bool数组或者unordered_set都可以

> 决策树的重要性!!!!!!!!!!!!!

思路一 : 其实无非就是全排列Ⅰ进行一个结果去重, 如果可以对vector<int\> 进行结果去重就好了, 112 112就会自动去重, 可是112 121会被去重吗?

思路二 : 画出决策树发现, 1. 之前选过的, 现在不能再选, 这是最基本的, 2. 在一个for内部, 有几个相同的元素, 若某个被选了, 则后续不再选择这个元素

![image-20231113132715934](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231113132715934.png)

其实相比于之前的全排列Ⅰ, 全排列Ⅰ是, 记录目前path用过哪些元素, 之前记录下标和值都可以, 因为元素值也具有唯一性, 但是注意这里必须记录的是下标

而这个题, 除了path里面有哪些下标的元素, 还要记录, 在一个for内部, 之前递归过的元素, 之后就不能再递归了, 比如第一行的1 1 2, 第二行第三组的112

```C++
class Solution {
public:
    vector<vector<int>> ret;
    vector<int> path;
    unordered_set<int> check;  // 记录之前选过的, 记录下标
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        dfs(nums);
        return ret;
    }
    void dfs(vector<int> &nums) {
        if(path.size() == nums.size()) {
            // 终止递归
            ret.push_back(path);
            return ;
        }
        unordered_set<int> used;  // 记录如果1递归过了, 则后续的1不再递归, 记录的是值
        for(int i = 0; i < nums.size(); ++i) {
            if(check.find(i) == check.end() && used.find(nums[i]) == used.end()) {
                // 这个元素目前路径没有用过, 且不与之前递归过的元素重复
                path.push_back(nums[i]);
                check.insert(i);
                dfs(nums);
                path.pop_back();
                check.erase(i);   // 恢复现场
                used.insert(nums[i]);
            }
        }
    }
};
```

check记录的是path用过的下标

而used只针对这个dfs函数, 也就是下面这个for循环, 递归过的后续不再递归

---

> ![image-20231114145200862](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231114145200862.png)
>
> 其实这个题的关键就是这一个点而已, 可以理解为, 我先选第一个位置的值, 这里重复的元素只能选择一次, 这也是剪枝操作的一种
>
> 第一点是这个题需要注意的, 第二点和全排列Ⅰ一样

### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

若干个字符串, 每个字符串选出一个, 进行搭配, 最终会出现多少种?

决策树很好画, 代码也容易

其实这个和全排列是有点像的, 但是这个比如之前选了a, 后面是不可能有a的, 所以不需要记录之前path有过的元素

![image-20231113140846277](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231113140846277.png)

```C++
class Solution {
public:
    vector<string> ret;
    string path;
    vector<string> letterCombinations(string digits) {
        if(digits.empty()) return ret;
        vector<string> vec = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"}; // 一共8个元素
        dfs(digits, vec, 0);
        return ret;
    }
    void dfs(string &digits, vector<string> &vec, int pos) {
        if(pos == digits.size()) {
            ret.push_back(path);
            return;
        }
        char c = digits[pos];  // 对应的按键
        string &s = vec[c - '2'];  // 本次需要for循环的字符串
        // pos标志着现在需要处理的字符串, 在vec中
        for(char & ch : s) {
            path += string(1, ch);
            dfs(digits, vec, pos + 1);  // 递归
            path.pop_back();  // 恢复现场
        }
    }
};
```

### [22. 括号生成](https://leetcode.cn/problems/generate-parentheses/)

没画决策树

核心思路: 粗略来说, 每次递归可以选(, 可以选), 而选左需要一定条件, 选右也需要一定条件, 判断即可

全局: 

path记录当前的字符串

num记录现在已凑成()的数量

leftNum记录当前没有配对)的(的数量

下面的逻辑仅限于目前还没有凑齐全部()的情况

若leftNum == 0则只能选(,

否则就是有(, 还要判断, 若不能再加新的(, 则只能加), 若可以, 则就是可以加(, 可以加)

每种情况加了括号之后都要递归, 回溯时要恢复现场

若进入递归时发现num == n, 则代表终止递归, 当前path就是一个合法path

----

就这???????

---

### [77. 组合](https://leetcode.cn/problems/combinations/)

![image-20231113150040103](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231113150040103.png)

这东西真得画决策树

画了之后把规律找到就清楚了

> 有点像子集, 因为12 21是重复的
>
> 又有点像全排列, 不是Ⅱ, 因为数组中没有重复元素

找上面的规律, 每一行是一个for, 1选了之后, 要从2开始, 2选了, 从3开始, 3选了从4开始

其实下面还会递归, 只是到了下一层递归之后发现个数已经满足, 直接返回终止递归

```C++
class Solution {
public:
    vector<vector<int>> ret;
    vector<int> path;
    vector<vector<int>> combine(int n, int k) {
        vector<int> v;
        for(int i = 1; i <= n; ++i) v.push_back(i);
        dfs(v, k, 0);
        return ret;
    }
    void dfs(vector<int> &v, int k, int pos) {
        // pos为从pos开始for循环遍历v, k是path元素数量上限
        if(path.size() == k) {
            ret.push_back(path);
            return ;  // 终止循环
        }
        for(int i = pos; i < v.size(); ++i) {
            path.push_back(v[i]);
            dfs(v, k, i + 1);
            path.pop_back();     // 恢复现场
        }
    }
};
```

最后这个for还真得注意一下

**是从pos开始遍历, 且递归传参时是i + 1**

### [494. 目标和](https://leetcode.cn/problems/target-sum/)

很简单哇

其实每一层只有一个元素, 从第一个元素 + / - 开始, 后面的每一个都是+ / -

不用遍历, 每个元素两个情况即可

![image-20231114152353862](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231114152353862.png)

如果是数组类的, 比如vector就不适合做参数了, 适合做全局.  像这种一个int, 做参数是比较合适的

且这个题做参数不超时, 做全局就超时, 因为做参数会有一点点的优化

### [39. 组合总和](https://leetcode.cn/problems/combination-sum/)

![image-20231113152239708](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231113152239708.png)

这不就清晰了吗? 233 323 332都是重复的, 怎么办?

还是那样的, 2可以从2开始, 3可以从3开始

```C++
class Solution {
public:
    vector<vector<int>> ret;
    vector<int> path;
    int pathSum = 0;
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        dfs(candidates, target, 0);
        return ret;
    }
    void dfs(vector<int> & candidates, int target, int pos) {
        if(pathSum == target) {
            ret.push_back(path);
            return ;
        }
        if(pathSum > target) {
            return ;
        }
        // 从pos开始进行遍历
        for(int i = pos; i < candidates.size(); ++i) {
            path.push_back(candidates[i]);
            pathSum += candidates[i];
            dfs(candidates, target, i);
            path.pop_back();            // 回溯 - 恢复现场
            pathSum -= candidates[i];   // 回溯 - 恢复现场
        }
    }
};
```

没剪枝

### [784. 字母大小写全排列](https://leetcode.cn/problems/letter-case-permutation/)

每次递归不用遍历, 只需要对当前元素处理即可

如果是字母, 则大小写两种递归, 如果不是字母, 直接加到path中

> a - z 97 - 122   A - Z 65 - 90  
>
> A -> a += 32   妈的

![image-20231113160001193](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231113160001193.png)

```C++
class Solution {
public:
    vector<string> ret;
    string path;
    vector<string> letterCasePermutation(string s) {
        dfs(s, 0);
        return ret;
    }
    void dfs(string &s, int pos) {
        if(pos == s.size()) {
            ret.push_back(path);
            return ;
        }
        char ch = s[pos];
        if(ch >= '0' && ch <= '9') {
            path.push_back(ch);
            // return dfs(s, pos + 1);
            dfs(s, pos + 1);
            path.pop_back();
            return ;
        }
        // 分小写大写两个情况
        if(ch >= 'a' && ch <= 'z') ch = (char)(ch - 32);
        // ch一定是大写
        path.push_back(ch);
        dfs(s, pos + 1);
        path.pop_back();  // 回溯
        // 小写
        path.push_back((char)(ch + 32));
        dfs(s, pos + 1);
        path.pop_back();
        return ;
    }
};
```

**致命错误, 看中间的数字的递归逻辑, 递归之后, 不能直接返回的, 比如a1b2, 2递归进入, 发现pos == s.size() 返回, 返回到2这里, 难道直接返回吗? 必须恢复现场, 把2去掉 变为a1b, 再回到b这一层, 小写处理完, 处理大写, 且小写递归完了 还要恢复现场, 变为a1, 再插入B, 变为a1B, 再进一步递归**

### [526. 优美的排列](https://leetcode.cn/problems/beautiful-arrangement/)

1 - n n个数字

逐个位置进行选择

从下标为0开始选, 候选项为所有数字, 每个位置遍历所有数字时都有两个条件: **之前没用过 且 符合条件**

<u>每个位置都可以遍历所有的数字, 只要这个数字没有被选过 且 符合条件, 就可以进一步递归</u>

之前选了x, 之后不能再选x

---

比如n = 5吧

第一个下标处选1 ? 2 3 4 5 ? 任何一个符合完美条件都可以进一步递归

第二个下标选1 2 3 4 5 ? 条件是之前没选过 且这个数字符合完美条件

主要是因为21 12 是不重复的

这里不必记录path, 因为最终只要符合条件的path的数量, 所以只需要记录当前用过哪些数字, 当然这个东西也需要恢复现场

```C++
class Solution {
public:
    int ret = 0;
    unordered_set<int> check;  // 记录已经使用过的元素, 存储值即可
    int countArrangement(int n) {
        vector<int> v;
        for(int i = 1; i <= n; ++i) v.push_back(i);
        dfs(v, 0);
        return ret;
    }
    void dfs(vector<int> &v, int pos) {
        // v是候选的所有元素, pos是即将填入的下标
        if(pos == v.size()) {
            ret++;
            return ;
        }
        for(int i = 0; i < v.size(); ++i) {
            if(check.find(v[i]) == check.end() && perfect(v[i], pos + 1)) {
                check.insert(v[i]);
                dfs(v, pos + 1);
                check.erase(v[i]);
            }
        }
    }
    bool perfect(int num, int pos) {
        if((num % pos == 0) || (pos % num == 0)) return true;
        return false;
    }
};
```

### [667. 优美的排列 II](https://leetcode.cn/problems/beautiful-arrangement-ii/)

1- 选过的不能再选

主要目的: 凑成n个时, 有k个不同的数字, 这个path 就符合条件

为了避免超时

1- 当找到了合法path, 后续都需要终止

2- 如果到了某一个位置时的不同数字已经超了, 则直接返回, 不要递归下去?

---

这B题用回溯根本解不了好吧??????

### [79. 单词搜索](https://leetcode.cn/problems/word-search/)

这个题的思路其实很简单, 按照目标字符串, 逐个字符进行查找即可

且每次查找时并不是遍历整个board

只有找第一个字符时, 可以遍历, 只要找到一个字符, 那么下次递归进入之后找下一个字符的搜索区域就很少了, 只是上一个位置的周围四个而已

判断, 这个新的位置是否越界, 判断这个位置是否使用过, 判断这个位置是否是目标字符

如果都满足, 则进一步递归...

```C++
struct PairHash {
    size_t operator()(const std::pair<int, int> &p) const {
        return std::hash<int>()(p.first) ^ std::hash<int>()(p.second);
    }
};

struct PairEqual {
    bool operator()(const std::pair<int, int> &lhs, const std::pair<int, int> &rhs) const {
        return lhs.first == rhs.first && lhs.second == rhs.second;
    }
};
class Solution {
public:
    std::unordered_set<std::pair<int, int>, PairHash, PairEqual> pairSet;
    // vector<vector<bool>> used;
    bool ret;
    int row;
    int col;
    bool exist(vector<vector<char>>& board, string word) {
        row = board.size();
        col = board[0].size();
        // used.resize(row);
        // for(auto & vec : used) vec.resize(col, false);
        {
            unordered_set<char> bSet;
            unordered_set<char> wSet;
            for(int i = 0; i < row; ++i) {
                for(int j = 0; j < col; ++j) {
                    bSet.insert(board[i][j]);
                }
            }
            for(auto & ch : word) wSet.insert(ch);
            for(auto & ch : wSet) {
                if(bSet.find(ch) == bSet.end()) return false;
            }
        }
        dfs(board, word, 0, {-1, -1});
        return ret;
    }
    void dfs(vector<vector<char>> &board, string &word, int pos, pair<int, int> prevPos) {
        if(pos == word.size()) {
            ret = true;
            return ;
        }
        // 现在在找word[pos]这个字符
        char target = word[pos];
        if(prevPos.first == -1 && prevPos.second == -1) {
            // 最开始, 找第一个字符
            for(int i = 0; i < row; ++i) {
                for(int j = 0; j < col; ++j) {
                    if(board[i][j] == target) {
                        pairSet.insert({i, j});
                        dfs(board, word, pos + 1, {i, j});
                        if(ret) return ;
                        pairSet.erase({i, j});  // 恢复现场
                    }
                }
            }
        } else {
            int i = prevPos.first;
            int j = prevPos.second;
            // 从prevPos的周围的合法坐标中, 找target, 找到了就递归, 没找到就返回
            vector<pair<int, int>> choice = {{i - 1, j}, {i + 1, j}, {i, j - 1}, {i, j + 1}};
            for(auto & p : choice) {
                if(func(p)
                && board[p.first][p.second] == target
                && pairSet.find(p) == pairSet.end()) {  // 又找到了一个
                    pairSet.insert(p);
                    dfs(board, word, pos + 1, p);
                    if(ret) return ;
                    pairSet.erase(p);   // 恢复现场
                }
            }
        }
    }
    bool func(pair<int, int> &pos) {
        if(pos.first >= 0 && pos.first < row && pos.second >= 0 && pos.second < col) return true;
        return false;
    }
};
```

unordered_set的第二个模板参数: 求哈希值的类, 第三个 : 判断是否相等的类

> `std::unordered_set` 是 C++ 标准库中的一个容器，它是无序、不重复元素集合的实现。以下是 `std::unordered_set` 的各个模板参数的解释：
>
> 1. **Key（键类型）**：
>    - 这是集合中存储的元素类型。对于 `unordered_set`，键就是元素本身。例如，如果你要存储整数，键类型就是 `int`；如果要存储自定义类型，键类型就是该自定义类型。
> 2. **Hash（哈希函数类型）**：
>    - 这是用于计算键的哈希值的函数对象。哈希函数将键转换为容器内部索引的无符号整数值。对于自定义类型，你可能需要提供自定义的哈希函数。
> 3. **KeyEqual（键相等性判定函数类型）**：
>    - 这是用于比较键是否相等的函数对象。在哈希冲突时，它用于检查两个键是否相等。对于自定义类型，你可能需要提供自定义的相等性判定函数。
> 4. **Allocator（分配器类型）**：
>    - 这是用于分配内存的分配器类型。默认情况下，使用 `std::allocator`，但你可以指定其他分配器类型。
>
> 举例说明，使用 `std::unordered_set` 存储整数的情况下，模板参数通常如下所示：
>
> ```
> cppCopy code
> std::unordered_set<int> mySet;
> ```
>
> 如果要使用自定义类型（比如 `std::pair<int, int>`）作为键，你可能需要提供自定义的哈希函数和相等性判定函数：
>
> ```
> cppCopy codestruct PairHash {
>     size_t operator()(const std::pair<int, int> &p) const {
>         // 自定义的哈希函数
>         return std::hash<int>()(p.first) ^ std::hash<int>()(p.second);
>     }
> };
> 
> struct PairEqual {
>     bool operator()(const std::pair<int, int> &lhs, const std::pair<int, int> &rhs) const {
>         // 自定义的相等性判定函数
>         return lhs.first == rhs.first && lhs.second == rhs.second;
>     }
> };
> 
> std::unordered_set<std::pair<int, int>, PairHash, PairEqual> pairSet;
> ```
>
> 模板参数的选择取决于你存储的类型以及你对容器的特定需求。

### [51. N 皇后](https://leetcode.cn/problems/n-queens/)

> 要求N * N的棋盘, 放N个棋子, 每一行, 每一列只能放一个, 另外, 每一斜排也只能放一个

> 关键是一开始没什么画出决策树的思路
>
> 第一排: 可以放在第一个位置, .... 到第N个位置, 然后看第二排, 
>
> 这样一来, 我只需要记录每一列的棋子的放置情况, 不能在同一列放置超过一个即可
>
> 可是斜侧怎么处理?如果是4 * 4, 就是有7 + 7个斜侧, 前7个每个最多有一个, 后7个每个最多有一个

![image-20231114165745600](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231114165745600.png)

> 这样一看其实也不算很难啊
>
> 其实图中每一行都是棋盘中某一行的选择

决策树已出, 怎么转化为代码?

每一行遍历嘛, 然后每一列的冲突其实可以用一个unordered_set解决, 不难

<u>主要是斜的怎么搞? 其实, 比如ij我要放, 此时直接左上遍历, 右上遍历, 看有没有棋子不就行了? 如果竖的不冲突, 且斜的不冲突, 就放入, 然后递归下一行呗</u>

easy

全局变量: 搞一个N * N棋盘(这里直接一个vector string 即可) , 一个unordered_set, 一个ret即可..

---

超时??????

![image-20231114173036066](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231114173036066.png)

这种处理斜方的方法, 其实我之前想过, 但是实现起来 / 想起来都不如直接遍历来的简单, 当然可能更高效一点~

注意: 如果从上往下处理每一行, 则考虑斜方向时就是左上和右上, 因为下面不可能有棋子(即使之前递归过, 也会恢复现场), 如果从下往上处理每一行, 则考虑右下和坐下的位置有没有棋子
