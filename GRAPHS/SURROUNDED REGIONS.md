```java
class Solution {
    int dr[] = {-1,1,0,0};
    int dc[] = {0,0,-1,1};
    public void solve(char[][] board) {
        boolean vis[][] = new boolean[board.length][board[0].length];
       for(int i=0;i<board.length;i++) {
        for(int j=0;j<board[0].length;j++) {
            if(!vis[i][j]&&board[i][j]=='O'&&(i==0||i==board.length-1||j==0||j==board[0].length-1)) {
                dfs(board,vis,i,j);
            }
        }
       } 
       for(int i=0;i<board.length;i++) {
        for(int j=0;j<board[0].length;j++) {
            if(!vis[i][j]&&board[i][j]=='O') board[i][j]='X';
        }
       }
    } 
    private void dfs(char[][] board,boolean[][] vis,int i,int j) {
        vis[i][j]=true;
        for(int k=0;k<4;k++) {
            int nr = i + dr[k];
            int nc = j +dc[k];
            if(nr>=0&&nr<board.length&&nc>=0&&nc<board[0].length&&!vis[nr][nc]&&board[nr][nc]=='O') dfs(board,vis,nr,nc);
        }
    }
}
```
GO TO THE 'O' WHICH IS AT THE BORDER. APPLY DFS TO IT AND MAKE EVERY 'O' CONNECTED TO THE BORDER 'O' INVALID. DO THIS FOR ALL BORDER 'O's. ITERATE THROUGH THE MATRIX AND REPLACE THE UNVISITED 'O's WITH 'X'.