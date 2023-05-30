### Question 860 Lemonade Change

![image-20230525000539645](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230525000539645.png)

这道题目看起来复杂，其实仔细想想，只有三种情况

- 情况1:给了5块的钞票，不用找钱，直接收下
- 情况2:给了10块的纸钞，给5块change
- 情况3:给了20块的纸钞，我们返回给15块，但是我们优先消耗10块的纸钞，因为5块的纸钞更加的万能，能同时处理情况2，3，而10块的面值只能帮助处理情况3，这里就是我们局部最优的地方

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        Map<Integer, Integer> cashNotes = new HashMap<>();
        cashNotes.put(5, 0);
        cashNotes.put(10, 0);
        cashNotes.put(20, 0);
        for(int i = 0; i < bills.length; i++) {
            int cashChange = bills[i] - 5;
            if (cashChange == 0) {
                cashNotes.put(5, cashNotes.get(5) + 1);
            } else if (cashChange == 5) {
                if (cashNotes.get(5) == 0) {
                    return false;
                }
                cashNotes.put(5, cashNotes.get(5) - 1);
                cashNotes.put(10, cashNotes.get(10) + 1);
            } else if(cashChange == 15) {
                cashNotes.put(20, cashNotes.get(20) + 1);
                if (cashNotes.get(10) >= 1 && cashNotes.get(5) >= 1) {
                    cashNotes.put(5, cashNotes.get(5) - 1);
                    cashNotes.put(10, cashNotes.get(10) - 1);
                } else if (cashNotes.get(5) >= 3) {
                    cashNotes.put(5, cashNotes.get(5) - 3);
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}
```

一开始写的，用map来记录目前手上每一种面值的个数，但是上面的代码有点冗余，直接看下面的版本

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0, ten = 0, twenty = 0;
        for(Integer bill: bills) {
            int change = bill - 5;
            // gave $5
            if (change == 0) {
                five++;
            // gave $10
            } else if (change == 5) {
                if (five <= 0) {
                    return false;
                }
                five--;
                ten++;
            // gave $20
            } else if (change == 15) {
                if (ten >= 1 && five >= 1) {
                    ten--;
                    five--;
                } else if (five >= 3) {
                    five -= 3;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}
```

这题就不多解释了，上面的代码一目了然