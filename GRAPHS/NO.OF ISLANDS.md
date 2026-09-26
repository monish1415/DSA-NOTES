```java
class Solution {
    int dr[] = {-1,1,0,0};
    int dc[] = {0,0,-1,1};
    public int numIslands(char[][] grid) {
        int islands=0;
        boolean vis[][] = new boolean[grid.length][grid[0].length];
        for(int i=0;i<grid.length;i++) {
            for(int j=0;j<grid[0].length;j++) {
                if(!vis[i][j]&&grid[i][j]=='1') {
                    dfs(grid,vis,i,j);
                    islands++;
                }
            }
        } return islands;
    } 
    private void dfs(char[][] grid,boolean vis[][],int i,int j) {
        vis[i][j]= true;
        for(int k=0;k<4;k++) {
            int nr = i+dr[k];
            int nc = j+dc[k];
            if(nr>=0&&nr<grid.length&&nc>=0&&nc<grid[0].length&&grid[nr][nc]=='1'&&!vis[nr][nc]) dfs(grid,vis,nr,nc);
        }
    }
}
```

MAKE A 2D VISITED ARRAY TO STORE THE VISTED LOCATIONS WHICH ARE '1'. IN DFS FUNCTION, THE LOOP RUNS 4 TIMES. UP,DOWN,LEFT,RIGHT. NOW CHECK IF THE NEXT LOCATION TO BE VISITED IS VALID OR NOT AND IS '1'.