```java
public List<Integer> topoSort(int V, List<List<Integer>> adj) {

    int[] indegree = new int[V];

    for(int i = 0; i < V; i++) {
        for(int node : adj.get(i)) {
            indegree[node]++;
        }
    }

    Queue<Integer> queue = new ArrayDeque<>();

    for(int i = 0; i < V; i++) {
        if(indegree[i] == 0) {
            queue.add(i);
        }
    }

    List<Integer> topo = new ArrayList<>();

    while(!queue.isEmpty()) {

        int node = queue.poll();
        topo.add(node);

        for(int next : adj.get(node)) {
            indegree[next]--;

            if(indegree[next] == 0) {
                queue.add(next);
            }
        }
    }

    return topo;
}
```

**FOR CYCLE DETECTION**
```java
if(topo.size() != V)
    return new ArrayList<>();
```

```
indegree = number of incoming edges.
Add all indegree == 0 nodes to queue.
Remove node → decrease indegree of its neighbors.
If neighbor becomes 0, add it to queue.
topo.size() == V → no cycle.
topo.size() < V → cycle.
Time: O(V + E)
Space: O(V)
```

