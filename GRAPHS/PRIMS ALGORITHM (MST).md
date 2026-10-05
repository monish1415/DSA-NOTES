```java
class Solution {
    public int spanningTree(int V, int[][] edges) {
        // code here
        ArrayList<ArrayList<int[]>> adjList = new ArrayList<>();
        for(int i=0;i<V;i++){
            adjList.add(new ArrayList<>());
        }
        for(int i=0;i<edges.length;i++){
            adjList.get(edges[i][0]).add(new int[]{edges[i][1],edges[i][2]});
            adjList.get(edges[i][1]).add(new int[]{edges[i][0],edges[i][2]});
        }
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->Integer.compare(a[1],b[1]));
        pq.add(new int[]{0,0});
        boolean vis[] = new boolean[V];
        int sum=0;
        int count=0;
        while(!pq.isEmpty()){
            int curr[] = pq.poll();
            if(vis[curr[0]]) continue;
            if(count==vis.length) return sum;
            vis[curr[0]]=true;
            count++;
            sum+=curr[1];
            for(int nei[]:adjList.get(curr[0])){
                if(!vis[nei[0]]) {
                    pq.add(new int[]{nei[0],nei[1]});
                }
            }
        }
        return sum;
    }
}

```
### Prim's Algorithm (PriorityQueue)

* Finds the **Minimum Spanning Tree (MST)**.
* Start from any vertex and repeatedly choose the **minimum-weight edge connecting the MST to an unvisited vertex**.
* Use a **min PriorityQueue** storing `{node, weight}`.
* Skip already visited nodes.

```java
if (vis[node]) continue;
vis[node] = true;
sum += weight;
```

Then add all unvisited neighbors to the PQ.

**Complexity:** `O(E log E)` approximately, `O(E)` space.

**For 1584:** No adjacency list is given; calculate the Manhattan distance between points when adding neighbors.
