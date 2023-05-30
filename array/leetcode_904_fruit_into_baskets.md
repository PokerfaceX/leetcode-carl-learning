### Question 904 Fruit into Baskets

![image-20230416091526894](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230416091526894.png)

这也是一道滑动窗口的题，我们不断的滑动当前的窗口，一直往窗口里面加入数值，每次加入之后，在看这个map里面是不是只有两个key，如果多于两个key，就不断的移除，指导满足这个窗口的条件位置，也就是两个key



```python
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        count = collections.defaultdict(int)
        left, total, res = 0, 0, 0
        for right in range(len(fruits)):
            count[fruits[right]] += 1
            total += 1
            while len(count) > 2:
                f = fruits[left]
                count[f] -= 1
                total -= 1
                left += 1
                if not count[f]:
                    count.pop(f)
            res = max(res, total)
        return res
```

