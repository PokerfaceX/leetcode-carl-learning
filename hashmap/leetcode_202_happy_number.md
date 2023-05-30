### Question 202 Happy Number

![image-20230429213421345](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230429213421345.png)

这道题目，一开始的时候其实有点发懵，找到当前的由每一个数值的平方和倒是不难，但是没有想清楚怎么处理无限循环的情况，所以看了下题解，就是说如果当前的sum曾经出现过的话，就会导致无限循环，这就好办了

```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> res = new HashSet<>();
        int ans = getDigitSum(n);
        while (ans != 1) {
            if (res.contains(ans)) {
                return false;
            }
            res.add(ans);
            ans = getDigitSum(ans);
        }
        return true;
    }
    
    public int getDigitSum(int n) {
        int sum = 0;
        while (n != 0) {
            int digit = n % 10;
            sum += digit * digit;
            n = n / 10;
        }
        return sum;
    }
}
```



```python
class Solution:
    def isHappy(self, n: int) -> bool:
        dict = {}
        while n != 1:
            if n in dict:
                return False
            dict[n] = 1
            n = self.sumOfDigit(n)
        return True
    
    def sumOfDigit(self, n: int) -> int:
        currSum = 0
        while n != 0:
            currSum += (n % 10) ** 2
            n = n // 10
        return currSum
```

