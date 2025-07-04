public class SudokuSolver {

    public static boolean solveSudoku(char[][] board) {
        for (int row = 0; row < board.length; row++) {
            for (int col = 0; col < board[0].length; col++) {
                if (board[row][col] == '.') { // Find an empty cell
                    for (char num = '1'; num <= '9'; num++) { // Try numbers from '1' to '9'
                        if (isValid(board, row, col, num)) { 
                            board[row][col] = num; // Place number
                            if (solveSudoku(board)) return true; // Recur
                            board[row][col] = '.'; // Backtrack
                        }
                    }
                    return false; // No valid number found
                }
            }
        }
        
        return true; // Solved successfully
    }

    private static boolean isValid(char[][] board, int row, int col, char num) {
        for (int i = 0; i < 9; i++) { 
            if (board[row][i] == num || board[i][col] == num || 
                board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == num)
                return false;
        }
        
        return true;
    }

   public static void main(String[] args) { 
       char[][] board = { 
           {'5', '3', '.', '.', '7', '.', '.', '.', '.'}, 
           {'6', '.', '.', '1', '9', '5', '.', '.', '.'}, 
           {'.', '9', '8', '.', '.', '.', '.', '6', '.'}, 
           {'8', '.', '.', '.', '6', '.', '.', '.', '3'}, 
           {'4', '.', '9', '8', '.', '3', '.', '.', '1'}, 
           {'7', '.', '.', '2', '4', '.', '.', '9', '.'}, 
           {'.', '6', '.', '.', '.', '.', '2', '8', '.'}, 
           {'.', '.', '2', '7', '5', '6', '9', '.', '.'}, 
           {'.', '8', '.', '.', '2', '.', '.', '4', '.'} 
       };

       if(solveSudoku(board)) { 
          System.out.println("Sudoku solved successfully!"); 
       } else { 
          System.out.println("No solution exists."); 
       } 

       for(char[] row : board){ 
          System.out.println(row); 
       } 
   } 
}
 
