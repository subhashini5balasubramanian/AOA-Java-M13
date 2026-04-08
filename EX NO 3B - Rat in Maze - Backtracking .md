
# EX 3B Rat in Maze- Backtracking 

## AIM:
To write a Java program to for given constraints.
here is a ball in a maze with empty spaces (represented as 0) and walls (represented as 1). The ball can go through the empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the m x n maze, the ball's start position and the destination, where start = [startrow, startcol] and destination = [destinationrow, destinationcol], return true if the ball can stop at the destination, otherwise return false.

You may assume that the borders of the maze are all walls (see examples).
<img width="573" height="573" alt="image" src="https://github.com/user-attachments/assets/d6f1c054-cdc2-4bb3-9c55-512fb2cf0fb7" />
Input: maze = [[0,0,1,0,0],[0,0,0,0,0],[0,0,0,1,0],[1,1,0,1,1],[0,0,0,0,0]], start = [0,4], destination = [4,4]
Output: true
Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.


## Algorithm
1. Read the maze dimensions (m, n), the maze matrix, starting position, and destination position.

2. Initialize a visited array to keep track of visited cells to avoid revisiting the same position.

3. Start DFS from the starting cell:
   - If the current cell is already visited, return false.
   - If the current cell is the destination, return true.

4. From the current cell, move in all four directions (up, down, left, right):
   - Continue moving in a direction until hitting a wall or boundary.
   - Recursively call DFS from the stopping position.

5. If any recursive call reaches the destination, return true; otherwise, after exploring all paths, return false.   

## Program:
```java

import java.util.*;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int m = sc.nextInt();
        int n = sc.nextInt();

        int[][] maze = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maze[i][j] = sc.nextInt();
            }
        }

        int[] start = new int[]{sc.nextInt(), sc.nextInt()};
        int[] destination = new int[]{sc.nextInt(), sc.nextInt()};

        Solution sol = new Solution();
        boolean result = sol.hasPath(maze, start, destination);

        System.out.println(result);
    }
}

class Solution {

    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        int m = maze.length;
        int n = maze[0].length;
        boolean[][] visit = new boolean[m][n];

        return dfs(m, n, maze, start, destination, visit);
    }

    public boolean dfs(int m, int n, int[][] maze, int[] curr, int[] destination, boolean[][] visit) {

        int x = curr[0];
        int y = curr[1];

        if (visit[x][y]) return false;
        if (x == destination[0] && y == destination[1]) return true;

        visit[x][y] = true;

        int[][] dir = {{1,0},{-1,0},{0,1},{0,-1}};

        for(int[] d : dir){

            int nx = x;
            int ny = y;

            while(nx + d[0] >= 0 && nx + d[0] < m &&
                  ny + d[1] >= 0 && ny + d[1] < n &&
                  maze[nx + d[0]][ny + d[1]] == 0){

                nx += d[0];
                ny += d[1];
            }

            if(dfs(m, n, maze, new int[]{nx, ny}, destination, visit)){
                return true;
            }
        }

        return false;
    }
}
```

## Output:
<img width="370" height="513" alt="image" src="https://github.com/user-attachments/assets/206e1a04-32d1-472a-8819-f7afc959bb36" />

## Result:
The program successfully implemented and the expected output is verified.

