
# EX 3C Tug of War problem - Backtracking.

## AIM:
To write a Java program to for given constraints.
Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.
Example 1:
Input: Enter the number of elements: 4
Enter the elements of the array:
1 5 11 5
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].

Constraints:

1 <= nums.length <= 200
1 <= nums[i] <= 100

## Algorithm
1. Read the number of elements and the array values from the user.

2. Calculate the total sum of all elements:
   - If the total sum is odd, return false (cannot be divided into two equal subsets).

3. Set target sum as totalSum / 2 and initialize a boolean DP array of size (target + 1):
   - Set dp[0] = true (base case).

4. For each element in the array:
   - Traverse the DP array backwards from target to current element.
   - Update dp[j] = dp[j] OR dp[j - current element].

5. If dp[target] is true, partition is possible; otherwise, it is not possible.  

## Program:
```java

import java.util.Scanner;
public class Solution {
    public boolean canPartition(int[] nums) {
        if (nums.length == 0)
            return false;
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }
        if (totalSum % 2 != 0)
            return false;
        int subSetSum = totalSum / 2;
        boolean[] dp = new boolean[subSetSum + 1];
        dp[0] = true;
        for (int curr : nums) {
            for (int j = subSetSum; j >= curr; j--) {
                dp[j] |= dp[j - curr];
            }
        }
        return dp[subSetSum];
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution sol = new Solution();
        int n = scanner.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }
        boolean canBePartitioned = sol.canPartition(nums);
        System.out.println(canBePartitioned);
    }
}
```

## Output:
<img width="594" height="1001" alt="image" src="https://github.com/user-attachments/assets/f7ae5dbd-e70d-419d-92f1-8c8d799d7148" />

## Result:
The program successfully implemented and the expected output is verified.

