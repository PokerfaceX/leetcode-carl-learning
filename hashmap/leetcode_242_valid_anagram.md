### Question 242 Valid Anagram

![image-20230427221620252](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230427221620252.png)

这道题目算是非常简单的了，我们只需要定义一个长度为26的数组，记录下每一个字母出现的次数就好

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] array = new int[26];
        for(int i = 0; i < s.length(); i++) {
            int index = s.charAt(i) - 'a';
            array[index]++;
        }
        // 遍历t时，递减array数组的元素，简单来说就是把array里面的所有的元素都给减回去
        for(int i = 0; i < t.length(); i++) {
            int index = t.charAt(i) - 'a';
            array[index]--;
        }
        // 如果出现的次数有任何一个不是0，就说明不是相同的字符组成的字符串
        for(int i = 0; i < 26; i++) {
            if (array[i] != 0) {
                return false;
            }
        }
        return true;
        
    }
}
```

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        map1, map2 = {}, {}
        for c in s:
            if c not in map1:
                map1[c] = 1
            else:
                map1[c] += 1
        for c in t:
            if c not in map2:
                map2[c] = 1
            else:
                map2[c] += 1
        return map1 == map2
```

