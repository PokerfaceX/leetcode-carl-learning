### Question 763 Partition Labels

![image-20230527231058684](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230527231058684.png)

这道题目有个trick，就是在遍历过程中，我们需要不断的更新字符出现的最大的范围，拿下面的举例子，我们不断的更新要找的最大范围，当i==8的时候，就囊括了所有最大范围为5和7的数值，所以可以成功找到一个范围

![image-20230527231559391](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230527231559391.png)

```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        List<Integer> ans = new ArrayList<>();
        int[] array = new int[26];
      // 统计每个字符的最远出现下标
        for(int i = 0; i < s.length(); i++) {
            array[s.charAt(i) - 'a'] = i;
        }
        int left = 0, right = 0;
        for(int i = 0; i < s.length(); i++) {
            char letter = s.charAt(i);
          // 不断更新可以囊括一个partition的最远下标
            right = Math.max(right, array[letter - 'a']);
            if (i == right) {
              // 当i等于right的时候就说明找到了一个范围了
                ans.add(right - left + 1);
                left = right + 1;
            }
        }
        return ans;
    }
}
```

