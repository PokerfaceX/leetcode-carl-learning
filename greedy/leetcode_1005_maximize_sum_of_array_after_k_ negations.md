### Question 1005 Maximize Sum Of Array After K Negations

![image-20230521234721850](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230521234721850.png)

这道题目其实也用到了贪心的思想，我们想找到最大的数组和，可以总共反转k次，一个数字可以被反转多次，那么其实，这道题目，需要用到两次贪心的思想

- 局部最优1：在可能的情况下，让所有的负数都反转成正数
- 局部最优2：在可能的情况下，若是所有数字为正，就一直来回反转数组里面**影响**最小的数字

上代码解释，我一开始是这么写的

```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        int used = 0;
        Arrays.sort(nums);
        for(int i = 0; i < nums.length && used < k; i++) {
          // 找出所有的负数，从最负的开始一个个反转
            if (nums[i] < 0) {
                nums[i] = -1 * nums[i];
                used++;
            }
        }
      // 因为负数可能被反转了，就需要在sort一次，来找到数组最小值
        Arrays.sort(nums);
        for(; used < k; used++) {
          // 反转n次
            nums[0] = -1 * nums[0];
        }
        return Arrays.stream(nums).sum();
    }
}
```

但是看了下卡哥的代码，觉得优雅很多，但是看了很多stream的知识点

```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
      // boxed会把IntStream变成一个Stream<Integer>
        nums = IntStream.of(nums).boxed()
      // 只有先变为Stream<Integer>才能使用sorted方法
        .sorted((o1, o2) -> Math.abs(o2) - Math.abs(o1))
         // 注意这里的区别，如果是map方法，就会返回一个Stream<Integer>，那toArray就会返回一个Object数组
      // mapToInt就会返回一个IntStream，toArray会返回int[] 
        .mapToInt(Integer::intValue)
        .toArray();
        for(int i = 0; i < nums.length; i++) {
            if (nums[i] < 0 && k > 0) {
                nums[i] = nums[i] * -1;
                k--;
            }
        }
      // 如果K还大于0，那么反复转变数值最小的元素，将K用完
        for(; k > 0; k--) {
            nums[nums.length - 1] = nums[nums.length - 1] * -1;
        }
      // Arrays.stream先返回一个IntStream然后sum就会返回和，只有IntStream才能这么做
        return Arrays.stream(nums).sum();
    }
}
```

这上面主要的想法是说，我们在找负数的时候，直接从一个根据绝对值从大到小排列的数组里面去找，第二次反转最小数值的时候就直接反转数组最右侧的最小值就可以了
