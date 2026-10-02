```java
class Solution {
    int infinity=100000000;
    public ArrayList<Integer> bellmanFord(int V, int[][] edges, int src) {
        // code here
        ArrayList<Integer> dist = new ArrayList<>();
        for(int i=0;i<V;i++){
            dist.add(infinity);
        }
        dist.set(src,0);
        for(int i=0;i<V-1;i++){
            for(int edge[]:edges){
                int u=edge[0];
                int v=edge[1];
                int w=edge[2];
                if(dist.get(u)!=infinity&&dist.get(u)+w<dist.get(v)) {
                    dist.set(v,dist.get(u)+w);
                }
            }
        }
        for(int edge[]:edges){
            int u=edge[0];
            int v=edge[1];
            int w=edge[2];
            if(dist.get(u)!=infinity&&dist.get(u)+w<dist.get(v)) {
                ArrayList<Integer> list = new ArrayList<>();
                list.add(-1);
                return list;
            }
        }
        return dist;
    }
}
```

### Bellman-Ford

* Finds shortest paths in a **weighted graph**.
* Works with **negative edge weights**.
* Can detect **negative-weight cycles**.

**Algorithm:**

1. `dist[src] = 0`, others = `∞`
2. Relax every edge **V − 1 times**:

   ```java
   if (dist[u] + w < dist[v])
       dist[v] = dist[u] + w;
   ```
3. One extra iteration:

   * If any distance still decreases → **negative cycle**.

**Why V − 1?**
A shortest path can have at most `V − 1` edges.

**Complexity:** `O(VE)` time, `O(V)` space.

**Remember:**
**Bellman-Ford = Relax all edges V−1 times + check once for negative cycle.**
