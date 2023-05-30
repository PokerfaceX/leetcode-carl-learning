### Question 51 N-Queens

<img src="/Users/jasonjin/Library/Application Support/typora-user-images/image-20221129220651436.png" alt="image-20221129220651436" style="zoom:50%;" />

这道题目算得上是经典中的经典，只有用回溯算法才能解决。

![image-20221129220750713](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221129220750713.png)

还是如此，这个图的搜索过程可以被抽象为一棵树。直接上代码来解释

~~~java
class Solution {
    char[][] array;
    List<List<String>> ans = new ArrayList<>();

    public List<List<String>> solveNQueens(int n) {
        this.array = new char[n][n];
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                array[i][j] = '.'; 
            }
        }
        traversal(array, 0, n);
        return this.ans;
    }

    public void traversal(char[][] array, int startRow, int n) {
      // 如果遍历到了一个空节点，也就是当当前行数大于等于n的时候就说明找到了一个合法的二位数组棋盘
        if (startRow >=n) {
            this.ans.add(collectAnswer(array));
            return;
        }
        for(int column = 0; column < n; column++) {
          // 不管怎样，先放一个queen
            array[startRow][column] = 'Q';
            if (checkValidChessBoard(array, startRow,column)) {
                traversal(array, startRow + 1, n);
            } 
          // 不管上面的checkValid返回了什么，都要进行回溯，dfs一次，回溯一次，要不然一行会有俩queen
            array[startRow][column] = '.';
            
        }
    }

    public boolean checkValidChessBoard(char[][] array, int row, int column) {
        // vertically
      // 看看竖着的一列有没有其他queen
        for(int i = 0; i < array.length; i++) {
            if(i != row && array[i][column] == 'Q') {
                return false;
            }
        }
        // horizontally
      // 看看横着的一列有没有queen
        for(int j = 0; j < array.length; j++) {
            if (j != column && array[row][j] == 'Q') {
                return false;
            }
        }
        // left diagonol
      // 假设我们的回溯算法写的完美，那么在当前皇后的下面，不可能有其他皇后，所以只需要检查左上斜线
        for(int i = row - 1, j = column - 1; i >= 0 && j >= 0; i--, j--) {
            if (array[i][j] == 'Q') {
                return false;
            }
        }
        // right diagonol
      // 同理，只检查右上斜线
        for(int i = row - 1, j = column + 1; i >= 0 && j <= array.length - 1; i--, j++) {
            if (array[i][j] == 'Q') {
                return false;
            }
        }
        return true;

    }
	// 当我们获得了一个2维数组的时候，把它转换成一个list，用来加入到答案
    public List<String> collectAnswer(char[][] array) {
        List<String> puzzle = new ArrayList<>();
        for(int i = 0; i < array.length; i++) {
            puzzle.add(String.valueOf(array[i]));
        }
        return puzzle;
    }
}
~~~



