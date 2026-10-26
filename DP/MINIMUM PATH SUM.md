```java
class Solution {
    public int minPathSum(int[][] grid) {
        int n=grid.length;
        int m=grid[0].length;
        int dp[]=new int[m];
        dp[0]=grid[0][0];
        for(int i=1;i<m;i++) {
            dp[i]=dp[i-1]+grid[0][i];
        }
        for(int i=1;i<n;i++) {
            for(int j=0;j<m;j++) {
                if(j==0) dp[j]+=grid[i][j];
                else dp[j]=grid[i][j]+Math.min(dp[j-1],dp[j]);
            }
        }
        return dp[m-1];
    }
}
```
SAME AS UNIQUE PATHS IN A GRID.
A CELL CAN BE VISITED IN 2 WAYS, FROM TOP AND FROM LEFT. TAKE THE MIN VALUE OF TOP AND LEFT AND ADD IT TO THE CURRENT CELL VALUE.
THEREFORE WE ONLY NEED THE TOP ROW AND LEFT INDEX,SIMILAR TO UNIQUE PATHS. IF THE INDEX IS '0'->THAT CELL CAN ONLY BE VISITED FROM TOP,IF NOT '0' TAKE MIN OF LEFT AND TOP.