```java
class Solution {
    
    static int time=0;
    static ArrayList<Integer> articulationPoints(int V, int[][] edges) {
        // code here
        int dis[]=new int[V];
        int low[]=new int[V];
        boolean ap[]=new boolean[V];
        Arrays.fill(dis,-1);
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        ArrayList<Integer> ans = new ArrayList<>();
        for(int i=0;i<V;i++) adjList.add(new ArrayList<>());
        for(int i=0;i<edges.length;i++){
            adjList.get(edges[i][0]).add(edges[i][1]);
            adjList.get(edges[i][1]).add(edges[i][0]);
        }
        for(int i=0;i<V;i++) {
            if(dis[i]==-1) dfs(adjList,dis,low,ap,i,-1);
        }
        for(int i=0;i<V;i++){
            if(ap[i]) ans.add(i);
        }
        if(ans.isEmpty())ans.add(-1);
        return ans;
    }
    private static void dfs(ArrayList<ArrayList<Integer>> adjList,int[] dis,int[] low,boolean[] ap,int i,int parent){
        dis[i]=time;
        low[i]=time;
        time++;
        int children=0;
        for(int j:adjList.get(i)) {
            if(j==parent) continue;
            if(dis[j]==-1) {
                children++;
                dfs(adjList,dis,low,ap,j,i);
                low[i]=Math.min(low[i],low[j]);
                if(parent!=-1&&low[j]>=dis[i]) ap[i]=true;
            }
            else{
                low[i]=Math.min(low[i],dis[j]);
            }
        }  if(parent==-1&&children>1) ap[i]=true;
    }
}
```
## INTUTION
A NODE WHEN REMOVED DIVIDES THE GRAPH INTO MULTIPLE COMPONENTS IS AN ARTICULATION NODE.
THIS ALGORITHM IS SIMILAR TO "BRIDGES IN A GRAPH". IN BRIDGES THE EDGE REMOVAL CONDITION IS
```java
 if(low[j]>dis[i]) ans.add(new ArrayList<>(List.of(i,j)));
```

IN A.P THE NODE REMOVAL CONDITION IS 
```java
 if(parent!=-1&&low[j]>=dis[i]) ap[i]=true;
```
THE '=' SAYS THAT, THE COMPONENTS WHICH ARE CONNECTED TO THE OTHER COMPONENTS CANNOT ACCESS EACH OTHER WHEN THE ARTICULATION POINT IS REMOVED.
IN BRIDGES, WE USE ONLY '>' BUT NOT '>=' BECAUSE REMOVING JUST AN EDGE DOES'NT NECESSARILY DESTROY THE PATH TO THE OTHER COMPONENT, BUT REMOVING THE ARTICULATION NODE COMPLETELY DESTROYS THE PATH TO THE OTHER COMPONENT. SO WE CONSIDER THE PARENT NODE ALSO AS AN "A.P" IF ITS CHILD NODES HAVE A LOW VALUE EQUAL TO ITS DISCOVERY VALUE(OR GREATER TOO.)

DIRECTLY ADDING THE A.P MAY RESULT IN DUPLICATE VALUES IN THE LIST. SO USING A FREQUENCY ARRAY TO TRACK THE A.P IS BETTER.
A SPECIAL CONDITION MUST BE USED TO CHECK IF A ROOT IS AN A.P.