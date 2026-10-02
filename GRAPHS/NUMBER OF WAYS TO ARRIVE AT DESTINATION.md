```java
class Pair{
    int node;
    long time;
    Pair(int node,long time){
        this.node=node;
        this.time=time;
    }
}
class Solution {
    long MOD=1000000007;
    
    public int countPaths(int n, int[][] roads) {
        List<List<Pair>> adjList = new ArrayList<>();
        for(int i=0;i<n;i++){
            adjList.add(new ArrayList<>());
        }
        for(int i=0;i<roads.length;i++){
            adjList.get(roads[i][0]).add(new Pair(roads[i][1],roads[i][2]));
             adjList.get(roads[i][1]).add(new Pair(roads[i][0],roads[i][2]));
        }
        
        long dist[] = new long[n];
        long ways[] = new long[n];
        Arrays.fill(dist,Long.MAX_VALUE);
        dist[0]=0;
        ways[0]=1;
        
        PriorityQueue<Pair> pq = new PriorityQueue<>((a,b)->Long.compare(a.time,b.time));
        pq.add(new Pair(0,0));
        while(!pq.isEmpty()){
            Pair curr=pq.poll();
            if(curr.time>dist[curr.node]) continue;
            
            for(Pair nei:adjList.get(curr.node)) {
                if(curr.time+nei.time<dist[nei.node]){
                    dist[nei.node]=curr.time+nei.time;
                    ways[nei.node]=ways[curr.node];
                    pq.add(new Pair(nei.node,dist[nei.node]));
                }
                else if(curr.time+nei.time==dist[nei.node]) {
                    ways[nei.node]=(ways[nei.node]+ways[curr.node])%MOD;
                }
            }
        }
        return (int)ways[n-1];
    }
}
```
### Count Ways to Arrive at Destination

Use **Dijkstra + path counting**.

* `dist[i]` → shortest time to reach `i`
* `ways[i]` → number of shortest paths to reach `i`

For each neighbor:

```java
if (newDist < dist[nei]) {           //newDist=curr.time+nei.time;
    dist[nei] = newDist;
    ways[nei] = ways[node];
}
else if (newDist == dist[nei]) {
    ways[nei] += ways[node];
}
```

* Shorter path → replace distance and ways.
* Equal shortest path → add the number of ways.
* Use `long` for distances to avoid overflow.
* Apply `% 1_000_000_007` to `ways`.
