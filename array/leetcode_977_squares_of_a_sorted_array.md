### Question 977 Squares of a Sorted Array

一开始的时候想到了应用双指针法，但是没有想到是两头各放一个指针！

题目截图

![image-20230415153708640](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230415153708640.png)

**暴力法的话时间复杂度为O(n) + O(n*log(n))，在这里我们不予考虑**

题目的唯一难点就是负数的处理，在这里使用两个指针left, right，原因是在新数组里面最大的值，要么是原数组最左侧数字的平方，要么是原数组最右侧数字的平方，那么逻辑就清晰了

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int left = 0, right = nums.length - 1;
        int k = nums.length - 1;
        int[] array = new int[nums.length];
        
        // 唯一需要一些思索的点就是这个"小于等于"，因为原数组里所有数值的平方都应该被放到新数组里，我使用了<=而不是<
        while (left <= right) {
            if (nums[left] * nums[left] > nums[right] * nums[right])  {
                array[k--] = nums[left] * nums[left];
                left++;
            } else {
                array[k--] = nums[right] * nums[right];
                right--;
            }
            
        }
        return array;
    }
}
```



```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        answer = []
        left, right = 0, len(nums) - 1
        while left <= right:
            leftSquare = nums[left] ** 2
            rightSquare = nums[right] ** 2
            if leftSquare > rightSquare:
                answer.insert(0, leftSquare)
                left += 1
            else:
                answer.insert(0, rightSquare)
                right -= 1
        return answer
```



 这里用了insert方法，可以插入到任意位置，然后那个位置以及后面的所有数字都会往后移动一格