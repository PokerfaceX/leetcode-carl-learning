### Question 968 Binary Tree Cameras

![image-20230530222018848](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230530222018848.png)

非常难的一道题目，没看讲解根本不可能想得到

解题思路是啥？

- 我们从底下网上看，我们不可能把摄像头放在叶子节点，因为那样的话就会造成摄像头的浪费
- 我们从叶子节点的父节点开始，每隔两个节点就放一个摄像头，就差不多能全部覆盖了，这就是我们的局部最优，然后我们需要用到节点状态

节点状态是什么鬼？

- 除了主函数之外，我们会定义一个traversal的函数，来找到需要的摄像头数量，但是同时这个函数也会返回每一个节点的状态，**有三种**
  - 用1来表示，这个节点没有被摄像头覆盖
  - 用2来表示，这个节点上已经有摄像头了
  - 用3来表示，这个节点已经被一个摄像头覆盖了
  - 注意，不会有当前**没有摄像头**这么一个状态，因为当没有摄像头的时候，要么被覆盖，要么没有

- 用节点状态来评估左右孩子节点，来判断对当前节点我们应该怎么做

上代码

```java
class Solution {

    int result;

    public int minCameraCover(TreeNode root) {
        int statusAtRoot = traversal(root);
      // 对于最初的根节点而言，如果没有被覆盖，那么就应该放一个摄像头，因为根节点没有父亲节点放摄像头了
        if (statusAtRoot == 0) {
            this.result++;
        }
        return this.result;
    }

    /**
        i == 0, not covered
        i == 1, have a camera
        i == 2, already covered

    */
    public int traversal(TreeNode root) {
      // 对于一个null节点而言，我们直接说他是被覆盖就行，想象一个叶子节点，他的左右孩子都是null，如果我们把null节点状态定义成有摄像头，那么叶子节点就会被判断成被覆盖了，那么叶子节点的父亲节点我们也不会放摄像头
      // 如果断言成没有被覆盖，那么就要在叶子节点放摄像头，很明显，这一点都不贪心，所以只能当成覆盖来对待
        if (root == null) {
            return 2;
        }
      // 后续遍历
        int left = traversal(root.left);
        int right = traversal(root.right);
      // 想象一个，不管怎么样，如果左右孩子都是被覆盖的转台，那么当前可以没必要放摄像头，而且当前也不可能被覆盖(左右没有摄像头，父亲节点还没遍历回去呢)，所以必须说是没有被覆盖
      // 情况1
      // 左右节点都有覆盖
        if (left == 2 && right == 2) {
            return 0;
        }
      // 情况2
      // 左右孩子，只要有一个没有被覆盖，就应该放一个摄像头
        if (left == 0 || right == 0) {
            this.result++;
            return 1;
        }
      // 情况3
      // 左右孩子，只要有一个摄像头，是不是就说明当前被覆盖了，对不对，问问自己
        if (left == 1 || right == 1) {
            return 2;
        }
      // 这个return就无所谓了，不可能到这里
        return -1;
    }
}
```

上面的主函数里面的if语句，这里在多一嘴，把图贴过来解释一下，其他三种情况，最好直接看卡哥的笔记

`![image-20230530223704645](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230530223704645.png)