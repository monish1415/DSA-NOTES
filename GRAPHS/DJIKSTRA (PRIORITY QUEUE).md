```java
class Solution {

    public int[] dijkstra(int V, List<List<int[]>> adj, int src) {

        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);

        dist[src] = 0;

        // {distance, node}
        PriorityQueue<int[]> pq = new PriorityQueue<>(
            (a, b) -> Integer.compare(a[0], b[0])
        );

        pq.add(new int[]{0, src});

        while (!pq.isEmpty()) {

            int[] current = pq.poll();

            int distance = current[0];
            int node = current[1];

            // Skip outdated entry
            if (distance > dist[node])
                continue;

            for (int[] edge : adj.get(node)) {

                int neighbour = edge[0];
                int weight = edge[1];

                if (distance + weight < dist[neighbour]) {

                    dist[neighbour] = distance + weight;

                    pq.add(new int[]{
                        dist[neighbour],
                        neighbour
                    });
                }
            }
        }

        return dist;
    }
}
```