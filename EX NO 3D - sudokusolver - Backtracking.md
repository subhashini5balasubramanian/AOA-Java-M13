
# EX 3D Sudoku solver - Backtracking.

## AIM:
To write a Java program to solve a Sudoku puzzle by filling the empty cells.

For example:
<img width="357" height="322" alt="image" src="https://github.com/user-attachments/assets/334b8c39-d547-4743-aca0-de92e38bdd1c" />



## Algorithm
1. Read the 9×9 Sudoku board from the user, where empty cells are represented by 0.

2. Start from the first cell (row = 0, col = 0) and move through each cell:
   - If the cell is already filled, move to the next column.

3. For an empty cell, try placing numbers from 1 to 9:
   - Check if placing a number is safe (not present in the same row, column, and 3×3 subgrid).

4. If a number is safe:
   - Place the number and recursively attempt to solve the next cell.
   - If it leads to failure, backtrack by resetting the cell to 0.

5. If all cells are filled successfully, print the solved board; otherwise, report that no solution exists.

## Program:
```java
import java.util.Scanner;

public class SudokuSolver {

    static boolean isSafe(int[][] board, int row, int col, int num) {
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == num || board[i][col] == num)
                return false;
        }

        int startRow = row - row % 3;
        int startCol = col - col % 3;

        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (board[startRow + i][startCol + j] == num)
                    return false;

        return true;
    }
    static boolean solveSudoku(int[][] board, int row, int col) {
        if (row == 8 && col == 9)
            return true;

        if (col == 9) {
            row++;
            col = 0;
        }

        if (board[row][col] != 0)
            return solveSudoku(board, row, col + 1);

        for (int num = 1; num <= 9; num++) {
            if (isSafe(board, row, col, num)) {
                board[row][col] = num;
                if (solveSudoku(board, row, col + 1))
                    return true;
                board[row][col] = 0;
            }
        }

        return false;
    }
    static void printBoard(int[][] board) {
        for (int[] row : board) {
            for (int val : row)
                System.out.print(val + " ");
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[][] board = new int[9][9];
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                board[i][j] = sc.nextInt();
            }
        }
        if (solveSudoku(board, 0, 0)) {
            System.out.println("Solved Sudoku:");
            printBoard(board);
        } else {
            System.out.println("No solution exists.");
        }

        sc.close();
    }
}
```

## Output:
<img width="555" height="570" alt="image" src="https://github.com/user-attachments/assets/6cfa66d5-7a13-4d49-9aee-bdffeee272f0" />

## Result:
The program successfully implemented and the expected output is verified.
