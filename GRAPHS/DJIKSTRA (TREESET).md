```java
class Solution {

    public int[] dijkstra(int V, List<List<int[]>> adj, int src) {

        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        // {distance, node}
        TreeSet<int[]> set = new TreeSet<>(
            (a, b) -> {
                if (a[0] != b[0])
                    return Integer.compare(a[0], b[0]);

                return Integer.compare(a[1], b[1]);
            }
        );

        set.add(new int[]{0, src});

        while (!set.isEmpty()) {

            int[] curr = set.pollFirst();

            int dis = curr[0];
            int node = curr[1];

            for (int[] edge : adj.get(node)) {

                int nei = edge[0];
                int weight = edge[1];

                if (dis + weight < dist[nei]) {

                    // Remove old {distance, node}
                    if (dist[nei] != Integer.MAX_VALUE) {
                        set.remove(new int[]{dist[nei], nei});
                    }

                    // Update distance
                    dist[nei] = dis + weight;

                    // Add new {distance, node}
                    set.add(new int[]{dist[nei], nei});
                }
            }
        }

        return dist;
    }
}
```

**IMPORTANT PART**
```java
set.remove(new int[]{dist[nei], nei});
```
same as priority queue, but can remove duplicate node from the treeset if the node is already visited.