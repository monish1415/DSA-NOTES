```java
class Solution {
    static int parent[];
    static int rank[];
    static int find(int x){
    if(parent[x]==x) return x;
    return parent[x]=find(parent[x]);
    }
    static void union(int u,int v){
        int rootA=find(u);                         //DISJOINT SET FUNCTIONS
        int rootB=find(v);
        if(rootA==rootB) return;
        if(rank[rootA]>rank[rootB]){
            parent[rootB]=rootA;
        }
        else if(rank[rootB]>rank[rootA]) {
            parent[rootA]=parent[rootB];
        }
        else{
            parent[rootA]=rootB;
            rank[rootB]++;
        }
    }
-----------------------------------------------------------------------------------
    static int kruskalsMST(int V, int[][] edges) {
        // code here
        Arrays.sort(edges,(a,b)->Integer.compare(a[2],b[2]));
        parent = new int[V];
        rank = new int[V];
        for(int i=0;i<V;i++){
            parent[i]=i;
        }
        int sum=0,count=0;                        //MAIN LOGIC
        for(int edge[]:edges){
            if(find(edge[0])!=find(edge[1])) {
                sum+=edge[2];
                count++;
                union(edge[0],edge[1]);
            }
            if(count==V-1) break;
        }
        return sum;
    }
}
```

### Kruskal's Algorithm

* Finds **Minimum Spanning Tree (MST)**.
* Sort all edges by **increasing weight**.
* Use **DSU (Disjoint Set Union)** to detect cycles.
* If `find(u) != find(v)` → take the edge and `union(u,v)`.
* Stop after selecting `V - 1` edges.

### DSU

* `parent[]` → represents the DSU tree.
* `find(x)` → finds the **ultimate parent/root**.
* **Path compression:** `parent[x] = find(parent[x])`.
* `rank[]` → keeps trees shallow.
* **Union by rank:** attach the lower-rank root under the higher-rank root.

### Complexity

* Sorting: `O(E log E)`
* DSU operations: approximately `O(E)`
* Overall: **`O(E log E)`**
