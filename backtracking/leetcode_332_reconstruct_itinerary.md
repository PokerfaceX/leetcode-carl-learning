### Question 332 Reconstruct Itinerary

![image-20230516205046096](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230516205046096.png)

这道题目是一道难题，是吧图论里的dfs和回溯算法结合到了一起，核心思想就是先记录下所有的路径，类似于adjacency list，然后因为这道题目要找smallest lexical order，我们就要把每一个adjacency list给sort了再进行dfs



```java
class Solution {

    List<String> path = new ArrayList<>();
    Map<String, List<String>> map = new HashMap<>();
    
    public List<String> findItinerary(List<List<String>> tickets) {
        for(List<String> list: tickets) {
            if (!map.containsKey(list.get(0))) {
                map.put(list.get(0), new ArrayList<>());
            }
            map.get(list.get(0)).add(list.get(1));
        }
        for(String key: map.keySet()) {
            Collections.sort(map.get(key));
        }
        path.add("JFK");
        traversal("JFK", tickets.size() + 1);
        return this.path;
    }

    public boolean traversal(String source, int targetNum) {
      // 合法性判断，如果路径里面的数量等于target，就说明是合法路径  
      if (path.size() == targetNum) {
            return true;
        }
      // 如果一个节点没有任何去别的地方的路径，那就是null，比如有些节点一开始就从来没加入过map中，因为这个节点可能孤悬在图外面，没链接任何路径，在这种情况下需要返回false
      // 如果一个节点在回溯的过程中，他到周围的链接的路径都被使用过了，就会是empty，那此事就被困住了，所以也要return null
        if (map.get(source) == null || map.get(source).isEmpty()) {
            return false;
        }
        // System.out.println("path is ->" + path);
        // System.out.println("map is ->" + map);
        // System.out.println("source is ->" + source);
        List<String> destinations = map.get(source);
        for(int i = 0; i < destinations.size(); i++) {
            String dest = destinations.get(i);
          // 删除这个路径
            destinations.remove(i);
          // 删除这个节点
            path.add(dest);
            if (traversal(dest, targetNum)) {
              // 当找到到了一个合法路径的时候，不用再往后看，直接return true
                return true;
            }
          // 因为没找到合法路径，所以进行回溯操作
            path.remove(path.size() - 1);
            destinations.add(i, dest);
        }
      // for循环里面没有找到合法路径，没有被return true，所以到最后返回false
        return false;
    }
}
```

