### Question 541 Reverse String II

![image-20230430151232122](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230430151232122.png)

其实这道题目的中心题目就是，每隔2k个字符，反转前面k个字符，只需要每隔2k的字符，对前面的k个字母施展一次reverse操作就好了，上代码

```
class Solution {
    public String reverseStr(String s, int k) {
        char[] array = s.toCharArray();
        for(int i = 0; i < s.length(); i += 2 * k) {
            reverse(i, i + k - 1, array);
        }
        return String.valueOf(array);
    }
    
    public void reverse(int i, int j, char[] array) {
        if (j >= array.length) {
            j = array.length - 1;
        }
        while (i < j) {
            char c = array[i];
            array[i] = array[j];
            array[j] = c;
            i++;
            j--;
        }
    }
}
```

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        left = 0
        ans = list(s)
        while left < len(s):
            end = left + k - 1
            start = left
            if end >= len(s):
                end = len(s) - 1
            while start < end:
                c = ans[start]
                ans[start] = ans[end]
                ans[end] = c
                start += 1
                end -= 1
            left = left + k + k
        return ''.join(ans)

```

