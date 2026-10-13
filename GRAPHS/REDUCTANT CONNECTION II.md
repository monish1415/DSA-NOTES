```java
class Solution {

    int[] parent;

    int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    boolean union(int u, int v) {
        int a = find(u);
        int b = find(v);

        if (a == b) return false;

        parent[a] = b;
        return true;
    }

    public int[] findRedundantDirectedConnection(int[][] edges) {

        int n = edges.length;
        int[] parentNode = new int[n + 1];

        int[] edge1 = null;
        int[] edge2 = null;

        // Find a node with two parents
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];

            if (parentNode[v] == 0) {
                parentNode[v] = u;
            } else {
                edge1 = new int[]{parentNode[v], v}; // Earlier edge
                edge2 = edge;                       // Later edge
                break;
            }
        }

        // Initialize DSU
        parent = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            parent[i] = i;
        }

        // Try removing the later edge
        for (int[] edge : edges) {
            if (edge == edge2) continue;

            if (!union(edge[0], edge[1])) {
                // A cycle remains: remove the earlier edge
                return edge1 == null ? edge : edge1;
            }
        }

        // No cycle remains: remove the later edge
        return edge2;
    }
}
```
## INTUTION:
TO CONVERT A GRAPH INTO A ROOTED TREE OF N NODES, WE NEED TO REMOVE AN UNNECESSARY EDGE.
A EDGE CAN BE REMOVED IF:
* THE NODE HAS AN INDEGREE GREATER THAN 1
* THE GRAPH HAS A CYCLE
* BOTH
TO CHECK IF A NODE HAS INDEGREE >1 WE CAN MAKE AN ARRAY AND STORE THE PARENT OF THE NODE IF THE VALUE IS ZERO. IF ITS NOT ZERO THE NODE ALREADY HAS A PARENT AND STORE THE 1ST EDGE AND THE NEW EDGE. IF WE REMOVE ONE OF THE EDGES THE GRAPH GETS CONVERTED TO A ROOTED TREE. MAKE THE NEW EDGE INVALID FROM THE LIST

RUN ANOTHER LOOP AND UNION ALL THE EDGES. IF A CYCLE IS FOUND THE 1ST EDGE IS THE CULPRIT AND RETURN IT. IF NO CYCLE RETURN SECOND EDGE(CAUSED THE CYCLE IN CASE 3 AND LAST INPUT BASED ON CASE 1).

IF NO VALUES ARE ASSIGNED TO THE FIRST EDGE, THEN THE NODES DOESNT HAVE INDEGREE>1.
=>CASE 2. SO RETURN THE CURRENT EDGE WHERE CYCLE IS FOUND IF EDGE1=NULL.