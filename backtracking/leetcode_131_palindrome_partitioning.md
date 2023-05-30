### Question 131 Palindrome Partitioning

![image-20230513185725778](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230513185725778.png)

这道题目是一道蛮复杂的题目了，但是确实是可以用回溯解决的一道经典的题目。可以看到以下的树形结构，!![image-20230513185752663](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230513185752663.png)

其实这道题目的中心思想就是，每次遍历我们都是查看从startIndex到i的子串，看看他们是不是palindrome，如果是的话就加入进去，在递归，不是的话就continue然后继续在当前层查找，可以看到所有的叶子节点都是应该添加到最终答案的选项

```java
class Solution {

    StringBuffer sb = new StringBuffer();
    List<String> path = new ArrayList<>();
    List<List<String>> ans = new ArrayList<>();


    public List<List<String>> partition(String s) {
        traversal(s, 0);
        return ans;
    }

    public void traversal(String s, int startIndex) {
      // 只有到了叶子节点，也就是startIndex指针遍历到了最后面就说明当前的path肯定是一个答案，因为如果不是的话早就被回溯上去了
      if (startIndex >= s.length()) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = startIndex; i < s.length(); i++) {
          // 这里的话算是一个剪枝操作，只有当这个是一个回文子串的时候才会加入到path中，而且这里得continue而不是break，因为例子"efe"中，“ef”不是回文子串但是“efe”是，我们不应该跳过所有的情况
            if (!isPalindrome(s, startIndex, i)) {
                continue;
            }
            path.add(s.substring(startIndex, i + 1));
            traversal(s, i + 1);
            path.remove(path.size() - 1);
        }
    }

    public boolean isPalindrome(String s, int start, int end) {
        while (start < end) {
            if (s.charAt(start) != s.charAt(end)) {
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
}
```
