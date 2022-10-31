### Question 501 Find Mode in Binary Search Tree

![image-20221026213308592](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221026213308592.png)

这道题目的话，我一开始想过用map单纯的做统计，但是后来觉得这样做浪费了BST的特性，然后试着用中序遍历去解决问题。但是在后来还是发现，因为mode可以是多个数值，还是得用map来记录下每个节点出现的频率

```java
class Solution {
    
    List<Integer> ans = new ArrayList<>();
    Map<TreeNode, Integer> map = new HashMap<>();
    int maxFrequency = Integer.MIN_VALUE;
    int currFrequency = 0;
    int prevNumber = -1;
    
    public int[] findMode(TreeNode root) {
        dfs(root);
        for(TreeNode node: map.keySet()) {
            if (map.get(node).equals(maxFrequency)) {
                ans.add(node.val);
            }
        }
        return ans.stream().mapToInt(i -> i).toArray();
    }
    
    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        if (root.val == prevNumber) {
            currFrequency++;
        } else {
            prevNumber = root.val;
            currFrequency = 1;
        }
        map.put(root, currFrequency);
        if (currFrequency > maxFrequency) {
            maxFrequency = currFrequency;
        }
        dfs(root.right);
    }
}
```



看了卡哥的代码，恍然大悟，其实不需要用map，在maxFrequency更新的时候，可以直接把list清空。当currFrequency和max相等的时候，我们可以直接放进list

~~~java
class Solution {
    
    TreeNode prev = null;
    int currFrequency = 0;
    int maxFrequency = 0;
    List<Integer> ans = new ArrayList<>();
    
    public int[] findMode(TreeNode root) {
        dfs(root);
        return ans.stream().mapToInt(i -> i.intValue()).toArray();// 这里的话得用mapToI
        
    }
    
    public void dfs(TreeNode curr) {
        if (curr == null) {
            return;
        }
        dfs(curr.left);
        if (prev != null && curr.val == prev.val) {
            currFrequency++;
        } else if (prev != null && curr.val != prev.val) {
            currFrequency = 1;
        } else if (prev == null) {
            currFrequency = 1;
        }
        prev = curr;
        // 这里进行清空操作
        if (currFrequency > maxFrequency) {
            maxFrequency = currFrequency;
            ans.clear();
            ans.add(curr.val);
        // 关键一步，因为当maxFrequency的时候会进行清空，所以只要等于maxFreuquency就直接先加进去
        } else if (currFrequency == maxFrequency) {
            ans.add(curr.val);
        }
        dfs(curr.right);
    }
}
~~~

