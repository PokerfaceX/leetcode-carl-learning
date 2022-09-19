### Question 454 4Sum II

![image-20220908225104376](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220908225104376.png)

一开始看到这个题目，有点发懵，但是仔细看题，会发现，这里并没有在乎重复的下标，也就是说，要找的是所有的排列，并不需要在意任何独特性。而且更加好的一点是，这里并不需要找出具体的排列，只需要找出总共有多少种排列就好。

那么，可以先定义一个map，用来发现nums1和nums2里面的所有可能的和与出现的次数。

在循环num3和nums4的过程中，找出0 - nums3[i] - nums4[j]所出现的次数

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        int count = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i: nums1) {
            for(int j: nums2) {
                if (map.containsKey(i + j)) {
                    map.put(i + j, map.get(i + j) + 1);
                } else {
                    map.put(i + j, 1);
                }
            }
        }
        for(int i: nums3) {
            for(int j: nums4) {
                if (map.containsKey(0 - i - j)) {
                    count += map.get(0 - i - j);
                }
            }
        }
        return count;
        
    }
}
```

