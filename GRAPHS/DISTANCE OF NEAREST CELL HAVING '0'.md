```java
class Data {
    int row;
    int col;
    int dis;
    public Data(int row,int col,int dis) {
        this.row=row;
        this.col=col;
        this.dis=dis;
    }
}
class Solution {
    int dr[] = {-1,1,0,0};
    int dc[] = {0,0,-1,1};
    public int[][] updateMatrix(int[][] mat) {
        Queue<Data> queue = new ArrayDeque<>();
        boolean vis[][] = new boolean[mat.length][mat[0].length];
        int disMat[][] = new int[mat.length][mat[0].length];
        for(int i=0;i<mat.length;i++) {
            for(int j=0;j<mat[0].length;j++) {
                if(mat[i][j]==0) {
                     queue.add(new Data(i,j,1));
                     vis[i][j]=true;
                }
            }
        } 
        while(!queue.isEmpty()) {
            for(int i=0;i<queue.size();i++) {
                Data data = queue.poll();
                for(int k=0;k<4;k++) {
                    int nr = data.row+dr[k];
                    int nc = data.col+dc[k];
                    if(nr>=0&&nr<mat.length&&nc>=0&&nc<mat[0].length&&!vis[nr][nc]) {
                        disMat[nr][nc]=data.dis;
                        queue.add(new Data(nr,nc,data.dis+1));
                        vis[nr][nc]=true;
                    }
                }
            } 
        } return disMat;
    } 
}
```
SIMILAR TO ROTTEN ORANGES. STORES DISTANCE IN THE QUEUE AND INCREMENTS EVERY PASS.