### Question 125 Valid Palindrome

![image-20220902190210274](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220902190210274.png)

一道熟悉的不能在熟悉的题目，学校1511期间就曾经接触过，只需要用双指针来陆续观看左右字符是否相等，只不过这道题目的**non-alphanumeric**有点坑人，其实要保留的是所有字母**和**数字

上代码

~~~java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuffer sBuffer = new StringBuffer();
        for(char c: s.toCharArray()) {
            if (Character.isLetter(c) || Character.isDigit(c)) {
                sBuffer.append(Character.toLowerCase(c));
            }
        }
        int left = 0, right = sBuffer.length() - 1;
        while (left < right) {
            if (sBuffer.charAt(left) != sBuffer.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
~~~

