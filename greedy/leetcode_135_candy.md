### Question 135 Candy

![image-20230523114917995](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230523114917995.png)

这道题目也是比较抽象的一道题，解题的关键最在于我们先确保，假设rating更高的情况下，每一个孩子都大于它的左孩子，在通过遍历，确保，每一个孩子都大于它的右孩子，如果它的rating更高的话

```java
class Solution {
    public int candy(int[] ratings) {
        int[] allocate = new int[ratings.length];
        Arrays.fill(allocate, 1);
      // 左侧遍历，确保大于左孩子
        for(int i = 1; i < ratings.length; i++) {
            if (ratings[i] > ratings[i - 1]) {
                allocate[i] = allocate[i - 1] + 1;
            }
        }
      // 右侧遍历，从倒数第二个开始，确保大于右孩子
        for(int i = allocate.length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
              // 这里的话稍微解释一下，我们这里有两个选项，allocate[i]是让当前的数量大于左孩子，allocate[i + 1]是让当前的数量大于右孩子，我们需要选择其中一个，所以选择大的才行
                allocate[i] = Math.max(allocate[i], allocate[i + 1] + 1);
            }
        }
        return IntStream.of(allocate).sum();
    }
}
```

