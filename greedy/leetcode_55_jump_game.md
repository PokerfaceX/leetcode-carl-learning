### Question 55 Jump Game

![image-20230521001138444](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230521001138444.png)

其实这道题目我一开始想复杂了，一开始想的是对于每一步而言，我就使劲往前走，只要能到最后一个节点就行，但是像是这种情况[2，5，0，0]，会忽视掉5这个格子



所以依照贪心的想法，我们不断的遍历，对于每一次节点，我们都要找到能达到的最大范围，只要能够到最后一个节点，就返回true

```java
class Solution {
    public boolean canJump(int[] nums) {
        int cover = 0;
      // 注意，这里得遍历cover，你只应该在能遍历的到的范围内遍历
      // 如果遍历的是num array的话永远都能返回true
        for(int i = 0; i <= cover; i++) {
            int jumpIndex = i + nums[i];
          // 这里的话得不断的对比cover，因为像是这种情况[1,3,1,1,0]，我们在第二个格子记录的能达到的最远范围应该被记录下来
            cover = Math.max(cover, jumpIndex);
            if (cover >= nums.length - 1) {
                return true;
            }
        }
        return false;
    }
}
```

