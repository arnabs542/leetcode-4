### Question {#question}

[https://leetcode.com/problems/unique-paths/description/](https://leetcode.com/problems/unique-paths/description/)

A robot is located at the top-left corner of a m x n grid \(marked 'Start' in the diagram below\).





**Example:**

```

```

### Thought Process {#thought-process}

1. DP
   1. For an one dimensional array, there is only one way to reach there, straight right or straight down
   2. Now for two dimensional array, the ways to get there will be way\[left\] and way\[top\]
   3. Time complexity O\(mn\)
   4. Space complexity O\(mn\)
2. DP - Optimized Space
   1. W
   2. We can choose the smaller one to save the space, for now we just stick with columns n
   3. Time complexity O\(mn\)
   4. Space complexity O\(n\)
3. Math formula
   1. There are total of m + n - 2 steps, m -1 down and n - 1 right
   2. This question is essentially asking how many ways we can get by performing m - 1 down steps out of total m + n - 2 moves
   3. The answer is simply Combination\(n, k\) =  n! / \(n - k\)! k!
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for (int c = 0; c < n; c++) dp[0][c] = 1;
        for (int r = 0; r < m; r++) dp[r][0] = 1;
        for (int r = 1; r < m; r++) {
            for (int c = 1; c < n; c++) {
                dp[r][c] = dp[r - 1][c] + dp[r][c - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}
```

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        dp[0] = 1;
        for (int r = 0; r < m; r++) {
            for (int c = 1; c < n; c++) {
                dp[c] += dp[c- 1];
            }
        }
        return dp[n - 1];
    }
}
```

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int num = m + n - 2, den = Math.min(m, n) - 1;
        long res = 1;
        for (int i = 0; i < den; i++) {
            res = res * (num - i) / (i + 1);
        }
        return (int) res;
    }
}
```

### Additional {#additional}


