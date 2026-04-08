
# EX 3E Generate Permutations using Backtracking  Approach.

## AIM:
To write a Java program to for given constraints.
Given an array nums of distinct integers, return all the possible Permutation. You can return the answer in any order.
Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

## Algorithm
1. Read the input array from the user.

2. Initialize an empty list to store all permutations and start backtracking with an empty current list.

3. At each step, check if the current list size equals the array length:
   - If yes, add a copy of the current list to the result.

4. Iterate through each element in the array:
   - If the element is not already in the current list, add it.
   - Recursively call the function to build the next position.
   - After recursion, remove the last element (backtrack).

5. Continue until all permutations are generated, then print the result list. 

## Program:
```java
import java.util.*;
public class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(new ArrayList<>(), ans, nums);
        return ans;
    }
    public void backtrack(List<Integer> curr, List<List<Integer>> ans, int[] nums) {
        if (curr.size() == nums.length) {
            ans.add(new ArrayList<>(curr));
            return;
        }
        for (int num : nums) {
            if (!curr.contains(num)) {
                curr.add(num);
                backtrack(curr, ans, nums);
                curr.remove(curr.size() - 1);
            }
        }
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String inputLine = scanner.nextLine().trim();
        inputLine = inputLine.replaceAll(".*\\[|\\].*", "");
        String[] parts = inputLine.split(",");

        int[] nums = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }
        Solution solution = new Solution();
        List<List<Integer>> permutations = solution.permute(nums);
        System.out.println(permutations);
        scanner.close();
    }
}
```

## Output:
<img width="1090" height="259" alt="image" src="https://github.com/user-attachments/assets/af13081d-732b-4cbc-9fa5-303fecc5a37c" />

## Result:
The program successfully implemented and the expected output is verified.`

