```java
class Pair {
    int row;
    int col;
    public Pair(int row,int col) {
        this.row=row;
        this.col=col;
    }
}
class Solution {
    int dr[] = {-1,1,0,0};
    int dc[] = {0,0,-1,1};
    int time = 0;
      Queue<Pair> queue = new ArrayDeque<>();
    public int orangesRotting(int[][] grid) {
     boolean vis[][] = new boolean[grid.length][grid[0].length];
     for(int i=0;i<grid.length;i++) {
        for(int j=0;j<grid[0].length;j++) {
            if(grid[i][j]==2) {
                queue.add(new Pair(i,j));  //adding all the rotte elements to queue
            } 
        }
     }
      while(!queue.isEmpty()) {
        boolean rotted =false;
            int size = queue.size();
            for(int k=0;k<size;k++) {
                Pair pair = queue.poll();   
                for(int d=0;d<4;d++) {
                    int nr = pair.row +dr[d]; //basic bfs
                    int nc = pair.col +dc[d];
                    if(nr>=0&&nr<grid.length&&nc>=0&&nc<grid[0].length&&grid[nr][nc]==1) {
                        grid[nr][nc]=2;
                        queue.add(new Pair(nr,nc));
                        rotted=true;
                    }
                }
            } if(rotted) time++;
        }   
     for(int i=0;i<grid.length;i++){
        for(int j=0;j<grid[0].length;j++) {
            if(grid[i][j]==1) return -1;   //checking if there are any fresh                                                   oranges left 
        }
     } return time;
    }
}
```
SIMILAR TO -> TIME TAKEN TO BURN A TREE. BUT CONTAINS MULTIPLE BURNING NODES