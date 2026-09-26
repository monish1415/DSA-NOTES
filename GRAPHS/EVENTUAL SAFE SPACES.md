```java
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int state[] = new int[graph.length];
        List<Integer> list = new ArrayList<>();
        for(int i=0;i<graph.length;i++) {
            if(dfs(graph,state,i)) list.add(i);
        } 
        return list;
    }
    private boolean dfs(int[][] graph,int[] state,int i){
        if(state[i]==1) return false;
        if(state[i]==2) return true;
        state[i]=1;
        for(int j:graph[i]) {
            if(!dfs(graph,state,j)) return false;
        }
        state[i]=2;
        return true;
    }
}
```
AFTER CALING DFS FOR A NODE, PUT THE NODE IN STATE:1. CALL DFS FOR ALL THE NODES CONNECTED TO THIS NODE. IF ITS A TERMINAL NODE STATE BECOMES 2 AND RETURNS TRUE, MARKING IT AS A SAFE NODE. IF ANY NODE RETURN FALSE ALL THE NODES CONNECTED TO IT RETURN FALSE. IF THE NODE REACHES A TERMINAL NODE, PUT THE NODE IN STATE:2 AND RETURN TRUE.