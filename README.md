### 数组

#### [209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

暴力解法O(N^2)

滑动窗口: 滑动窗口和双指针很像, 也是两个指针去维护这个窗口, 只是这个窗口一向右移动的时候很像一个滑动窗口, 所以用滑动窗口来表示这种思路相比双指针更形象一些

滑动窗口的重点: 一个for循环, 那么这个索引表示窗口的起始还是终止? 这个很重要, 如果表示起始, 那么和暴力的思路是一样的, **所以滑动窗口一定是用for里的索引表示窗口的终止**, 而起始位置如何表示/维护, **如何移动滑动窗口的起始位置, 就是滑动窗口的重点所在了**



好了, 现在说一个我的疑惑, 就是, 每次当滑动窗口内的数值满足条件时, 要进行while循环判断, 那么, 最终会导致滑动窗口内的数值不满足条件时才会结束, 然后滑动窗口右端右移, 那这样会有影响吗?

没有影响, 比如现在有10个元素, 窗口[0]比较大, 然后while的最后一次打破了条件, 此时右端右移, 之前考虑的是打破条件是否有影响, 起始没有, 比如如果我们让滑动窗口满足条件之后, 最后一次不打破, 右端右移, 此时, 滑动窗口大小加一, 加了一个值, 肯定更满足了, 那么左边右移, 其实有可能打破这个条件, 这时又有10个元素了, 可是不打破的话, 11一定比10大, 而我们期望找到最小的窗口大小, 所以, 右边不断右移, 左边一定要右移的, 

其实我害怕的无非是, 整体右移一个之后, 总大小变小了, 之前10个满足, 此时10个不满足了, 但是还是那句话, 我们期望的是找到更小的, 只要是10个不满足, 无所谓, 一直向右滑动即可, 明白了吗?   直到右边那个突然来了一个很大的, 让左边可以右移多次, 就找到更小的窗口了

所以其实整个的基础还是双指针, 只是用滑动窗口更形象罢了.

也就是说, 10个满足, 变9个, 不满足, 右边右移, 10个, 不满足了, 无所谓, 继续右移, 即使是11, 12, 13都不满足, 但是没事, 因为10已经记录下来了, 我们期望的是, 突然右边来了一个很大的, 然后左边右移很多, 窗口变得比10小了, 此时就有新的更小的窗口了, 明白了!!!!!

### 栈与队列

#### [239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

滑动窗口向右滑动, 取出滑动窗口的最大值.

单调队列: 队列首部(出口)维护的一定是当前滑动窗口内的最大值, 这样每次取出max时, 只需要获取front即可

但是如何做到这个效果/目的呢?

push: 每次入队列: 如果队列尾部的元素比新元素小, 则直接弹出, 直到降序为止(单调队列底层使用deque实现, 并不是使用queue实现, 所以可以pop_back)

pop: 如果要弹出的元素, 也就是滑动窗口右移之后不包含的元素, 不是front, 则说明其实要弹出的元素不是之前滑动窗口内的最大值, 自然也就不是front, 自然也就不在单调队列的内部了, 所以不用进行pop_front

get_max: 获取当前滑动窗口最大值的操作直接获取front即可

每次如果新值是最小的, 直接入队列尾部即可, 因为之后窗口右移到以这个值为第一个值的时候, 它可能是最大的

### 二叉树

#### [226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

只需要遍历每个节点, 操作是swap左右孩子即可, 所以直接递归前序即可(后序, 层序都可以)

递归的中序不可以, 为什么呢?

#### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

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

#### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

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

#### [111. 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)

这个当然可以按照层序的思想, 每一层遍历, 当某一层第一次出现左右孩子为空时, 直接返回这一层的层数即可, 这也就是遍历到这个节点所经过的最小深度~

但是我采用了递归的方式, 这里需要注意的是若左右孩子只有一个不为空时, 不能直接返回1 + min(min(minDepth(root->left), minDepth(root->right));) 因为为空的一方会直接返回0, 这样就大错特错了, 0一定比另一方小的, 且你某一孩子为空, 你还递归它干嘛, 这一定不符合条件啊, 所以只能递归不为空的那一方, 每一次返回都加一个1, 这样每经过一个节点都会加一个1, 最终也就是最小深度了

可以看出：**求二叉树的最小深度和求二叉树的最大深度的差别主要在于处理左右孩子不为空的逻辑。**

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

#### [222. 完全二叉树的节点个数](https://leetcode.cn/problems/count-complete-tree-nodes/)

这题就别想着递归遍历了, 时间复杂度不符合, 要利用完全二叉树的性质!

完全二叉树要么是满二叉树要么不是满二叉树

先判断这颗子树是不是满, 如果是, 则直接用公式求这颗子树的节点个数

若不是, 则返回1 + 递归左 + 递归右

每一次递归都是这样, 若满, 则直接求, 不满则递归, 最终当只有一个节点时, 就会符合满二叉树的性质~

满二叉树  n = 2^(depth) - 1
