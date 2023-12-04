> 前言：结合现在的阶段
>
> AVL：本身就是基于二叉搜索树的。
>
> 我只实现了插入，没实现删除。
>
> 插入：先按照二叉搜索树的基本套路进行插入，然后更新平衡因子，然后根据新插入结点的父节点的平衡因子进行处理。
>
> 若不平衡，则旋转。
>
> 其实重点也就是个旋转了。
>
> 四种旋转。
>
> 左单旋和右单旋来说，其实把抽象图画出来之后，就一目了然了，无非就是改变一下各种结点的父子关系，然后更新一下平衡因子（简单）
>
> 左右双旋和右左双旋来说，也就是两次单旋+更新平衡因子（较单旋来说需要分情况，较复杂一些）。其实画出来抽象图之后，平衡因子的更新以及两次单旋对谁进行也就很简单了。
>
> 所以核心也就是个抽象图~，抽象图画出来，AVL也就很简单了。
>
> **总结：AVL的重点是旋转，旋转的重点是抽象图~**

# AVL树的概念

二叉搜索树虽可以提高查找的效率，但如果插入数据时数据有序或接近有序二叉搜索树将退化为单支树，查找元素相当于在顺序表中搜索元素，效率低下。O(N)

> 故，两位俄罗斯的数学家G.M.Adelson-Velskii 和E.M.Landis**（AVL树名字的由来）**在1962年发明了一种解决上述问题的方法：当向二叉搜索树中插入新结点后，如果能保证每个结点的左右子树高度之差的绝对值不超过1(需要对树中的结点进行调整)，即可降低树的高度，从而减少平均搜索长度，提高效率，发挥二叉搜索树的作用。
>
> AVL树是最先发明的**自平衡二叉查找树**。在AVL树中任何节点的两个子树的高度最大差别为1，所以它也被称为**高度平衡树**。增加和删除可能需要通过一次或多次树旋转来重新平衡这个树。

一棵AVL树或者是空树，或者是具有以下性质的**二叉搜索树**：

1. 左右子树高度之差(简称平衡因子)的绝对值不超过1(-1/0/1)

2. 它的左右子树都是AVL树

(注意，AVL树的两个性质是基于二叉搜索树来说的)

<img src="https://img-blog.csdnimg.cn/46e43f426ea04df48eb0bcbd806dad98.png" alt="img" style="zoom:67%;" />

即，通过控制二叉搜索树中每颗子树的左右子树的高度差的绝对值不超过1，使得这颗二叉搜索树更接近于完全二叉树，高度接近log2N，提高查找效率。

# AVL树结点定义

```cpp
template <class K, class V>
struct AVLTreeNode
{
    AVLTreeNode(const pair<K, V>& kv)
    : _left(nullptr), _right(nullptr), _parent(nullptr), _kv(kv), _bf(0)
    { }
    AVLTreeNode<K, V>* _left;
    AVLTreeNode<K, V>* _right;
    AVLTreeNode<K, V>* _parent;
    pair<K, V> _kv;  // 键值对，AVL树的每个节点存储的数据类型
    int _bf; // balance factor 平衡因子
};
```

上方AVLTreeNode定义中，每个结点包含三个指针，左右子节点指针以及双亲结点指针，结点数据类型采取的键值对pair。其中_bf为balance factor平衡因子，这个不是定义AVL树必须的，只是这里采取了平衡因子的实现方法，或许更简便。

**平衡因子：**结点的平衡因子_bf = 右子树的高度 - 左子树的高度

# AVL树的插入

```cpp
bool Insert(const pair<K, V>& kv)
{
    // 如果此时是一个空树，直接建立新节点，改_root即可。此时左右子节点和父节点均为nullptr，平衡因子为0.
    if(_root == nullptr)
    {
        _root = new Node(kv);
        return true;
    }
    Node* parent = nullptr;
    Node* cur = _root;
    while(cur != nullptr)
    {
        if(kv.first > cur->_kv.first) {
            parent = cur;
            cur = cur->_right;
        }
        else if(kv.first < cur->_kv.first) {
            parent = cur;
            cur = cur->_left;
        }
        else {
            // 找到了相等的，此处的平衡二叉搜索树不支持多键值相等
            return false;
        }
    }
    // 此时找到了合适的位置，cur==nullptr,parent为要插入位置的父节点
    cur = new Node(kv);
    if(kv.first > parent->_kv.first) {
        parent->_right = cur;
    }
    else {
        parent->_left = cur;
    }
    cur->_parent = parent;
    // 现在整个树的父子结点关系都弄好了，新插入结点的左右子节点为nullptr，
    // 更新平衡因子（parent->_bf）
    while(parent != nullptr)
    {
        if(cur == parent->_right) {
            parent->_bf++;
        }
        else {
            parent->_bf--;
        }
        if(parent->_bf == 0) {
            // 表示之前_bf == -1 or _bf == 1，此时parent这个树高度不变，不会影响其他祖宗结点。
            break;
        }
        else if(abs(parent->_bf) == 1) {
            // 之前_bf == 0，此时parent这棵树高度改变，需要继续向上修改
            cur = parent;
            parent = parent->_parent;
        }
        else if(abs(parent->_bf) == 2) {
            // 需要旋转
//                if(parent->_bf == 2 && parent->_right->_bf == 1) {
            if(parent->_bf == 2 && cur->_bf == 1) {
                // 较高右子树的右边高，左单旋
                RotateL(parent);
            }
            else if(parent->_bf == -2 && parent->_left->_bf == -1) {
                // 较高左子树的左边高，右单旋
                RotateR(parent);
            }
            else if(parent->_bf == -2 && cur->_bf == 1) {
                // 较高左子树的右边插入，左右双旋
                RotateLR(parent);
            }
            else if(parent->_bf == 2 && cur->_bf == -1) {
                // 较高右子树的左边插入，右左双旋
                RotateRL(parent);
            }
            break;  // 一次插入最多一次旋转。
        }
        else {
            assert(false);
        }
    }
    return true;
}
```

AVL树是二叉搜索树的一种扩展，基于二叉搜索树的性质，增添了每个结点的左右子树的高度差的绝对值不超过1，也就是平衡因子<=1的规定，以此保证搜索性能。

故，AVL树的插入与二叉搜索树的插入原理相同。这里就不赘述了（参照二叉搜索树的插入方式）。在将结点插入之后（注意，三叉链），最重要的是更新平衡因子（因为AVL树就是通过保证整棵树的每个结点的平衡因子从而确保AVL树的高度以及效率的。）

# 平衡因子更新

新插入结点直接影响并改变父节点的平衡因子，可能改变根节点至该新增结点路径上的所有结点的平衡因子。 

平衡因子更新实现代码为上方Insert函数最后的那个while循环

（以下用cur代表新增结点，parent代表新增结点的父节点）

1. 若cur 是 parent的左孩子，parent的平衡因子--

2. 若cur 是 parent的右孩子，parent的平衡因子++

根据parent更新后的平衡因子，决定下一步操作。

1. 若parent->\_bf == 0，则结束平衡因子的更新。 
    原因：更新前\_bf == 1 or -1（注意任何一个结点的原始平衡因子都不可能是2 or -2），此时插入后，parent这颗树的高度不变，不影响parent的parent（基于parent不是根节点）。注意：新增结点的父节点要么只有一个子节点要么没有子节点。

2. 若parent->\_bf == 1 or -1 则继续向上更新，即执行cur = parent; parent = parent->_parent;
    原因：原本parent->\_bf == 0，此次插入新节点后，parent这颗子树高度改变，影响了parent的父节点，故需要循环更新。

3. 若parent->_bf == 2 or -2，表示此时parent这颗子树已经不平衡了，**需要进行旋转调整**。且旋转之后，平衡因子更新结束，原因见旋转的作用与结果。

4. 若abs(parent->_bf) >= 2，则表示这颗树在新增结点前就出现了问题，正常情况不会出现。

# AVL树的旋转

我们这里说的旋转，是因为某个结点的bf == 2 or -2，也就是这个结点的左右子树高度差超过了1，不平衡了，故需要旋转。而不平衡一定是由插入某个结点导致的。

**根据插入结点位置的不同，将AVL树的旋转分为4类：**

## 1. 新节点插入较高左子树的左侧，进行右单旋

**较高左子树的左侧插入新节点，右单旋抽象图：**

![img](https://img-blog.csdnimg.cn/e1110980a724469bbcb569d98d41f9bb.png)

注：此处h表示高为h的子树，h>=0。所有较高左子树的左侧插入新节点进行右单旋的情况都可以用上图归纳。

**H = 0，1，2的具体实例AVL树：**

![img](https://img-blog.csdnimg.cn/034c0a12d9684aa89b54636c83e32675.png)

上图，都属于在较高左子树的左侧插入新的结点，导致该子树根结点的bf == -2，且根节点的左孩子bf == -1，即较高左子树的左边高，需要进行右单旋。

注：H=1的情况就两种，15的左或者右插入新节点。H=2的情况很多，插入节点位置有四种，且60的右子树和30的右子树形状不定，但是必须是H=2，且30的左子树必须为上图形状。
 以此类推，实际的右单旋的实例情况非常多，但是都可以被抽象图归纳。

**右单旋代码：**

```cpp
    void RotateR(Node* parent)
    {
        Node* subL = parent->_left;
        Node* subLR = subL->_right;

        parent->_left = subLR;
        if(subLR)
            subLR->_parent = parent;

        Node* ppNode = parent->_parent;
        parent->_parent = subL;
        subL->_right = parent;

        if(parent == _root) {
            _root = subL;
            subL->_parent = nullptr;
        }
        else {
            if(parent == ppNode->_right) {
                ppNode->_right = subL;
                subL->_parent = ppNode;
            }
            else {
                ppNode->_left = subL;
                subL->_parent = ppNode;
            }
        }
        subL->_bf = parent->_bf = 0;
    }
```

**代码解析：**

结合抽象图观察，其实就是修改parent subL subLR的父子关系。还要注意一下parent是整棵树的根节点还是子树的根节点需要分情况处理。 

**右单旋后平衡因子更新：**

还是结合抽象图，所有右单旋，旋转完成之后，parent和subL的平衡因子都变为了0。
 且插入新节点前，整棵树的高度为h+2，插入新节点导致不平衡，旋转后整棵树的高度为h+2。因此，AVL树的Insert操作中，若进行了旋转调整，就可以直接结束平衡因子的更新，因为整棵树的高度没有改变。（见Insert函数中，旋转后的break）

## 2. 新节点插入较高右子树的右侧，进行左单旋

**较高右子树的右侧插入新节点，左单旋抽象图：**

![img](https://img-blog.csdnimg.cn/cc705e6277fa48dd98484ebd48efd8cf.png)

**左单旋代码：**

```cpp
    void RotateL(Node* parent)
    {
        Node* subR = parent->_right;
        Node* subRL = subR->_left;  // 可能为空

        parent->_right = subRL;
        if(subRL)
            subRL->_parent = parent;

        subR->_left = parent;
        Node* ppNode = parent->_parent;  // 修改parent->parent之前，保存原先parent->parent
        parent->_parent = subR;

        if(parent == _root)
        {
            _root = subR;
            subR->_parent = nullptr;
        }
        else
        {
            if(parent == ppNode->_right) {
                ppNode->_right = subR;
                subR->_parent = ppNode;
            }
            else {
                ppNode->_left = subR;
                subR->_parent = ppNode;
            }
        }
        // 这里是一定的！！！左单旋后的平衡因子结果
        subR->_bf = parent->_bf = 0;
    }
```

左单旋代码和平衡因子更新和右单旋的原理相同，不再赘述。 

## 3. 新节点插入较高左子树的右侧，进行左右双旋：先左单旋，再右单旋

**抽象图** 

![img](https://img-blog.csdnimg.cn/18cbdb6bd2674c0d9c08068ea9f33bcf.png)

**左右双旋示例图：**

![img](https://img-blog.csdnimg.cn/ab24bebb2a50484782a4bdb77914fb96.png)

![img](https://img-blog.csdnimg.cn/29b087ad1c884bf8b5212cd5c1998432.png)

H=0情况仅一种，H=1两种，左边还是右边插入。
 H=2情况比较多：90和30这两颗子树的子节点可以有两个，可以有一个，但是必须保证H=2.
 50必须有两个子节点，否则，50的bf == 1 or -1，这样，再在60的较高左子树的右边插入时，要么50的bf变为0，要么50这颗子树进行旋转（单旋双旋皆有可能)。而我们的目的是构建出H=2的左右双旋情景。

新插入结点可以在50的左孩子的左或者右，可以在50的右孩子的左或者右。这将直接决定旋转之后45的bf和60的bf，也就是parent和subL的bf。具体原因见下方左右双旋平衡因子的更新： 

**左右双旋代码：**

```cpp
    void RotateLR(Node* parent) {
        Node* subL = parent->_left;
        Node* subLR = subL->_right;

        int bf = subLR->_bf;

        RotateL(subL);
        RotateR(parent);

        if(bf == 1) {
            parent->_bf = 0;
            subL->_bf = -1;
            subLR->_bf = 0;
        }
        else if(bf == -1) {
            subL->_bf = 0;
            parent->_bf = 1;
            subLR ->_bf = 0;
        }
        else if(bf == 0) {
            subL->_bf = 0;
            parent->_bf = 0;
            subLR->_bf = 0;
        }
        else {
            assert(false);
        }
    }
```

**左右双旋平衡因子更新：**

先在subL进行左单旋，再在parent进行右单旋。最终结果是：subLR把左孩子给了subL的右，subLR把右孩子给了parent的左。
 故，结点插入在subLR这颗子树中是固定的，但是具体插入在subLR的左还是右将决定双旋后subL和parent的平衡因子，其中一方bf会变为0，另一方为1 or -1。且subLR的平衡因子一定变为0
 因此，根据旋转前subLR的平衡因子，可以推断出旋转后parent 和 subL的平衡因子。

这里平衡因子的更新有三种情况：

1. 新节点插入在subLR的左，subLR->bf == -1

2. 新结点插入在subLR的右，subLR->bf == 1

3. subLR就是新节点（H==0的情况） subLR->bf == 0

## 4. 新节点插入较高右子树的左侧，进行右左双旋：先右单旋，再左单旋

**抽象图** 

![img](https://img-blog.csdnimg.cn/a7f29d8c22214549a7d553eff257d961.png)

**右左双旋代码：** 

```cpp
   void RotateRL(Node* parent) {
        Node* subR = parent->_right;
        Node* subRL = subR->_left;

        int bf = subRL->_bf;

        RotateR(subR);
        RotateL(parent);

        if(bf == 1) {
            subR->_bf = 0;
            parent->_bf = -1;
            subRL->_bf = 0;
        }
        else if(bf == -1){
            parent->_bf = 0;
            subR->_bf = 1;
            subRL->_bf = 0;
        }
        else if(bf == 0) {
            // H = 0的情况，最简单的情况
            parent->_bf = 0;
            subR->_bf = 0;
            subRL->_bf = 0;
        }
        else {
            assert(false);
        }
    }
```

与左右双旋原理相同， 

#  如何理解旋转

0. 首先，你必须建立起对抽象图的信任和崇拜，因为每一个抽象图都真实地概括了所有对应旋转的实例情况。

1. 仅仅只是基于根节点的某一个子树：左子树或者右子树较高，使得根节点bf == 1 or -1，此时，在较高的那个子树中插入了新的值，导致根节点的bf == 2 or -2 违背了AVL树的规则，需要进行旋转降整棵树的高度。基于插入元素的位置，即左子树较高还是右子树较高，较高子树的左边还是右边。分为四种情况，对应四种旋转。

2. 双旋实际上就是两次单旋的组合，只是针对不同的情况，平衡因子的变化不同。双旋的关键在于平衡因子的更新

3. 总结：
   假如以pParent为根的子树不平衡，即pParent的平衡因子为2或者-2，分以下情况考虑

   1. pParent的平衡因子为2，说明pParent的右子树高，设pParent的右子树的根为pSubR
      ​         当pSubR的平衡因子为1时，执行左单旋
      ​         当pSubR的平衡因子为-1时，执行右左双旋
   2. pParent的平衡因子为-2，说明pParent的左子树高，设pParent的左子树的根为pSubL
      ​         当pSubL的平衡因子为-1是，执行右单旋
      ​         当pSubL的平衡因子为1时，执行左右双旋

   旋转完成后，原pParent为根的子树高度降低，已经平衡，不需要再向上更新。

4. 要想加深对旋转的理解，多思考思考抽象图即可，有兴趣再画几个具象图出来（实例的AVL树）

# 完整实现代码

[AVL](https://github.com/DaysOfExperience/data_structure_and_STL/tree/main/data_structure)

以上除了插入和旋转代码，还包含AVL树的测试代码（是否符合AVL树的规则，用于自检）。
AVL树的删除略了，或许某一天会再遇见。
查找就是普通二叉搜索树的查找，没什么不同。

# AVL树的性能

AVL树是一棵绝对平衡的二叉搜索树，其要求每个节点的左右子树高度差的绝对值都不超过1，这样可以保证查询时高效的时间复杂度，即log_2 (N)

**但是如果要对AVL树做一些结构修改的操作，性能非常低下，比如：插入时要维护其绝对平衡，旋转的次数比较多，更差的是在删除时， 有可能一直要让旋转持续到根的位置。**
因此：如果需要一种查询高效且有序的数据结构，而且数据的个数为静态的(即不会改变)，可以考虑AVL树，

**但如果一个结构经常修改，AVL树就不太适合。**

因此产生了红黑树。