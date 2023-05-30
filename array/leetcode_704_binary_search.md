### Question 704 Binary Search

二分查找看起来不难，但是其实难就难在他的边界判定上，这里一律使用**左闭右开**原则

![image-20230228224557592](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230228224557592.png)



*** **

```java
while (left < right) {
    // 无论中位数是大了还是小了，都说明他不是正确的数值，不是我们要找的target
    // 假设target是在左侧区域，right就应该等于我们之前的中位数下标，我们的右侧数组里应该包含一个"invalid"的数值，用来满足右开的原则。这里因为之前的中位数不是我们要找的数值，可以把这个数值当成一个延申(左闭右开)，用来满足"开"
    // 假设target是在右侧区域，left就应该等于我们的中位数下标+1,记住，我们是使用左闭右开原则，数组的左侧所包含的数值理论上都有可能是我们要找的target，所以left= mid + 1, 这里满足了"闭"原则
    
	if (array[mid] > target) {
		// 中位数太大，所以在左侧区域
		right = mid; // 
	} else if (array[mid] < target) {
        // 中位数太小，所以在右侧区域
		left = mid + 1; 
	} else if (array[mid] == target) {
		return mid;
	}
}
```

*****



```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length;
        while (left < right) {
            int mid = (left + right) / 2;
            if (target < nums[mid]) {
                right = mid;
            } else if (target > nums[mid]) {
                left = mid + 1;
            } else {
                return mid;
            }
        }
        return -1;
    }
}
```



```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)

        while left < right:
            mid = (left + right) // 2 # 如果用/ 而不是 //就会返回一个float数值
            if nums[mid] > target:
                right = mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
        return -1
```

