TABULATION METHOD
```java
class Solution {
    public int cherryPickup(int[][] grid) {
        int n = grid.length;
        int m = grid[0].length;

        int[][][] dp = new int[n][m][m];

        // Base case: last row
        for (int j1 = 0; j1 < m; j1++) {
            for (int j2 = 0; j2 < m; j2++) {
                if (j1 == j2) {
                    dp[n - 1][j1][j2] = grid[n - 1][j1];
                } else {
                    dp[n - 1][j1][j2] =
                            grid[n - 1][j1] + grid[n - 1][j2];
                }
            }
        }

        // Build DP from bottom to top
        for (int i = n - 2; i >= 0; i--) {
            for (int j1 = 0; j1 < m; j1++) {
                for (int j2 = 0; j2 < m; j2++) {

                    int cherries = (j1 == j2)
                            ? grid[i][j1]
                            : grid[i][j1] + grid[i][j2];

                    int max = Integer.MIN_VALUE;

                    for (int d1 = -1; d1 <= 1; d1++) {
                        for (int d2 = -1; d2 <= 1; d2++) {
                            int nc1 = j1 + d1;
                            int nc2 = j2 + d2;

                            if (nc1 < 0 || nc1 >= m ||
                                nc2 < 0 || nc2 >= m) {
                                continue;
                            }

                            max = Math.max(max, dp[i + 1][nc1][nc2]);
                        }
                    }

                    dp[i][j1][j2] = cherries + max;
                }
            }
        }

        return dp[0][0][m - 1];
    }
}
```
USE A 3D ARRAY TO STORE THE TOTAL CHERRIES PICKED UP BY ROBOTS AT TWO POSITIONS AT ONE LEVEL, A TOTAL OF MxM COMBINATIONS AT DIFFERENT LEVELS, WHICH LEADS TO 2D ARRAY FOR POSITION COMBINATIONS AND A 1D ARRAY FOR EACH ROW. THEREFORE THIS USES A 3D ARRAY.

### SPACE OPTIMIZATION
```java
class Solution {
    public int cherryPickup(int[][] grid) {
        int n=grid.length;
        int m=grid[0].length;
        int original[][]=new int[m][m];
        int temp[][]=new int[m][m];
        for(int i=0;i<m;i++) {
            for(int j=0;j<m;j++) {
                if(i==j) {
                    original[i][j]=grid[n-1][i];
                    temp[i][j]=original[i][j];
                }
                else {
                    original[i][j]=grid[n-1][i]+grid[n-1][j];
                    temp[i][j]=original[i][j];
                }
            }
        }
        for(int i=n-2;i>=0;i--) {
            for(int j1=0;j1<m;j1++) {
                for(int j2=0;j2<m;j2++) {
                    int value=0;
                    if(j1==j2) value=grid[i][j1];
                    else value=grid[i][j1]+grid[i][j2];
                    int max=Integer.MIN_VALUE;
                    for(int k1=-1;k1<=1;k1++) {
                        int nc1=j1+k1;
                        if(nc1<0||nc1>m-1) continue;
                        for(int k2=-1;k2<=1;k2++) {
                            int nc2=j2+k2;
                            if(nc2<0||nc2>m-1) continue;
                            max=Math.max(max,original[nc1][nc2]);
                        }
                    } temp[j1][j2]=value+max;
                }
            } 
            int swap[][]=original;
            original=temp;
            temp=swap;
        }
        return original[0][m-1];
    }
}
```
* USE 2 2D ARRAYS AND CHANGE ITS VALUES FOR EVERY LEVEL TILL WE REACH THE TOPMOST LEVEL INSTEAD OF STORING ALL THE VALUES OF EVERY LEVEL IN A 3D ARRAY.
* FILL UP THE ORIGINAL AND TEMP ARRAY WITH MAX CHERRIES PICKED-UP AT EVERY DIFFERENT POSITION OF THE LAST ROW. 
* MAKE CHANGES IN THE TEMP ARRAY WHILE USING THE ORIGINAL ARRAY FOR COMPARISION. COPY THE CONTENTS OF TEMP ARRAY TO ORIGINAL ARRAY AFTER A LEVEL IS PROCESSED.
* RETURN ORIGINAL(0,M-1) (OR) ORIGINAL(M-1,0) SINCE ORIGINAL SAYS ABOUT THE SUM OF CHERRIES PICKED UP WHEN ROBOTS ARE AT POSITION J1,J2.