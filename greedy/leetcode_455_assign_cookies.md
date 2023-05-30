### Question 455 Assign Cookies

![image-20230519223027958](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230519223027958.png)

这道题目的话是贪心算法的入门题目，整理思路挺简单的，我一开始写了这样的代码，对于每一个小孩而言，找到他应该吃的最小的饼干，简单来说就是对于每一个孩子而言，给它喂所能满足他的最小的饼干

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        List<Integer> cookies = Arrays.stream(s).boxed().collect(Collectors.toList());
        Arrays.sort(s);
        Collections.sort(cookies);
        int count = 0;
        for(int i = 0; i < g.length; i++) {
            if (findCookie(g[i], cookies)) {
                count++;
            } else {
                break;
            }
        }
        return count;
    }

    public boolean findCookie(int greedFactor, List<Integer> cookies) {
        for(int i = 0; i < cookies.size(); i++) {
            if (cookies.get(i) >= greedFactor) {
                cookies.remove(i);
                return true;
            }
        }
        return false;
    }
}
```



后来感觉这么做有点冗余，代码应该是可以进一步优化的，看了看卡哥的代码，也就是卡哥说的第二种遍历方式

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int childIndex = 0;
        int count = 0;
      // 注意： 这里遍历的是饼干，因为两个数组都已经排好序了，
        for(int i = 0; i < s.length; i++) {
            if (childIndex < g.length && s[i] >= g[childIndex]) {
                count++;
                childIndex++;
            }
        }
        return count;
    }
}
```

