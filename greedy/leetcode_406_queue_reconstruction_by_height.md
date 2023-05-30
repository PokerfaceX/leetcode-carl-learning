### Question 406 Queue Reconstruction by Height

![image-20230526204926755](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230526204926755.png)

这道题目很有意思，和leetcode_135有点像，需要从两个维度来思考问题，既要身高从高到小，又要满足k的条件，那么这种时候，想一次性sort好是非常困难的，必须要先sort某一个东西，在sort某一个东西

这里的话我们可以先根据每一个人的身高做一个排序，所以让高个子都站在前面，在根据k进行排序，让k小的在前面，k大的在后面，因为k代表着前面比自己大的人数，所以大的k方面合理一些

在排序好了之后，我们在创建一个list，从排序好的数组里面，一个个的根据他们的k插入到list里面，因为我们后面插入的节点不会影响已经插入的节点，原因就是前面已经插入的节点一定比后面插入的要大，所以即便被击倒了后面，也所谓

![image-20230526205534905](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230526205534905.png)



```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
      // rule of thumb: 想从小到的排，就person1 - person2
      // 从大到小排，就person2 - person1
        Arrays.sort(people, (person1, person2) -> {
          // 身高一样的时候让k小的站前面
            if (person1[0] == person2[0]) {
                return person1[1] - person2[1];
            }
          // 根据身高排列
            return person2[0] - person1[0];
        });
        List<int[]> list = new LinkedList<>();
      // 这个insert不看卡哥的视频确实想不出来
        for(int i = 0; i < people.length; i++) {
            list.add(people[i][1], people[i]);
        }
        int[][] ans = new int[people.length][];
        for(int i = 0; i < list.size(); i++) {
            ans[i] = list.get(i);
        }
        return ans;
    }
}
```

用了更优雅的写法

```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (person1, person2) -> {
            if (person1[0] == person2[0]) {
                return person1[1] - person2[1];
            }
            return person2[0] - person1[0];
        });
        List<int[]> list = new LinkedList<>();
        for(int[] person: people) {
            list.add(person[1], person);
        }
      // 这里面的参数就是要返回的数组类型
        return list.toArray(new int[people.length][]);
    }
}
```

