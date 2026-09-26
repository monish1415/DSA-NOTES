```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        boolean vis[] = new boolean[isConnected.length];
        int provinces=0;
        for(int i=0;i<isConnected.length;i++) {
            if(!vis[i]) {
                dfs(isConnected,vis,i);
                provinces++;
            } 
        } return provinces;
    }
    private void dfs(int[][] matrix,boolean[] vis,int i){
        vis[i]=true;
        for(int j=0;j<matrix.length;j++) {
            if(!vis[j]&&matrix[i][j]==1) {
            
            dfs(matrix,vis,j);
            }
        }
    }
}
```
BASIC DFS SOLUTION. NO.OF PROVINCES = NO.OF CONNECTED COMPONENTS IN THE GIVEN GRAPH. A NEW NODE WHICH IS NOT CONNECTED TO ANY GRAPH GIVES US A PROVINCE.