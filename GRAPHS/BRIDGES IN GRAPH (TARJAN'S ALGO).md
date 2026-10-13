```java
class Solution {
    List<List<Integer>> ans = new ArrayList<>();
    int time=0;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        List<List<Integer>> adjList = new ArrayList<>();
        int dis[]=new int[n];
        int low[]=new int[n];
        Arrays.fill(dis,-1);
        for(int i=0;i<n;i++) adjList.add(new ArrayList<>());
        for(int i=0;i<connections.size();i++){
            int u=connections.get(i).get(0);
            int v=connections.get(i).get(1);
            adjList.get(u).add(v);
            adjList.get(v).add(u);
        }
        for(int i=0;i<n;i++){
            if(dis[i]==-1) dfs(adjList,dis,low,i,-1);
        }
        return ans;
    }
    private void dfs(List<List<Integer>> adjList,int[] dis,int[] low,int i,int parent){
        dis[i]=time;
        low[i]=time;
        time++;
        for(int j:adjList.get(i)) {
            if(j==parent) continue;
            if(dis[j]==-1) {
                dfs(adjList,dis,low,j,i);
                low[i]=Math.min(low[i],low[j]);
                if(low[j]>dis[i]) ans.add(new ArrayList<>(List.of(i,j)));
            }
            else {
                low[i]=Math.min(low[i],low[j]);
            }
        }
    }
}
```
## INTUTION
THE QUESTION ASKS US TO RETURN ALL THE EDGES BETWEEN 2 ANY COMPONENTS IN A GRAPH.
WHEN THE EDGE IS REMOVED THE GRAPH IS DIVIDED INTO 2 COMPONENTS.

WE INITIALIZE TIME=0, DIS[]={-1},LOW[]. IF THE NEIGBOURING NODE HAS'NT BEEN VISITED (i.e) DIS[NODE]=-1, WE PERFORM DFS BY PASSING THE PARENT.IF THE DFS ENCOUNTERS A VISITED NODE WHICH IS NOT THE PARENT, IT STORES ITS DIS NUMBER(NODE NUM) IN LOW ARRAY. EVERY TIME A NEW NODE IS VISITED WE STORE THE TIME WHEN ITS VISITED IN DIS AND LOW AND INCREMENT TIME.

THE BASIC IDEA OF THIS ALGORITHM IS IF WE ENCOUNTER A CC ALL THE CHILD NODES WILL HAVE A LOW NUMBER SMALLER THAN THE DIS NUMBER OF THE PARENT NODE.
MOST OF THE TIME THE NODES IN CC WILL HAVE A SAME LOW NUMBER.

ANY NODE WHICH HAS ITS LOW NUMBER GREATER THAN ITS PARENT LOW NUMBER SIGNIFIES THAT THE CHILD NODE CAN NEVER CONNECT TO THE PARENT NODE VIA OTHER NODES.
SO THIS EDGE IS CONSIDERED AS A BRIDGE BETWEEN TWO CC's.

