```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 || j == 0) {
                    dp[i][j] = 1;
                } else {
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }

        return dp[m - 1][n - 1];
    }
}
```
**RETURN TOTAL NO.OF UNIQUE PATHS FROM (0,0) TO (N,M) IF U ARE ONLY ALLOWED TO MOVE EITHER RIGHT OR DOWN.**

FOR EVERY CELL THE TOTAL NO.OF UNIQUE PATHS IS THE SUM OF UNIQUE PATHS OF TOP CELL AND LEFT CELL. IF THE CELL IS A BORDER CELL IT CAN HAVE ONLY 1 PATH.

## SPACE OPTIMIZED
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        Arrays.fill(dp, 1);

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] = dp[j] + dp[j - 1];
            }
        }

        return dp[n - 1];
    }
}
```
TO SOLVE THIS PROBLEM U DONT NEED AN ENTIRE 2D ARRAY, U JUST NEED THE TOP CELL AND LEFT CELL. SO HAVE A COPY OF THE TOP ROW AND CHANGE THE VALUE OF CURRENT CELL MY ADDING THE VALUE IN THE TOP ROW AT THAT INDEX(TOP CELL) AND PREVIOUS INDEX OF THE CURRENT ROW(LEFT CELL).

```java
dp[j]+=dp[j-1];
```