# 一. unordered_map unordered_set 和 map set的区别

1. map set底层采取的红黑树的结构，unordered_xxx 底层数据结构是哈希表。unordered_map容器通过key访问单个元素要比map快，但它通常在遍历元素子集的范围迭代方面效率较低。

2. Java中对应的容器名为 HashMap HashSet TreeMap TreeSet，命名方面比C++好了很多。主要是早期C++并没有实现哈希结构的容器（C++11之前），也就是unordered系列，在C++11中新增了unordered_map，unordered_set，unordered_multimap，unordered_multiset，故因为历史命名问题，取了这样的名字。

3. 它们的使用大体上几乎一致。显著的差别是：
    a、map和set为双向迭代器，unordered_xxx和是单向迭代器。
    b、map和set存储为有序存储（红黑树结构，中序遍历有序），unordered_xxx为无序存储（哈希表的结构致使）

4. 性能差异：采取哈希表的unordered系列容器在大量数据的增删查改效率更优，尤其是查（搜索）

# 二. 