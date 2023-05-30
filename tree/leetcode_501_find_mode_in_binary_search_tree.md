### Question 501 Find Mode in Binary Search Tree

![image-20221026213308592](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221026213308592.png)

这道题目的话，我一开始想过用map单纯的做统计，但是后来觉得这样做非常的麻烦，而且没有啥挑战性，只是单纯的统计了每一个节点的个数，然后通过map找到最大值

随后想到了卡哥的双指针遍历，试着用中序遍历去解决问题，一边用一个prev指针来指向前面的数值，一边用curr遍历，就能遍历一次二叉树找到mode而且不用额外的空间来记录

```java
class Solution {
    int currFrequency = 0;
    int maxFrequency = Integer.MIN_VALUE;
    List<Integer> modes = new LinkedList<>();
    TreeNode prev = null;

    public int[] findMode(TreeNode root) {
        dfs(root);
      // 把list转换为int array的标准写法
        return modes.stream().mapToInt(a -> Integer.valueOf(a)).toArray();
    }

    public void dfs(TreeNode curr) {
        if (curr == null) {
            return;
        }
        dfs(curr.left);
      	// 这里当prev为null curr不为null就是找到了最左侧的数值，那么frequency肯定是1
        if (this.prev == null) {
            this.currFrequency = 1;
        } else {
          	// 当前一个数值和当前数值不一样就肯定说明当前frequency是1
            if (this.prev.val != curr.val) {
                this.currFrequency = 1;
            } else {
               // 一样的话就添加
                this.currFrequency += 1;
            }
        }
      // 如果当前的次数等于目前已知的最大次数那么就要加入list中，如果大于已知最大次数就要清空结果，然后在加入到结果中
        if (this.currFrequency == maxFrequency) {
            this.modes.add(curr.val);
        } else if (this.currFrequency > maxFrequency) {
            maxFrequency = this.currFrequency;
            this.modes.clear();
            this.modes.add(curr.val);
        }
      // prev和curr来同步
        prev = curr;
        dfs(curr.right);
  
    }
}
```



这里的话就是看起来简洁一点

~~~java
class Solution {
    int currFrequency = 0;
    int maxFrequency = Integer.MIN_VALUE;
    List<Integer> modes = new LinkedList<>();
    TreeNode prev = null;

    public int[] findMode(TreeNode root) {
        dfs(root);
        return modes.stream().mapToInt(a -> Integer.valueOf(a)).toArray();
    }

    public void dfs(TreeNode curr) {
        if (curr == null) {
            return;
        }
        dfs(curr.left);
        if (this.prev == null || this.prev.val != curr.val) {
            this.currFrequency = 1;
        } else {
            this.currFrequency += 1;
        } 
        if (this.currFrequency == maxFrequency) {
            this.modes.add(curr.val);
        } else if (this.currFrequency > maxFrequency) {
            maxFrequency = this.currFrequency;
            this.modes.clear();
            this.modes.add(curr.val);
        }
        prev = curr;
        dfs(curr.right);
  
    }
}
~~~

