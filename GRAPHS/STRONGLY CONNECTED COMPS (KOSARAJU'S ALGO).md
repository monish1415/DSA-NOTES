```java
class Solution {
    Deque<Integer> stack = new ArrayDeque<>();
    public int countSCC(int V, int[][] edges) {
        // code here
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        ArrayList<ArrayList<Integer>> adjListT = new ArrayList<>();
        for(int i=0;i<V;i++){
            adjList.add(new ArrayList<>());
            adjListT.add(new ArrayList<>());
        }
        for(int i=0;i<edges.length;i++){
            adjList.get(edges[i][0]).add(edges[i][1]);
            adjListT.get(edges[i][1]).add(edges[i][0]);
        }
        boolean vis[] = new boolean[V];
        for(int i=0;i<V;i++){
            if(!vis[i]) dfs1(adjList,vis,i);
        }
        Arrays.fill(vis,false);
        int scc=0;
        while(!stack.isEmpty()){
            int node=stack.pop();
            if(!vis[node]) {
                dfs2(adjListT,vis,node);
                scc++;
            }
        }
        return scc;
    }
    private void dfs1(ArrayList<ArrayList<Integer>> adjList,boolean[] vis,int node) {
        vis[node]=true;
        for(int i:adjList.get(node)){
            if(!vis[i]) dfs1(adjList,vis,i);
        }
        stack.push(node);
    }
    private void dfs2(ArrayList<ArrayList<Integer>> adjList,boolean[] vis,int node) {
        vis[node]=true;
        for(int i:adjList.get(node)) {
            if(!vis[i]) dfs2(adjList,vis,i);
        }
    }
}
```
## INTUTION
SCC -> EVERY NODE CAN VISIT EVERY OTHER NODE IN THAT COMPONENT.
THE NODES WHICH CAN STILL VISIT THE OTHER EVEN AFTER THE GRAPH IS REVERSED ARE STRONGLY CONNECTED COMPONENTS/
#### KOSARAJU'S ALGORITHM (3 STEPS)
*  PERFORM DFS AND STORE ALL THE NODES IN A STACK, SO THAT WE CAN HAVE THE LAST FINISHED NODE AT THE TOP AND PERFORM DFS AGAIN (WHICH IS NOT POSSIBLE IF QUEUE IS USED).
* REVERSE THE GRAPH TO CHECK THE PROPERTY OF SCC's.
* PERFORM DFS AGAIN USING THE FIRST NODE IN THE STACK. SO THE SCC's OF THAT NODE GETS VISITED AND CANNOT BE PROCESSES AGAIN.
USE A COUNTER AND INCREMENT FOR EVERY UNVISITED NODE IN THE STACK WHICH GIVES US THE STRONGLY CONNECTED COMPONENTS.

