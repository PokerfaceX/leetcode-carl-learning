### Question 383 Ransom Note

![image-20220910205337881](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220910205337881.png)

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

