### Question 1 Two Sum

![image-20220908224719833](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220908224719833.png)

这道题目算得上是最经典的题目了，也是必做题。其实比较核心的逻辑就是，我们定义一个哈希表，这个哈希表可以存储nums的数值和它的下标，若是target - nums[i] 曾经在数组里面出现过的话，就说明找到了两数之和。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> ans = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            if (ans.containsKey(target - nums[i])) {
                return new int[]{i, ans.get(target - nums[i])};
            }
            ans.put(nums[i], i);
        }
        return new int[2];
    }
}
```

