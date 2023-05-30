## 二叉树基础知识

| 二叉树的种类                                        |
| --------------------------------------------------- |
| 完美二叉树/ 满二叉树(Perfect Binary Tree)           |
| 完全二叉树(Complete Binary Tree)                    |
| 完满二叉树(Full Binary Tree， Strictly Binary Tree) |
| 二叉搜索树(Binary Search Tree)                      |
| 平衡二叉搜索树                                      |



### 完美二叉树/满二叉树, Perfect Binary Tree

所有的叶子节点都在同一层，并且所有非叶子节点的度数为2

#### ![image-20230504185619007](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230504185619007.png)

### 完全二叉树, Complete Binary Tree

在完全二叉树中，除了最底层的节点可能没有填满以外，其他的层数都填满了，并且所有的叶子节点全部向左对对齐，均是集中在最左边的若干位置

![image-20230504185700164](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230504185700164.png)

在之前leetcode347里面所用的堆就是一个完全二叉树(complete binary tree)，只不过父子节点之间是有着顺序关系的



### 完满二叉树, Full Binary Tree

在完满二叉树(Full Binary Tree)中，所有非叶子结点的度数为2，也就是说对于当前节点而言，只要有孩子节点，那么必定有2个子节点

![image-20230504185801409](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230504185801409.png)

### 二叉搜索树, Binary Search Tree

前面介绍的树，都没有数值的，而二叉搜索树是有数值的了，**二叉搜索树是一个有序树**。

- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
- 它的左、右子树也分别为二叉排序树

![image-20220919123640466](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919123640466.png)

### 平衡二叉搜索树，Balanced Binary Search Tree/ AVL Tree

平衡二叉搜索树：是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

![image-20230504185843420](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230504185843420.png)







## 二叉树的存储方式

![image-20220919123936566](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919123936566.png)

![image-20220919123958569](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919123958569.png)



## 二叉树的遍历方式

跟图论一样，二叉树也有两种遍历方式，分别为DFS和BFS，从这里进行了一些扩展，才出现了专属于树的遍历方法。

- 深度优先搜索(DFS)
  - 前序遍历 -> 中左右
  - 中序遍历 -> 左中右
  - 后序遍历 -> 左右中
- 广度优先搜索(BFS)
  - 层次遍历



在DFS的三种扩展里面，"中"，其实指的就是**处理逻辑**，左和右指的就是左子树和右子树。



![image-20220919124844562](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919124844562.png)

- 在上面的中序遍历里面，我们先看左子树，在看左子树的左子树，直到碰到null为止，在开始读取数值1，这时候读取中间值4，再读取右子树的数值2，在读取中间数值5，再看右侧的最左侧子树7，中间节点6， 右子树8

我们做二叉树相关题目，经常会使用递归的方式来实现深度优先遍历，也就是实现前中后序遍历，使用递归是比较方便的。**栈其实就是递归的一种实现结构**，也就说前中后序遍历的逻辑其实都是可以借助栈使用非递归的方式来实现的。



而一般BFS的遍历方式往往需要用到队列来实现，也是因为队列先进先出的特点，才能帮助我们实现二叉树的层序遍历。



**深度**：根节点到一个节点的距离，depth

**高度**:  从一个节点到叶子节点的最远距离，height



**https://www.cnblogs.com/idorax/p/6441043.html**