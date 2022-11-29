### Question 51 N-Queens

<img src="/Users/jasonjin/Library/Application Support/typora-user-images/image-20221129220651436.png" alt="image-20221129220651436" style="zoom:50%;" />

这道题目算得上是经典中的经典，只有用回溯算法才能解决。

![image-20221129220750713](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221129220750713.png)

还是如此，这个图的搜索过程可以被抽象为一棵树。直接上代码来解释

~~~java
class Solution {
    
    List<List<String>> ans = new ArrayList<>();
    char[][] chessBoard;
    
    public List<List<String>> solveNQueens(int n) {
        chessBoard = new char[n][n];
        // 棋盘的初始化
        for(int i = 0; i < n; i++) {
            Arrays.fill(chessBoard[i], '.');
        }
        traversal(chessBoard, 0, n); // 我们需要一个currRow变量来看当前遍历到第几层了，for循环是看遍历到第几列了
        return ans;
    }

    public void traversal(char[][] chessBoard, int currRow, int n) {
      // 当目前行数等于n的时候说明到了叶子结点，返回就行，在这里我们可以放心的认为叶子结点都是符合规定的棋盘因为不符合规定的情况在循环中就被跳过了
      if (currRow >= n) {
            ans.add(convert2DArrayToList(chessBoard));
            return;
        }
        for(int col = 0; col < n; col++) {
            // 不管三七二十一，直接先放一个皇后棋子
            chessBoard[currRow][col] = 'Q';
            // 看看当前的棋盘是不是符合规定的
            if (validChessBoard(chessBoard, col, currRow)) {
                traversal(chessBoard, currRow + 1, n);
            }
            chessBoard[currRow][col] = '.'; // 常规的回溯操作

        }
    }
    
    // valid棋盘只需要看横着，竖着，斜着，在这三条线上有没有棋子
    public boolean validChessBoard(char[][] chessBoard, int currCol, int currRow) {
      // 画图才能解释清楚，简单来说我们没必要遍历所有的row，因为假设row目前为3，那么row等于4或者5的时候，那里是不可能有棋子的  
      
      // 按照row来排查，看看有没有女王
      for(int i = 0; i < currRow; i++) {
            if (chessBoard[i][currCol] == 'Q') {
                return false;
            }
        }
      // 从最新的queen的位置的左上角到棋盘的左上角有没有棋子
        for(int i = currRow - 1, j = currCol - 1; i >= 0 && j >= 0; i--, j--) {
            if (chessBoard[i][j] == 'Q') {
                return false;
            }
        }
      // 从最新的queen的位置的右上角到棋盘的右上角有没有棋子
        for(int i = currRow - 1, j = currCol + 1; i >= 0 && j <= chessBoard.length - 1; i--, j++) {
            if (chessBoard[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }
		
  // 这个函数没什么特别的，就是把一个2d数组转换成一个list of string
    public List<String> convert2DArrayToList(char[][] chessBoard) {
        List<String> tmp = new ArrayList<>();
        for(int i = 0; i < chessBoard.length; i++) {
            String rowString = String.valueOf(chessBoard[i]); // 可以直接吧char数组转换成list
            tmp.add(rowString);
        }
        return tmp;
    }
}
~~~



