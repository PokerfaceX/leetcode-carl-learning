### Question 541 Reverse String II

![image-20220911192011380](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220911192011380.png)

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

