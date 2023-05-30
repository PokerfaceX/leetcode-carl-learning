### Question 37 Sudoku Solver

![image-20230518233427096](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230518233427096.png)

应该是整个回溯算法章节最难的一道题目了，这道题目难就难在二维的递归上面，我们从第一行第一个空格子开始fill in，如果是valid，就往第一行第二个格子里面去fill，如果不是valid

```java
class Solution {
    public void solveSudoku(char[][] board) {
        backtracking(board);
    }

    public boolean backtracking(char[][] board) {
      // 每一个都是从头开始看，直到第一个空格才开始做判断  
      for(int i = 0; i < 9; i++) {
            for(int j = 0; j < 9; j++) {
                if (board[i][j] != '.') {
                    continue;
                }
              // 这里1-9都得试一次
                for(char num = '1'; num <= '9'; num++) {
                  // 先放置在说  
                  board[i][j] = num;
                    if (validBoard(board, i, j)) {
                      // 如果合适的数值的话，在看下个空格
                        if (backtracking(board)) {
                          // 最后返回true了就说明，所有空格都已经填满了，所以一层层往上return
                            return true;
                        }
                    } 
                  // 当前数值不合法，直接回溯
                    board[i][j] = '.'; 
                }
              // 9个数字都尝试了，都不合法，所以返回false
                return false;
            }
        }
      // 棋盘都遍历完了，到最后了，就说明都被符合条件的填写好了，直接返回true就好了
      // 一直向下递归，不断的选数，成功找到了一次所有填写的数值都符合条件的情况，就应该直接返回true
        return true;
    }

    public boolean validBoard(char[][] board, int row, int col) {
        Set<Character> set = new HashSet<>();
        for(int j = 0; j < 9; j++) {
            if (board[row][j] != '.' && set.contains(board[row][j])) {
                return false;
            }
            set.add(board[row][j]);
        }
        set.clear();
        for(int i = 0; i < 9; i++) {
            if (board[i][col] != '.' && set.contains(board[i][col])) {
                return false;
            }
            set.add(board[i][col]); 
        }
        set.clear();
        int startRow = row / 3 * 3;
        int startCol = col / 3 * 3;
        for(int i = startRow; i < startRow + 3; i++) {
            for(int j = startCol; j < startCol + 3; j++) {
                if (board[i][j] != '.' && set.contains(board[i][j])) {
                    return false;
                } 
                set.add(board[i][j]);
            }
        }
        return true;
    }
}
```

