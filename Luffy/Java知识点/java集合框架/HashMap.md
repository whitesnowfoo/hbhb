HashTable

HashMap的容量，默认是16
```java
 /**
     * The default initial capacity - MUST be a power of two.
     */
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

 /**
     * The load factor used when none specified in constructor.
     */
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
```

   
HashMap的加载因子，默认是0.75
当HashMap中元素数超过容量*加载因子时，HashMap会进行扩容。



拉链法
HashMap使用拉链法管理其中的每个节点。

由Node节点组成链表之后，HashMap定义了一个Node数组：

transient Node<K,V>[] table;


如果HashMap初始化的时候指定了容量，HashMap会把这个容量修改为2的倍数，然后创建对应长度的table。


1、当节点长度（链表长度）大于8 并且数组长度大于64时候，则将链表转换成为红黑树


reeifyBin()方法就是链表转红黑树

关于TreeNode
当HashMap把链表转为红黑树的时候，原来的Node节点就会被转为TreeNode节点，TreeNode也是HashMap中定义的内部类，定义大概是这样的：

红黑树--平衡二叉树

红黑树基础
红黑树是一种近似平衡的二叉查找树，他并非绝对平衡，但是可以保证任何一个节点的左右子树的高度差不会超过二者中较低的那个的一倍。

红黑树有这样的特点：

1，每个节点要么是红色，要么是黑色。

2，根节点必须是黑色。叶子节点必须是黑色NULL节点。

3，红色节点不能连续。

4，对于每个节点，从该点至叶子节点的任何路径，都含有相同个数的黑色节点。

5，能够以O(log2(N))的时间复杂度进行搜索、插入、删除操作。此外,任何不平衡都会在3次旋转之内解决。
