```java
class Solution {

    int[] parent;
    int[] rank;

    int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    void union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);

        if (rootA == rootB) return;

        if (rank[rootA] > rank[rootB]) {
            parent[rootB] = rootA;
        } else if (rank[rootA] < rank[rootB]) {
            parent[rootA] = rootB;
        } else {
            parent[rootA] = rootB;
            rank[rootB]++;
        }
    }

    public List<List<String>> accountsMerge(List<List<String>> accounts) {

        int n = accounts.size();

        parent = new int[n];
        rank = new int[n];

        for (int i = 0; i < n; i++)
            parent[i] = i;

        // email -> account index
        HashMap<String, Integer> map = new HashMap<>();

        // Connect accounts having common emails
        for (int i = 0; i < n; i++) {

            for (int j = 1; j < accounts.get(i).size(); j++) {

                String email = accounts.get(i).get(j);

                if (map.containsKey(email)) {
                    union(i, map.get(email));
                } else {
                    map.put(email, i);
                }
            }
        }

        // root -> emails
        HashMap<Integer, List<String>> merged = new HashMap<>();

        for (String email : map.keySet()) {
            int root = find(map.get(email));

            merged.putIfAbsent(root, new ArrayList<>());
            merged.get(root).add(email);
        }

        List<List<String>> ans = new ArrayList<>();

        for (int root : merged.keySet()) {

            List<String> emails = merged.get(root);
            Collections.sort(emails);

            List<String> account = new ArrayList<>();
            account.add(accounts.get(root).get(0));
            account.addAll(emails);

            ans.add(account);
        }

        return ans;
    }
}
```
### Accounts Merge — DSU

* Treat each **account as a DSU node**.
* If two accounts share an email → `union(account1, account2)`.
* `email → account index` stored in `HashMap`.
* After all unions, group emails by their **DSU root**.
* Sort emails and add the account name.

```text
email → account index
same email → union()
        ↓
find(root)
        ↓
root → all emails
```

**Important:** Initialize DSU:

```java
for(int i=0; i<n; i++)
    parent[i] = i;
```

**Complexity:** `O(E α(N) + E log E)`
(`E log E` mainly for sorting emails)
