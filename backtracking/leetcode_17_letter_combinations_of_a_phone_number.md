### Question 17 Letter Combinations of a phone number

![image-20221105213350419](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221105213350419.png)

这道题目有思路，但是确实是看了卡哥的代码才知道怎么写的，但是和leetcode_77和leetcode_216相比，有了一些不同，不同的就是每一次遍历的字符串不一样了

我认为关键有两步骤，一个是用一个数据结构来记录下键盘的对应关系，一个就是解决index的问题，一开始分不太清楚，传进traversal方法里面的index是指的键盘的index还是键盘对应的string的index

```java
class Solution {

    String[] array = {
        "",
        "",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz"
    };

    List<String> ans = new ArrayList<>();

    StringBuffer sb = new StringBuffer();

    public List<String> letterCombinations(String digits) {
        if (digits.equals("")) {
            return ans;
        }
        traversal(digits, 0);
        return ans;
    }

    public void traversal(String digits, int digitIndex) {
        if (sb.length() == digits.length()) {
            ans.add(sb.toString());
            return;
        }
        // 键盘的index
        int buttonIndex = digits.charAt(digitIndex) - '0';
        // 当前要遍历的string
        String buttonString = array[buttonIndex];
        for(int i = 0; i < buttonString.length(); i++) {
            sb.append(buttonString.charAt(i));
            traversal(digits, digitIndex + 1);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```

![image-20221105213744431](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221105213744431.png)

