### Question 383 Ransom Note

![image-20230429230532509](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230429230532509.png)

非常简单的题目，一开始是用了hashmap来记录magazine里面各个字母出现的次数，但是后来题目说到只会出现小写的英文字母，所以优化了下空间，用个array记录次数

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] array = new int[26];
        for(char c: magazine.toCharArray()) {
            array[c - 'a']++;
        }
        for(char c: ransomNote.toCharArray()) {
            if (array[c - 'a'] <= 0) {
                return false;
            }
            array[c - 'a']--;
        }
        return true;
    }
}
```

```python
from collections import defaultdict

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        map = defaultdict(int)
        for c in magazine:
            map[c] += 1
        for c in ransomNote:
            if map[c] == 0:
                return False
            map[c] -= 1
        return True
```

