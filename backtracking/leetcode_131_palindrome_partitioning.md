### Question 131 Palindrome Partitioning

![image-20221108225642103](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221108225642103.png)

这道题目是一道蛮复杂的题目了，但是确实是可以用回溯解决的一道经典的题目。可以看到以下的树形结构，![image-20221108225758881](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221108225758881.png)

可以看到每一个叶子节点其实都是一个可以出现的分割后的字符串，上面有4种情况，第二个没画出来不过是可以感受到通过纵向遍历是可以找到所有分割后的字符串的。

下面的代码比较关键的一步就是，每一次分割，我们看的都是[startIndex, i]区间的字符串。看第一层，是不是a, aa, aab

```java
class Solution {

    List<String> path = new ArrayList<>();
    List<List<String>> ans = new ArrayList<>();

    public List<List<String>> partition(String s) {
        traversal(s, 0);
        return ans;
    }

    public void traversal(String s, int startIndex) {
        if (startIndex >= s.length()) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = startIndex; i < s.length(); i++) {
            // 算是剪枝操作，如果当前字字符串是回文就加入到path
            if (this.isPalindrome(s, startIndex, i)) {
                // 比较关键的一步
                path.add(s.substring(startIndex, i + 1));
            } else {
                // 如果不是回文字符串压根就不会被加入到path所以也不需要回溯，直接continue就好
                continue;
            }
            traversal(s, i + 1);
            path.remove(path.size() - 1);
        }
    }
	
    public boolean isPalindrome(String s, int start, int finish) {
        int i = start;
        int j = finish;
        while (i < j) {
            char c1 = s.charAt(i);
            char c2 = s.charAt(j);
            if (c1 != c2) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

上面的基本是按照卡哥的代码写的，但是其实我自己也写了一个简单更容易理解的版本

```java
class Solution {
    
    List<String> path = new ArrayList<>();
    List<List<String>> ans = new ArrayList<>(); 
    
    public List<List<String>> partition(String s) {
        traversal(s, 0);
        return ans;
    }

    public void traversal(String s, int startIndex) {
        if (startIndex >= s.length()) {
            boolean flag = true;
            // 到最后再看看当前path里面的字符串是不是都是回文串
            for(String a: path) {
                if (!isPalindrome(a, 0, a.length() - 1)) {
                    flag = false;
                    break;
                }
            }
            if(flag) {
                ans.add(new ArrayList<>(path));
            }
            return;
        }
        for(int i = startIndex; i < s.length(); i++) {
            // 每次都是直接加入path，忽略是不是回文
            path.add(s.substring(startIndex, i + 1));
            traversal(s, i + 1);
            path.remove(path.size() - 1);
        }
    }

    public boolean isPalindrome(String s, int start, int finish) {
        int i = start;
        int j = finish;
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

上面我写的代码也是可以通过的，但是效率非常的低，因为没有进行任何的剪枝操作，完全是2^n的时间复杂度，没有任何优化
