### Question 40 Combination Sum II

![image-20230513180221092](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230513180221092.png)

这道题目的关键在于去重，在最终的答案里，不能出现相同的组合

举个例子[1, 1, 2], target = 3，在这里我们只能返回一个[1, 2]

但是要注意的是，尽管不能有重复的答案，且每一个数字在组合中只能使用一次，但是这每一个数字是针对candidates数组里面的下标而言的。意思就是说同一个index对应的数字只能使用一次，所以第一个1和第二个1实际上指的是不同的数字.

这道题目，卡哥给了两个关键词，树层去重和树枝去重，看图

![image-20230513180240896](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230513180240896.png)



~~~java
class Solution {
    
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    boolean[] used;
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        
        Arrays.sort(candidates);
        this.used = new boolean[candidates.length];
        traversal(candidates, target, 0, 0);
        return ans;
    }

    public void traversal(int[] candidates, int target, int currSum, int startIndex) {
        if (currSum > target) {
            return;
        }
        if (currSum == target) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = startIndex; i < candidates.length; i++) {
            // 这里如果是used[i - 1] == true，那么就会抛弃所有类似于[1, 1]的情况，这不是我们想要的，我们想要删除的只是回溯过程结束之后发现前面有重复的数值才跳过 
            if (i > 0 && used[i - 1] == false && candidates[i] == candidates[i - 1]) {
                continue;
            }
            path.add(candidates[i]);
            used[i] = true;
            traversal(candidates, target, currSum + candidates[i], i + 1);
            path.remove(path.size() - 1);
            used[i] = false;
        }
    }
}
~~~



自己做了做，发现卡哥的代码还是复杂了，

```java
class Solution {

    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    int currSum = 0;

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        // 想要去重，必须要一个sorted array
        Arrays.sort(candidates);
        backtracking(candidates, target, 0);
        return ans;
    }

    public void backtracking(int[] candidates, int target, int startIndex) {
        if (currSum == target) {
            ans.add(new ArrayList<>(path));
            return;
        }
        if (currSum > target) {
            return;
        }
        for(int i = startIndex; i < candidates.length; i++) {‘
           // 去重操作，如果当前的数值不是当前这一层第一个数值且和前一位重复，就说明是应该去重的数值，举个例子[1,2,2,2]，找target == 5， 那么每次递归的时候第一个2都是可以接受的数值，需要跳过的是在当前这一层重复的2，之所以这样是因为我们进行的是回溯搜索，也是暴力搜索，在搜索以当前的层的第一个2为基准，和为5的所有组合的时候，就已经把后面所有的可能性包含了
            if (i > startIndex && candidates[i] == candidates[i - 1]) {
                continue;
            }
            currSum += candidates[i];
            path.add(candidates[i]);
            backtracking(candidates, target, i + 1);
            currSum -= candidates[i];
            path.remove(path.size() - 1);
        }
    }
}
```

