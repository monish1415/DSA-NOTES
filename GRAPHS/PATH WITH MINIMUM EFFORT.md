```java
class Tuple{
    int row;
    int col;
    int effort;
    Tuple(int row,int col,int effort){
        this.row=row;
        this.col=col;
        this.effort=effort;
    }
}
class Solution {
    int dr[] = {-1,1,0,0};
    int dc[] = {0,0,-1,1};
    public int minimumEffortPath(int[][] heights) {
        int dist[][]=new int[heights.length][heights[0].length];
        for(int i=0;i<heights.length;i++){
             Arrays.fill(dist[i],Integer.MAX_VALUE);
        }
        dist[0][0]=0;

        PriorityQueue<Tuple> pq = new PriorityQueue<>((a,b)->Integer.compare(a.effort,b.effort));
        pq.add(new Tuple(0,0,0));
        while(!pq.isEmpty()){
            Tuple t = pq.poll();
            if(t.row==heights.length-1&&t.col==heights[0].length-1) return t.effort;
            for(int k=0;k<4;k++){
                int nr = t.row+dr[k];
                int nc = t.col+dc[k];
               
                if(nr>=0&&nr<heights.length&&nc>=0&&nc<heights[0].length) {
                    int newEff=Math.max(t.effort,Math.abs(heights[t.row][t.col]-heights[nr][nc]));
                    if(newEff<dist[nr][nc]) {
                    dist[nr][nc]=newEff;
                    pq.add(new Tuple(nr,nc,newEff));
                    }
                } 
            }
        } return 0;
    }
}
```

MAKE A 2D DISTANCE ARRAY, IF THE NEW ABSOLUTE DIFFERENCE BETWEEN 2 ELEMENTS IS GREATER THAN THE PREVIOUS DIFFERENCE, PUT THE NEW DIFFERENCE IN THAT POSITION OF THE ARRAY, ELSE PUT THE PREVIOUS DIFFERENCE. IF THE POINTER IS AT THE LAST INDEX RETURN THE EFFORT VALUE, BECAUSE PRIORITY QUEUE ALWAYS POLLS THE SMALLEST VALUE. THEREFORE YOU WILL BE GETTING THE MIN EFFORT VALUE AMONG ALL THE PATHS.