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

# 链表

### [203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)

秒了, 直接搞一个哨兵节点会好做很多, 每次判断当前节点的next即可

### [707. 设计链表](https://leetcode.cn/problems/design-linked-list/)

浪费好长时间, 其实没什么问题, 主要是双向链表在初始化时, sentinel的next和prev要初始化为sentinel本身, 这样在链表为空时才好复用不为空时的头插和尾插代码

也算是对链表操作的回顾吧, 其实不难, 就那样

### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

三个指针, prev cur next往后遍历就行了

### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

依旧是搞一个哨兵节点

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

### [面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

没难度, 秒了

先求两个的长度, 然后求差值, 然后较长的先走差值步, 然后再一起走, 直到相等, 可能为空, 那就没有相交, 可能不为空, 那就相交

### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

- set可以去重
- 数学公式 - 不想搞
- 先求一个环形内的结点, 然后直接把该节点与next断开, 以next为头, 另一条以head为头, 转化为链表相交问题

### [234. 回文链表](https://leetcode.cn/problems/palindrome-linked-list/)

栈先进先出即可, 要判断一下链表长度是偶数还是奇数

另一种思路: 后半段链表进行逆置, 然后与前半段进行比较, 若一样, 则回文, 不一样则不回文.

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

### [155. 最小栈](https://leetcode.cn/problems/min-stack/)

.... 为什么还是不会???

思路: stack存pair first是元素, second表示当该元素是栈顶元素, 即将pop时, 栈中的最小值

因此, push就很简单了, first固定, second只需要判断栈中已有的所有元素中的最小值和当前元素哪个小, 取较小值即可

pop很简单, top很简单, min也就依靠这个second实现了

对呀, 这个其实很简单的啊?? = == = = = = = =

### [394. 字符串解码](https://leetcode.cn/problems/decode-string/)

数字一定表示次数, 遇到]一定要找上一个数字, 然后生成一个字符串, 可是这个字符串也有可能要和前面的拼接起来, 怎么办? 

ok 过了, 怎么说呢... 其实不算特别难, 但是很多小细节需要处理好

整体来说, 只要有一个数字, 就搞一个string, 且原始的那个也要搞一个string

也就是每次遇到], 就处理一下, 然后得到一个结果, 现在需要考虑的是, 可能这个是另一个的string的一部分, 然后整体再乘倍数, 那如果不是, 其实就是最终字符串的一部分了, 这个使用stack就可以完美处理掉, 就是我也不知道这是其他的一部分还是最终的一部分, 无妨, 利用stack就可以完美解决

## 单调栈

### [739. 每日温度](https://leetcode.cn/problems/daily-temperatures/)

<u>**单调栈: 用于求解当前元素左面或者右面第一个比他大或者第一个比他小的元素!!!!!!**</u>

这个题就是单调栈的最直接, 最简单的运用

单调栈: 作用: 针对这个题就是, 存放我们遍历过的元素(从左向右遍历)

我明白了, 这个题关键就是: 遍历过的, 就存储起来, 而来了一个新元素, 此时可能左边某个或某些元素的右边第一个比它大的元素就是这个新的元素, 那么, 怎么才能及时的, 当第一个比它大的元素来到时, 就及时得出对应左边元素的结果呢? 使用一个单调递增的栈就ok了, 挨个与栈顶比较, 如果大, 就符合, 就更新结果, 弹出栈顶元素, 继续比较下一个

这样就达到了一个目的: 当某元素的右边第一个比它大的元素来到时, 就会及时的更新它的结果. 因为这是一个单调递增的栈.

如果是单调递减, 比如栈内存储 90 80 70, 此时来了一个75, 是可以更新70的, 但是因为栈只能获取top, 所以75 < 90, 就直接被栈顶元素挡住了, 就无法更新70的结果

---

针对这个题: 从左向右遍历, 遍历到i下标时, 并不知道它右边谁第一个比他大, 所以i下标的结果无法填入, 但是, 遍历到i时, 它可能是它左边某元素的右边第一个比它大的, 所以, 是可以填它左边的元素的结果的

单调栈: 顾名思义, 栈内的元素始终保持单调递增 / 单调递减, 对于找右边第一个大的, 就递增, 也就是当一个新元素到来时, 除非栈顶的元素>= 这个元素, 否则栈顶的元素就是小于这个新的元素的, 此时, 这个栈顶元素的右边第一个比它大的元素就是这个新元素, 因此栈顶元素就可以填结果了

另外, 栈内是要填下标的, 而不是元素值, 否则通过元素值找下标还需要O(N)遍历

过了, 这个题逻辑过程并不难, 再缕一缕思路: 遍历到某元素时, 它左边的元素才有可能填值, 而如果左边的某些元素没有结果, 就一定在栈中, 如果你比它大, 就可以得出它的结果, 只要是它还在栈中, 就说明, 至此为止, 一直都没有比它大的出现, 而如果你满足条件, 就可以得出它的结果, 又因为这个栈是从栈顶到栈底递增的, 所以新元素可以得出所有比它小的元素的结果

![image-20231030125510511](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231030125510511.png)

比如左图, 是递增的, 只要新元素比栈顶的大, 就可以得出它的结果. 而右图, 是递减的, 并不会因为栈顶比新元素大, 而后面的小就无法得出后面的元素的结果.

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

### [226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

只需要遍历每个节点, 操作是swap左右孩子即可, 所以直接递归前序即可(后序, 层序都可以)

递归的中序不可以, 为什么呢?

### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

之前的问题是: 我可以做到判断当前根节点的左右子树的两个根节点是否符合条件, 但是我总不能递归左根节点的左右孩子 / 右根节点的左右孩子吧? 因为这根本不对啊, 我不要求左右孩子的左右孩子是符合条件的, 而是要求左孩子的右孩子与右孩子的左孩子符合条件, 哈哈, 那这样不就成了吗

对于二叉树是否对称，要比较的是根节点的左子树与右子树是不是相互翻转的，理解这一点就知道了**其实我们要比较的是两个树（这两个树是根节点的左右子树）**，所以在递归遍历的过程中，也是要同时遍历两棵树。

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

前序

严格来说, 这里求的才是深度的, 也就是用max_depth记录最大的深度, 逐步向下前序递归, 遍历时处理方法很简单就是更新max_depth

而每个节点的深度用参数depth来记录, 向下递归时要+1, 回溯回来要减1

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

层序

当然用层序也可以, 每经过一层depth++

> 后序是高度, 也就是从叶子节点到该节点的, 上面 高
>
> 前序是深度, 是从顶部开始计算的, 从上往下, 也就是从根节点向下, 下面 深

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

每个节点都是先看自己是不是pq之一, 是直接返回, 或者到了空也返回.

那, 如果自己不是, 则要看左右情况, 所以后序先进行左右递归

若左右都不是空, 说明左右各有一个p/q, 则自己就是最近公共祖先

若左右有一个为空, 一个不为空, 此时情况不好说, 因为可能两个都在这个不为空的子树中, 也有可能只有p/q之一在里面

不管怎样, 都直接返回这个不为空的, 若只有一个, 则这个节点的上方的另一边也会收到不为空

若pq都在里面, 则一路向上返回即可, 好好想一下这个过程其实不难, 但是很难自己一开始就想到

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

高度平衡, 所以简单来说, 只要每棵树的左右都平衡, 整棵树就平衡了, 最多是左一个孩子, 右没有呗, 这样其实就是 12345

思路很简单, 找出数组中间点, 中间点就是根节点, 然后分成左和右两个数组, 递归处理就行, 数组为0, 就是返回nullptr, 数组为1 返回根节点就行了= =

12345 就是根节点的左右子树的高度为2

1234567 就是深度为三的满二叉树= =

> 首先取数组中间元素的位置，不难写出`int mid = (left + right) / 2;`，**这么写其实有一个问题，就是数值越界，例如left和right都是最大int，这么操作就越界了，在[二分法](https://programmercarl.com/0035.搜索插入位置.html)中尤其需要注意！**
>
> 所以可以这么写：`int mid = left + ((right - left) / 2);`

上方内容指的是另外写一个函数进行递归处理 记得保持边界不变量, 左闭右闭 左闭右开, 要始终统一!

### [538. 把二叉搜索树转换为累加树](https://leetcode.cn/problems/convert-bst-to-greater-tree/)

反中序即可= =, 还有就是其实不用维护vector

### [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

这个题来说, 最先需要搞清楚的是直径怎么计算, 其实对于任何一个根节点来说, 经过此根节点的路径, 一定是左子树的最深节点到右子树的最深节点, 经过这个根节点的最长路径一定是这样的, 而对于整颗树来说, 最长路径可能并不经过根节点, 但是一定经过某颗子树的根节点!!!!



所以, 后序遍历, 每个根节点求出左子树的最深叶子节点到根节点的节点个数, 右子树的最深叶子节点到根节点的个数

而路径 = left + right + 1 - 1 第一个1是根节点, 第二个1是路径的边数 = 总节点个数 - 1

说真的, 对后序回溯越来越熟练了, 而这个题最好的解法就是从下往上处理, 而不是从上往下, 因为前序从上往下时, 到了一个根节点并不知道这个子树的情况, 后序就很棒了

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
};
```

# 动态规划

## 斐波那契数列模型

dp基本解题流程

- 状态表示: 先以一个一维数组或二维数组作为一个dp表, 然后将其填满, 而每个下标都有一个值嘛, 而这个值代表一个含义, 而这个含义就是一个状态表示



心得/技巧:

所以dp的核心就是状态表示, 状态转移方程, 其实就是dp数组的每个元素的含义嘛, 你要把这个dp数组存什么东西, 一般都由经验 + 题目来得出, 而状态标识可能正确可能错误, 我们要勇于去定义状态表示, 然后尝试推到状态转移方程, 如果定义对了, 皆大欢喜, 若错了, 就再来一次 , 就是要多定义, 多体会, 多总结~

### [1137. 第 N 个泰波那契数](https://leetcode.cn/problems/n-th-tribonacci-number/)

推导状态转移方程:  

状态转移方程是什么? dp[i] = x  x就是状态转移方程!!!!  这道题而言: dp[i] 依赖于前三个状态, 而具体怎么依赖呢? 题目已经说的很清楚了, 就是相加. 所以 dp[i] = dp[i-1] + dp[i-2] + dp[i-3], 这个就是这道题的状态转移方程

### [746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)

比如这个题, 要求到达楼顶的最小花销, 那么状态表示有两种, 也对应着两种解题方法,  第一个: dp[i] 标识到达i位置的最小花销, 所以返回值也就是dp[n]了. 第二种: 从dp[i]到达楼顶的最小花销, 所以返回值也就是dp[0]和dp[1]的较小值了, 因为要从0或1号台阶开始嘛, 所以就是0或1台阶到达楼顶的最小花销~

### [91. 解码方法](https://leetcode.cn/problems/decode-ways/)

这个题相比于前几个入门题来说, 难度上就有了一个小的提升了

但是现在的总结很遗憾是我看了解析之后的, 并不是直接做出来的, 我觉得还是需要自己先思考思考

状态表示: dp[i]表示字符串解码到i下标字符时的解码方法个数, 所以返回值理所应当就是dp.back(), 也就是最后一个字符时的整个字符串的解码方法

下面是状态转移方程, 其实到了s[i]的时候, 无非两种情况, 单独解码 或 i && i-1两个字符一起解码, 此时就需要具体考虑了

单独解码和两个字符一起解码都有可能失败, 若单独解码成功, 则单独解码贡献的字符串解码方式就是dp[i-1] 若失败, 则至i字符为止, 单独解码i字符的整个字符串的解码方式个数都是0

若两个字符一起解码, 也就是i && i-1, 则如果解码成功, 其实就是贡献了dp[i-2]个解码方式, 而若失败, 则0, 因为最后两个字符无法联合解码 则在此情况下, 整个字符串就无法解码, 所以其实就是这样的

我们知道, 状态转移方程肯定是要结合最近一步或两步的结果的, 但是确实... 得思考思考这个方程怎么实现的

把情况分析清楚之后, 程序就很好写了, 但是分析这个题的重点又在状态转移方程上, 而状态转移方程又需要对题有一定的理解,  也就是到了某个字符之后, 应该怎么解码, 有哪些情况....



----

所以, 为了少几行冗余代码, 就多注意这么多真的值得吗?=. =

## 路径问题

### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

虽然是第一道二维dp数组, 但是其实比较简单, dp\[i][j] 表示到达i,j下标时的路径方法个数, 而状态转移方程还是惯例 : 根据附近的状态表示求出, 也很简单, 根据题目, 到达ij只能从它的上或者左过来, 所以, 到达ij的路径方法个数 dp[i]\[j] = dp[i]\[j-1] + dp[i-1]\[j] 注意, 比如从它的左边走一步过来, 是路径的个数+1, 而不是路径的方法加一, 到了这个地方的路径个数还是那个个数, 只是多了一步而已, 一步是不一个方法!

所以, 这个题只是dp数组变二维了, 其他没有很大的变化

### [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)

讲真的, 确实没难度啊, dp数组肯定是二维的毋庸置疑, 但是, 对于mn的大小来说, 是开辟mn还是m+1 n+1呢? 其实多开辟一行一列是为了初始化方便, 而mn的话初始化就有点麻烦了

实践过了, mn初始化确实麻烦, 因为若第一行或第一列的某一个元素为1, 也就是为障碍物, 则直接影响后面的

而m+1n+1的话, 多的一行一列初始化不变, 而后面的直接进行一个判断即可

---

状态表示: dp[i]\[j] 表示 : 到达ij位置时, 一共有多少种不同的路径

状态转移方程: dp[i][j\] 分两个情况, 有障碍物, 则0, 无障碍物, dpij = dpi-1 j + dpi j-1 

### [LCR 166. 珠宝的最高价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

原剑指offer - 礼物的最高价值, 没什么区别

其实题目来说还是二维矩阵, 每次往右或往下收集礼物, 然后求出最大价值

状态表示: dp[i][j\] 表示到达ij位置时的最大价值

状态转移方程: dp[i\][j\] 分两个情况, 从上面走和从左边走, 若上面则上面的最大价值 + 自己的价值 左边 则左边的最大价值+自己的价值, 而根据状态表示, 上面和左面的最大价值就是对应坐标的dp值, 因此, 取一个较大值

![image-20231012124126215](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231012124126215.png)

初始化 : 目的: 防止越界, 所以多一行多一列即可, 两个问题: 多出的空间存什么值: 0, 原因略了   下标映射问题, 很简单

而多一行一列就是为了在处理第一行和第一列时它的上&&左不越界嘛, 所以多一行多一列, 让原本的第一行&第一列成为第二行第二列=. =

### [931. 下降路径最小和](https://leetcode.cn/problems/minimum-falling-path-sum/)

状态表示: 以某个位置为结尾 => 到达ij位置时的最小的下降路径

状态转移方程: 某位置的dp值, 也就是路径下降最小和的值 分三个情况, 也就是上一排的三个位置走过来, 所以应该是三者里面的最小值, 而每个的最小值又是它的下降路径最小值 + 自己的值, 而它的下降路径最小值根据状态表示 其实就是dp[对应位置] 因此

![image-20231012124924574](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231012124924574.png)

> 也就是说, 某一个位置的dp值, 取决于它的上一排的若干三个(可能两个), 那么这样层层依赖, 其实第一排的是固定的, 所以第二排就是固定的,  因此从上至下, 从左至右, 就可以把dp数组填满喽

初始化, 多加一行 两列即可, 且第一行初始化为0 两列初始化为+无穷, 还是两个问题, 填值以及映射问题, 很简单

n*n 则dp 为n+2 * n+2 dp[i]\[j] 表示到达ij下标时的下降路径最小和

那么返回值就是min(dp的倒数第二行的所有元素中的下降路径最小和) (最小值)    (最后一行没意义, 所以n+1 n+2的话就是返回最后一行的最小值即可)

其实也可以n+1 n+2 行上多一行, 列上多两列, 就可以解决边界问题了, 且第一行要初始化为0, 其余的多出的两列要初始化为INT_MAX

这样就没什么难度了, 就是边界需要稍微注意一下~

### [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

状态表示 : 以某个位置为结尾 xxxx  : dp[i][j\] 表示 到达ij位置时的最小路径和

状态转移方程: 依旧两个情况, 从上面来或者从左面来, 所以取两个情况较小值, 而每个情况的值都是原始位置的最小路径和+自己位置的值, 而根据状态表示, 原始位置的最小路径和本身就是dp[x][y\]  所以 就很简单 = =

![image-20231012130926657](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231012130926657.png)

典的不能再典了

初始化 : 目的: 不越界

两个注意事项: 填值, 映射. 

### [174. 地下城游戏](https://leetcode.cn/problems/dungeon-game/)

这道题的关键在于为什么要逆向dp而不是正向dp, 若正向, 则状态表示为: dp[i][j\]表示从起点出发, 到达ij位置所需要的最小健康值.  也就是为以什么什么为重点......   而逆向dp的状态表示为 : 从ij位置出发, 到达终点所需的最低健康点数

为什么正向不行? 因为仅记录mn的所需最低健康点数是不对的, 因为可能中间直接-1000 +1000, 也就是只能保证到达mn时健康值>0, 但是中间是有可能健康值<=0的, 所以还需要记录这个过程中所需的最低健康点数的最大值

逆向dp: 某位置的dp值等于下一个位置(右或下)所需的最低健康点数 - 当前值(负数), 比如下一个位置所需最低值为5, 当前为-6, 则就是12

## 简单多状态dp问题

### [面试题 17.16. 按摩师](https://leetcode.cn/problems/the-masseuse-lcci/)

状态表示: 为什么说多状态呢? 因为每个地方的dp值都有两个状态, 也就是, 选还是不选, 选的最大预约时长 , 不选的最大预约时长

则每个下标都对应存储两个值, 选择该位置的情况下的最大预约时长, 不选该位置的情况下的最大预约时长

状态转移方程: 选的dp值 dp[i] = 不选上一个的最大预约时长 + 自己的值  不选的dp = 上一个的最大预约时长(两个状态的较大值) + 自己的值

所以返回值也就是最后一个位置的两个状态的最大预约时长的较大值~

> 关键在于, 其实如果前面一个位置的两个状态的最大值确定了, 那么后面一个位置的也就确定了, 因为根据状态转移方程得知每个位置的选或不选的最大结果都只和前一个位置有关, 所以层层后移推导, 就会得出最终结果~

### [198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

和上一个一模一样=. =

> i位置偷的话, 则前一个和后一个就不能偷, 那, 状态转移方程中i位置只考虑前一个可以吗? 其实是可以的, 因为后一个的最大值到时候会考虑前一个的, 所以不需要每个值都考虑前后

### [213. 打家劫舍 II](https://leetcode.cn/problems/house-robber-ii/)

和上一个太像了, 唯一不同就是首尾连接

思路是没想到的, 其实Ⅰ和Ⅱ的唯一区别就是, 比如0号偷, 那么尾是不受影响的, 只要n-2不偷, n-1就可以偷, 也就是0和n-1可以同时偷, 而打家劫舍Ⅱ中的首偷了, 则1和n-1都不能偷, 其实这就是唯一的区别的, 没有其他区别了!!!!  认识到这点很重要, 所以这个题可以转化为打家劫舍Ⅰ的问题

所以, 0号偷, 则1 n-1不能偷, 中间的2 - n-2为线性问题, 转化为打家劫舍Ⅰ   而0号不偷, 则首尾不需要再注意了, 所以1 - n-1为线性问题

这个思路确实牛, 没想到, 可以学习理解一下

### [740. 删除并获得点数](https://leetcode.cn/problems/delete-and-earn/)

这个题感觉描述的不是很到位, 其实本质就是: 选择x, 则获取所有x的点数, 但是x-1 与 x+1就不能选了, 计算怎么选择是最大的结果

和打家劫舍Ⅰ很像, 因为首尾不相连, 并且有区别的是, 可能数组的相邻元素的值并不相邻

状态表示: 两个值: 选该元素的最大值, 不选该元素的最大值

状态转移方程: 选该元素的最大值 = 不选x-1的最大值 + 该元素 * 个数

不选该元素的最大值 = x-1选/不选的最大值的较大值

> 本质就是选x 则x-1 x+1就不能选, 且每个值可能有多个, 看最大的选择结果为多少, 神似打家劫舍Ⅰ, 因为首尾不相连, 且可能相邻元素可以都选, 因为可能并不是值相邻的关系 = =

### [LCR 091. 粉刷房子](https://leetcode.cn/problems/JEj789/)

动态规划的题, 重点还是相邻的房子颜色不能相同, 也就是当前为红, 则上一个就不能为红了, 且下一个也不能为红, 也就是实际上i位置是否为红要受前后两个影响, 但是我们只需要处理好当前和前一个, 之后当后一个处理时也会顾及前一个, 就没问题了

状态表示: 以i位置为结尾, i位置涂为某颜色的最小开销(所有),  而颜色有三种, 这就是多状态, 所以用三个数组即可存储, 类似于之前的选/不选 

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

也可以直接搞一个dp二维数组, n个房子n个元素, 每个元素是一个三元素的vector数组, 分别对应三个颜色, 都一样

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

3. 不持股 - 且以后不可购买   =   昨天不可购买 / 昨天持股, 然后今天卖了就不可购买了

> 这种股票问题, 变幻莫测, 因为你可以在任何一天买/卖, 所以最佳方式就是记录每天的每种不同操作之后的最大利润, 而i天受i-1天的结果影响, 实际上i-1天其实还受之前的影响, 所以就是层层递进=. =

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

### [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

![image-20231014202447618](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231014202447618.png)

> dp问题, 首先确定状态表示

状态表示: dp[i] 表示 以i位置为结尾的所有子数组里面的最大和  (这些子数组以i为结尾)

所以 一共的情况其实就是上面的那几个

状态转移方程: 

这些子数组可以分为两类, 1. 只包含i自己  2. 包含其他元素, 最后一个元素为i

我们要找这些里面的最大和, 第一个的和已经知道了, 后面几个的最大和怎么求呢?

其实, 后面几个的子数组有一个共同点, 抛去最后一个i元素之后, 其实求的就是以i-1元素结尾的所有子数组里面的最大和, 而这个最大和加上一个nums[i], 就是以i结尾的所有子数组的最大和, 此时, 这个最大和再和Nums[i]比较一下,  也就是第一个子数组, 结果就是dp[i]应该存储的了

> 这个很牛逼啊, 能理解倒是能理解, 但是自己想出来是真想不出来

这样一来, dp[i]又和dp[i-1]联系起来了

这样一来 dp[i] = max(nums[i], dp[i-1] + nums[i]);  确实牛逼    

### [918. 环形子数组的最大和](https://leetcode.cn/problems/maximum-sum-circular-subarray/)

相比于最大子数组和的差别就是首尾可以相连, 所以可以直接分为以下两个情况

1. 最大和子数组是在原始数组的内部
2. 最大和子数组包含首元素和尾元素且不是全部元素, 也就是数组前方有一段, 尾部有一段

1的解法和最大子数组和一样, 2的解法: 当首尾两段的和是最大和时, 中间的子数组的和就是最小的和, 因为sum = max + min, 当max越大, min越小, max最大, min最小, 所以求解情况2, 可以转化为求解最小子数组和, 然后sum - min

特殊情况: 当最小子数组和 = sum时, 说明数组全部为负数, 最大子数组和为0, 也就是空的, 这是不对的, 此时不能通过sum - min 获取最大子数组和, 因为为空了

### [152. 乘积最大子数组](https://leetcode.cn/problems/maximum-product-subarray/)

> 基本思路和最大子数组和是一样的, 但是有差别
>
> 最直接显著的差别: 当nums[i] < 0时, 比如-10, 那么之前的做法是dp[i] = max(dp[i - 1] * nums[i], nums[i]),  此时, -10 相乘的数越大, 结果越小, 相乘的数越小, 结果越大, 所以, 若nums[i] < 0, 正确的结果应当是 max(nums[i], 以i-1结尾的最小子数组乘积 * nums[i]), 若nums[i] > 0, 结果应当是max(nums[i], 以i-1为结尾的最大乘积子数组 * nums[i]) , 因为>0的数的乘数越大, 结果越大

所以, 这个题需要两个dp表, f数组的状态表示为: dp[i] 为 以i元素为结尾的所有子数组中的最大乘积, 另一个g数组dp表的状态表示为: dp[i] 为以i元素为结尾的所有子数组的最小乘积

因为每一个元素的dp值(最大乘积)的结果, 可能用到f 可能用到g, 取决于它是>0 还是 <0

### [1567. 乘积为正数的最长子数组长度](https://leetcode.cn/problems/maximum-length-of-subarray-with-positive-product/)

这个和上一个题很像

状态表示: dp[i] 表示以i元素为结尾的乘积为整数的最长子数组的长度

但是dp[i] 不能直接用dp[i - 1] + 1, 因为确实dp[i-1]为以i-1为结尾的乘积为正数的最长子数组的长度, 但是nums[i] 如果大于0, 那加一个1没什么问题, 但是如果nums[i]为负的, 就错了

如果为负的, 其实dp[i]应该是 = i-1为结尾的乘积为负数的最长子数组的长度, 这样再乘一个负的 就是正的了

所以需要维护两个dp表

并且这里还有一些情况, 当维护f表和g表时, 比如如果nums[i] > 0, 则g[i] 应该是g[i-1] + 1, 但是不能直接这样, 因为如果g[i-1]为0, 则g[i]应该为0, 而不是1, 这个我也考虑到了

### [413. 等差数列划分](https://leetcode.cn/problems/arithmetic-slices/)

状态表示: 以某元素为结尾, 巴拉巴拉

dp[i] 表示 以i元素为结尾的等差数列的个数

状态转移方程: 若nums[i] - nums[i - 1] == nums[i -  1] - nums[i - 2]; 则dp[i] = dp[i - 1] + 1;

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

状态表示: dp[i]表示以i元素为结尾的最长湍流子数组

```C++
class Solution {
public:
    int maxTurbulenceSize(vector<int>& arr) {
        int n = arr.size();
        vector<int> dp(n);
        dp[0] = 1;
        int m = dp[0];
        for(int i = 1; i < n; ++i) {
            if(dp[i - 1] == 1 && arr[i] != arr[i - 1]) dp[i] = 2;
            else if(dp[i - 1] == 1 && arr[i] == arr[i - 1]) dp[i] = 1;
            else {
                // 不管是2, 3, 4都一样
                // 1 5 2
                if(arr[i] == arr[i - 1]) dp[i] = 1;
                else if(arr[i] > arr[i - 1] && arr[i - 1] < arr[i - 2]) dp[i] = dp[i - 1] + 1;
                else if(arr[i] < arr[i - 1] && arr[i - 1] > arr[i - 2]) dp[i] = dp[i - 1] + 1;
                else dp[i] = 2;
            }
            if(dp[i] > m) m = dp[i];
        }
        return m;
    }
};
```

状态转移方程: 分情况, 其实上面写的还不错, 但是可能是有优化空间

当nums[i] == nums[i - 1] 则直接dp[i] = 1; 不用考虑

下面的就是不相等的情况下

若dp[i-1] == 1则dp[i] = 2;

若不是1, 则肯定>=2, 则直接湍流判断, 若成立 则dp[i] = dp[i-1] + 1 不成立, 则dp[i] = 2

> 除非第一个元素, 或者前一个等于它, 不然不会是1的

略微优化

```C++
if(arr[i] == arr[i - 1]) dp[i] = 1;
else {
    if(dp[i - 1] == 1) dp[i] = 2;
    else {
        // 不相等, 且dp[i - 1] != 1
        if((arr[i] > arr[i - 1] && arr[i - 1] < arr[i - 2])
        || (arr[i] < arr[i - 1] && arr[i - 1] > arr[i - 2]))
            dp[i] = dp[i - 1] + 1;
        else
            dp[i] = 2;
    }
}
```

### [139. 单词拆分](https://leetcode.cn/problems/word-break/)

dp问题

状态表示: dp[i] 表示以i字符结尾的前沿整体字符串能否拼接成功

状态转移方程: 如下图, dp[i] 是否等于true, 也就是能否拼接成功, 需要校验多次, 任意一种情况可以成功, 则dp[i]就是true

而每一种情况 = dp[i - 1] && s[j, i+1)在字典中, 若两个条件都可以达成, 则为true

最后一种情况也就是当搜索的字符串的起始下标j == 0时, dp[-1]不存在, 所以就是直接搜索整体字符串s[j, i+1)是否在字典中

起始我最初的想法是: 每到一个新的下标, 直接看左侧的dp为true的下标x之后的字符串s[x+1, i+1)是否在字典中, 其实本质是和这个一样的

每到一个新的下标, 然后逐步左移, 先看dp[j-1]是否为true, 若为true, 再看s[j, i+1)字符串是否在字典中, 若在, 则整体为true, 即拼接成功

> 这个如果加一个虚拟首元素, 则可能会稍微方便一点, 只是初始化的方式不同而已

![image-20231015150852302](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231015150852302.png)

### [467. 环绕字符串中唯一的子字符串](https://leetcode.cn/problems/unique-substrings-in-wraparound-string/)

> 感觉和978最长湍流子数组很像

状态表示: dp[i]表示以i字符结尾的不同非空子串在base中出现的次数

状态转移方程: 

任意一个字符, 单个字符组成的子串肯定在base中, 这个是1

abc d  

若i字符和i-1字符相衔接, 则包含但不仅限于i-1字符和i字符组成的子串的个数为dp[i - 1], 因为只是每种情况多了一个字符而已, 所以就是dp[i - 1]个情况

所以, dp[i] = 1 + dp[i - 1];

但是问题是, 最终结果不能是dp数组全部的和, 因为完全可能有重复的 = =

如果有两个d 且在不同的位置怎么办????   比如一个d的dp值为4, 一个d的dp值为3, 则4的情况一定包含3????

没错的, 所以要保存一个所有字符结尾的最大值即可

> 吗的, 我好棒啊, 这都直接做出来了?????

### [300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)

> 直接dp干就行了
>
> 碰壁了, 因为这个和过往的子数组系列的题的最大差别是子序列可以不连续
>
> 那, 这个其实n^2肯定是能解的, 但是... 就有点没意思了, 而且好像还可dp/不dp
>
> = = 就n^2吧, dp的话只能这样

> 非常非常经典???

状态表示: dp[i]表示以i元素结尾的最长严格递增子序列的长度

状态转移方程: 求dp[i]时, 并不只需要dp[i - 1], 而是需要遍历0 - i-1, 当nums[i] > nums[j]时, 更新dp[i] = max(dp[j] + 1, dp[i])

![image-20231015195857289](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231015195857289.png)

### [376. 摆动序列](https://leetcode.cn/problems/wiggle-subsequence/)

> 这个和最长湍流子数组很像, 只是这个是子序列, 也就是元素之间可以不连续
>
> 像湍流子数组就很简单, 因为dp[i]只需要看nums[i] nums[i - 1] nums[i - 2]之间的关系即可, 不用考虑其他的
>
> 但是这个就不一样了, 这个和上一题一样, 子序列问题很有可能需要向前遍历

状态表示: 以某个位置为结尾, 然后分析问题

dp[i]是一个pair, first表示以i下标元素为结尾的最长摆动序列的长度, 而second是一个int, 表示该元素与摆动数组中上一个元素的大小关系, 不然没法搞

状态转移方程:

> 我怎么感觉这个dp表不能只存长度啊, 还需要存该元素与摆动数组中上一个元素之间的大小关系, 不然怎么搞...
>
> 没错, 直接过了, 没压力, 我太聪明了

和上一个题一样, 序列问题到i元素时都需要遍历0 - i-1, 当摆动条件符合(借助dp[i].second)时更新dp[i]的first和second

这个second挺秒的, 主要是因为你这个序列的元素可能在原数组中不相邻, 所以摆动条件不好判断, 加个这个直接解决~

### [673. 最长递增子序列的个数](https://leetcode.cn/problems/number-of-longest-increasing-subsequence/)

状态表示:

dp[i]是一个pair, pair之一的元素表示以i下标元素为结尾的最长递增子序列的个数, 这个完完全全可能不止一个 比如 1 3 5 4 7 则7的最长长度为4, 但是个数为2

> 不对, 这个除了记录以i下标结尾的最长递增子序列的个数, 还要记录这个最长递增子序列的长度, 因为可能有多个元素的长度一样, 这样返回值就需要相加了,  这个其实用处很大

但是不能只存储个数, 还要存储这个最长递增子序列的长度, 这是肯定的

状态转移方程:

> dp[i]这里, 因为是序列问题嘛, 所以肯定是要遍历0 - i-1的
>
> 若符合大于的关系, 则更新dp[i]呗, 这么简单???

在求dp[i]时, 遍历0 - i-1

没到一个元素, 记为j, 则先比较, 若大于, 也就是j为结尾的递增子序列此时来了一个新的值, 但是只有当这个新的长度大于i保存的最长底层子序列的长度时, dp[i]的记录的长度才需要更新, 因为存储的是最长的嘛

除了大于, 当等于时也需要更新, 因为这里需要记录个数

而每处理完一个dp[i], 就更新全局的最大长度和最大长度的子序列的个数, 最后直接返回这个个数~

```C++
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<pair<int, int>> dp(n, {1, 1});   // first: 个数, second: 长度
        int max_num = dp[0].first;   // 总的最长递增子序列的个数
        int max_len = dp[0].second;  // 整个数组中的最长递增子序列的长度
        for(int i = 1; i < n; ++i) {
            for(int j = i - 1; j >= 0; --j) {
                if(nums[i] > nums[j]) {
                    if(dp[j].second + 1 > dp[i].second) {
                        dp[i].second = dp[j].second + 1;   // 新的更长的子序列
                        dp[i].first = dp[j].first;  // 新的更长子序列的个数
                    } else if(dp[j].second + 1 == dp[i].second) {
                        dp[i].first += dp[j].first;
                    }
                }
            }
            // dp[i]处理完了
            if(dp[i].second > max_len) { // 有了新的更长的子序列
                max_len = dp[i].second;
                max_num = dp[i].first;
            }
            else if(dp[i].second == max_len) {
                max_num += dp[i].first;
            }
        }
        return max_num;
    }
};
```

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

<u>**比如 现在处理的dp[i]的数对是  10  12 而前面有  3 9   3 6   2 3 这样的数对, 是否first越大, dp值一定越大呢? 我想是的,  那first一样, dp值一定一样吗? 我想是的,  那这样的话, 是不是就不用继续往前遍历了呢???**</u>  

> 这里挺牛逼~~~

结论: 找到第一个符合要求的直接结束即可

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

所以, 用哈希表做dp能成功主要是因为这里的diff已经给了!!!!!

![image-20231015215143501](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231015215143501.png)

### [873. 最长的斐波那契子序列的长度](https://leetcode.cn/problems/length-of-longest-fibonacci-subsequence/)

状态表示:

dp[i] 表示以i下标元素为结尾的最长的斐波那契子序列的长度

状态转移方程:

> 因为是子序列问题嘛, 所以如果dp的话肯定是n^2复杂度的, 主要是因为子序列问题的序列的元素组成可以不连续, 所以需要遍历0 - i-1
>
> 但是dp表中的关键是 不能只存储长度, 还要存储该最长斐波那契子序列的上一个元素的值, 这样才好判断i元素是否符合条件
>
> 其实之前也见过这样的题, 也就是除了dp值外, 还要存一些用于判断条件是否成立的值, 这是子序列问题的常见问题和套路

> 按照上面的解法, 也是不对的, 因为任意一个元素都不能只存一个前一个元素, 
>
> **这个题一维dp解不了, 需要二维dp**

状态表示: dp[i][j\] 表示以ij元素为末尾的最长斐波那契子序列的长度



![image-20231016114225692](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231016114225692.png)

二维dp\[i][j\]表示以ij元素为结尾的最长的斐波那契子序列的长度, 为什么这样可以? 因为ij知道, 前一个元素就知道了, 这样直接在0 - i-1范围内查找这个目标元素即可, 这是固定的!!!! 这样, dp\[i][j] = dp[k][i\] + 1

![image-20231016141537601](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231016141537601.png)

j逐步向后, i在0 - j-1范围内逐步向前, 这就已经是O(N^2)了, 目标元素已知, 就需要在0 - i-1范围内查找, 但是这样是可以优化的, 因为目标元素已知, 且元素值和下标一一对应, 所以直接用哈希就可以O(1)求出k的值为多少, 此时dp[k][j\]就直接得出了

注意这里的i 永远 < j, 所以二维dp数组的横坐标永远小于纵坐标, 

![image-20231016142027723](https://cdn.jsdelivr.net/gh/DaysOfExperience/blogImage@main/img/image-20231016142027723.png)

求解dp\[i][j\] 时需要dp[k\][j], k < i i < j所以只需要dp数组的横坐标更小的值, 也就是上方的, 所以dp数组的求值顺序是从上到下

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

这个和上一个斐波那契感觉很像

主要是状态表示不能是以i元素为结尾的最长等差数列的长度, 这是不对的

因为i需要遍历0 - i-1, 你到了j之后, j这里只有这一个长度信息, 是完全不够的

因为任何一个元素组成的等差数列都是很灵活的,  前一个元素是什么都可以, 而当两个元素固定之后, 其他元素也就固定了

所以直接二维dp, dp[i][j\]表示以ij元素为结尾的最长等差数列的长度, 这样的话, 任意一个元素都可以和多个元素搭配成等差数列, 而不仅限于一维dp的只能存储一个值

j逐步向后, i遍历0 - j-1, 这样一来, 最后两个元素固定, 倒数第三个确定了就, 这样dp\[i][j\] = dp[n][i\] + 1

i小于j j从2开始, i从1开始, 
