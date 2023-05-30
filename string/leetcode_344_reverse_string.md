### Question 344 Reverse String

![image-20230430134051268](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230430134051268.png)

这道题目实在是经典中的经典，刚开始学1511的时候就碰到过无数次字符串反转的题目

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s) - 1
        while left < right:
            c = s[left]
            s[left] = s[right]
            s[right] = c
            left += 1
            right -= 1
        return s
```

