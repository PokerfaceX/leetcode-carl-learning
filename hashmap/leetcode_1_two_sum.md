### Question 1 Two Sum

![image-20230429214706156](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230429214706156.png)

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

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        record = dict()
        for index, value in enumerate(nums):#返回一个enumerate对象
            if target - value in record:
                return [index, record[target - value]]
            record[value] = index
        return []
```

