```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int color[] = new int[graph.length];
        for(int i=0;i<graph.length;i++) {
            if(color[i]==0) {
                if(!bfs(graph,color,i)) return false;
            }
        } return true;
    }
    private boolean bfs(int[][] graph,int[] color,int i) {
        Queue<Integer> queue = new ArrayDeque<>();
        queue.add(i);
        color[i]=1;
        while(!queue.isEmpty()) {
            int node = queue.poll();
            for(int j:graph[node]) {
                if(color[j]==0) {
                    color[j]= -(color[node]);
                    queue.add(j);
                } else if(color[node]==color[j]) {
                    return false;
                }
            } 
        } return true;
    }
}
```
COLOR THE INITIAL NODE TO 1. THEN COLOR ITS CHILDREN TO NEGATIVE OF ITS COLOR IF ITS CHILDREN ARE NOT COLORED (COLOR=0). IF THE COLOR OF CHILDREN AND PARENT IS THE SAME RETURN FALSE.