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

> 后序是高度, 也就是从叶子节点到该节点的, 上面 高
>
> 前序是深度, 是从顶部开始计算的, 从上往下, 也就是从根节点向下, 下面 深

#### [111. 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)

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

#### [222. 完全二叉树的节点个数](https://leetcode.cn/problems/count-complete-tree-nodes/)

这题就别想着递归遍历了, 时间复杂度不符合, 要利用完全二叉树的性质!

完全二叉树要么是满二叉树要么不是满二叉树

先判断这颗子树是不是满, 如果是, 则直接用公式求这颗子树的节点个数

若不是, 则返回1 + 递归左 + 递归右

每一次递归都是这样, 若满, 则直接求, 不满则递归, 最终当只有一个节点时, 就会符合满二叉树的性质~

满二叉树  n = 2^(depth) - 1

> 求深度可以从上到下去查 所以需要前序遍历（中左右），而高度只能从下到上去查，所以只能后序遍历（左右中）

#### [257. 二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/)

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

#### [404. 左叶子之和](https://leetcode.cn/problems/sum-of-left-leaves/)

没难度, 前序即可

> 这道题目要求左叶子之和，其实是比较绕的，因为不能判断本节点是不是左叶子节点。
>
> 此时就要通过节点的父节点来判断其左孩子是不是左叶子了。
>
> **平时我们解二叉树的题目时，已经习惯了通过节点的左右孩子判断本节点的属性，而本题我们要通过节点的父节点判断本节点的属性。**
>
> 希望通过这道题目，可以扩展大家对二叉树的解题思路。

#### [513. 找树左下角的值](https://leetcode.cn/problems/find-bottom-left-tree-value/)

第一反应: 层序可以= =, 最后一层的第一个即可

递归:

目的: 找出最后一层(深度最深)的第一个节点

深度最深很简单, 直接维护一个全局的max_depth即可, 可是第一个怎么办? 如何防止右边的不重复更新, 其实也很简单, 只需要当深度大于max_depth时再更新就好了, 这样右边的就不会更新了~

两个版本, 一个详细回溯版, 一个简略版

核心就是一个前序即可, 之前就说过了前序求深度最合适

#### [112. 路径总和](https://leetcode.cn/problems/path-sum/)

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

#### [106. 从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

![image-20231008205858998](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20231008205858998.png)

关键是搞清楚, 后序最后一个是根, 根在中序的左和右分别就是左子树对应的数组, 和右子树对应的数组, 而后序的前面一部分就是左子树, 后面一部分就是右子树, 且中序左数组和后序左数组大小相等, 对应的就是左子树, 中序的右数组和后序的右数组对应右子树, 完全可以递归处理, 因为本来这个函数的作用就是通过一个树的中序和后序数组构建一棵树!!!!!!!!

而当中序左或右数组分割成空, 后序的对应数组也会是空, 此时直接就会返回nullptr

如果只有一个, 则中序和后序的左右数组都是空, 也会进一步返回空的~

所以核心就是分割数组!!!!!!



> 其实还是递归的思路, 首先我可以把根节点构造出来, 那么这个函数的参数就是两个数组, 我再把左右子树的数组找出来, 就可以递归构建了

#### [654. 最大二叉树](https://leetcode.cn/problems/maximum-binary-tree/)

输入是一个数组, 那么, 找到根之后构建根节点, 递归的思路很显然就可以想到, 找出左右子树的数组就可以递归了

最终的叶子节点的左右子树的数组为空, 这其实也是递归的终止条件嘛, 返回nullptr即可

每次递归都是 : 构建根节点, 递归左右子树, 就是这样的

#### [654. 最大二叉树](https://leetcode.cn/problems/maximum-binary-tree/)

说实话没啥难度, 只是可以再稍微优化一下, 不用构造新的数组, 直接在原数组中处理

> **注意类似用数组构造二叉树的题目，每次分隔尽量不要定义新的数组，而是通过下标索引直接在原数组上操作，这样可以节约时间和空间上的开销。**
>
> 一些同学也会疑惑，什么时候递归函数前面加if，什么时候不加if，这个问题我在最后也给出了解释。
>
> 其实就是不同代码风格的实现，**一般情况来说：如果让空节点（空指针）进入递归，就不加if，如果不让空节点进入递归，就加if限制一下， 终止条件也会相应的调整。**

#### [617. 合并二叉树](https://leetcode.cn/problems/merge-two-binary-trees/)

如果一方为空, 一方不为空, 是直接返回这个不为空的, 还是自己再复制一个新的这个不为空的

如果后者, 就是完全构造一个新的二叉树出来~ 我都写了

#### [700. 二叉搜索树中的搜索](https://leetcode.cn/problems/search-in-a-binary-search-tree/)

对于一般二叉树，递归过程中还有回溯的过程，例如走一个左方向的分支走到头了，那么要调头，在走右分支。

而**对于二叉搜索树，不需要回溯的过程，因为节点的有序性就帮我们确定了搜索的方向。**

例如要搜索元素为3的节点，**我们不需要搜索其他节点，也不需要做回溯，查找的路径已经规划好了。**

中间节点如果大于3就向左走，如果小于3就向右走



二叉搜索树的迭代不需要栈和队列, 因为二叉搜索树的搜索路径是确定的, 因为它本身的性质, 所以直接一路往下走即可

#### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

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
