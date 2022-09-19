### Question 76 Minimum Window Substring

![image-20220628173203664](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220628173203664.png)



一道偏难的leetcode题目，一开始看到题目的标题可能就会想到滑动窗口，且这种找字符串子串的题目，基本都会用到hashmap。但是一开始可能想不到很好的思路，若是采用暴力遍历法，那么获得所有字串需要的时间为O(n<sup>2</sup>)，每一次还需要对比哈希表，那么时间复杂度直接就成了O(n<sup>3</sup>)，时间复杂度太高，直接不予考虑。

直接上代码来解释

```java
class Solution {
    public String minWindow(String s, String t) {
        //一个哈希表用来存储t字符串，一个用来存储当前窗口的字符
        Map<Character, Integer> tMap = new HashMap<>();
        Map<Character, Integer> windowMap = new HashMap<>();
         
        for(char c: t.toCharArray()) {
            tMap.put(c, tMap.getOrDefault(c, 0) + 1);
        }
        //举个例子，若是tMap里有a=1,b=2, c =3，而windowMap有a=2,b=1那么have就是1，have变量就是检查有多少字符达到了覆盖t的要求
        int need = tMap.size(), have = 0;
        int left = 0, right = 0;
        int maxSize = Integer.MAX_VALUE;
        int start = -1, end = -1;
        while (right < s.length()) {
            char c = s.charAt(right);
            if (tMap.containsKey(c)) {
                windowMap.put(c, windowMap.getOrDefault(c, 0) + 1);
                if (windowMap.get(c).equals(tMap.get(c))) {
                    have++;
                }
            }
            while(have == need) {
                if (right - left + 1 < maxSize) {
                    maxSize = right - left + 1;
                    start = left;
                    end = right;
                }
                char c2 = s.charAt(left);
                if (tMap.containsKey(c2)) {
                    windowMap.put(c2, windowMap.getOrDefault(c2, 0) - 1);
                    if (windowMap.get(c2).compareTo(tMap.get(c2)) < 0) {
                        have--;
                    }
                }
                left++;
            }
            right++;
        }
        return maxSize == Integer.MAX_VALUE ? "" : s.substring(start, end + 1);
    }
}
```

这里额外插一句，在进行Integer的大小比较的时候，需要使用equals方法，否则过不去几个特殊情况，原因涉及到jvm以及封装问题，这里就不展开了。另外因为这里用的都是Integer，为了严谨，使用了Integer自带的compareTo方法。