```java
class Solution {
    int[] parent, rank;

    int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    void union(int a, int b) {
        a = find(a);
        b = find(b);

        if (a == b) return;

        if (rank[a] < rank[b]) parent[a] = b;
        else if (rank[a] > rank[b]) parent[b] = a;
        else {
            parent[a] = b;
            rank[b]++;
        }
    }

    public List<Integer> numOfIslands(int rows, int cols, int[][] operators) {
        int n = rows * cols;

        parent = new int[n];
        rank = new int[n];
        Arrays.fill(parent, -1);

        List<Integer> ans = new ArrayList<>();
        int count = 0;

        int[][] dir = {{1,0},{-1,0},{0,1},{0,-1}};

        for (int[] op : operators) {
            int r = op[0], c = op[1];
            int cell = r * cols + c;

            // Already land
            if (parent[cell] != -1) {
                ans.add(count);
                continue;
            }

            // Add new island
            parent[cell] = cell;
            count++;

            for (int[] d : dir) {
                int nr = r + d[0];
                int nc = c + d[1];

                if (nr < 0 || nr >= rows || nc < 0 || nc >= cols)
                    continue;

                int neighbor = nr * cols + nc;

                if (parent[neighbor] == -1)
                    continue;

                if (find(cell) != find(neighbor)) {
                    union(cell, neighbor);
                    count--;
                }
            }

            ans.add(count);
        }

        return ans;
    }
}
```
### Number of Islands II

* Grid starts completely **water**.
* Land is added one cell at a time.
* Use **DSU** to maintain connected islands.
* Add land → `count++`.
* Check its **4 neighbors**.
* If neighbor is land and belongs to a different component → `union()` and `count--`.
* Convert `(r,c)` to 1D index: `r * cols + c`.
* `parent[i] = -1` means water.

**Complexity:** `O(K α(R×C))` time, `O(R×C)` space.
