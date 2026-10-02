```java
public int[][] floydWarshall(int V, int[][] edges) {

    int INF = 1_000_000_000;
    int[][] dist = new int[V][V];

    // Initialize
    for (int i = 0; i < V; i++) {
        Arrays.fill(dist[i], INF);
        dist[i][i] = 0;
    }

    // Add edges
    for (int[] edge : edges) {
        int u = edge[0];
        int v = edge[1];
        int w = edge[2];

        dist[u][v] = w;
    }

    // Floyd-Warshall
    for (int via = 0; via < V; via++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {

                if (dist[i][via] != INF && dist[via][j] != INF) {
                    dist[i][j] = Math.min(
                        dist[i][j],
                        dist[i][via] + dist[via][j]
                    );
                }
            }
        }
    }

    return dist;
}
```
### Floyd-Warshall

* **All-pairs shortest path**
* Works with **negative edges**
* Uses `dist[][]`

Core idea:

```java
for (int k = 0; k < V; k++)
    for (int i = 0; i < V; i++)
        for (int j = 0; j < V; j++)
            dist[i][j] = Math.min(dist[i][j],
                                   dist[i][k] + dist[k][j]);
```

`k` = intermediate vertex.

**Negative cycle:** `dist[i][i] < 0`

**Complexity:** `O(V³)` time, `O(V²)` space.
