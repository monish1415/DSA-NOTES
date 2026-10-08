```java
class Solution {
    int parent[];
    int rank[];
    int find(int x) {
        if(parent[x]==x) return x;
        return parent[x]=find(parent[x]);
    }
    void union(int u,int v) {
        int a=find(u);
        int b=find(v);
        if(a==b) return;
        if(rank[a]>rank[b]) parent[b]=a;
        else if(rank[a]<rank[b]) parent[a]=b;
        else{
            parent[a]=b;
            rank[b]++;
        }
    }
    public int makeConnected(int n, int[][] connections) {
        if(connections.length<n-1) return -1;
        parent=new int[n];
        rank=new int[n];
        int components=n;
        for(int i=0;i<n;i++) parent[i]=i;
        for(int edge[]:connections) {
            if(find(edge[0])!=find(edge[1])) {
                union(edge[0],edge[1]);
                components--;
            }
        }
        return components-1;
    }
}
```

1 UNION MAKES 2 COMPONENT INTO 1 COMPONENT. CALCULATE NO.OFF EDGES REQUIRED TO CONNECT ALL THE LEFT OVER COMPONENTS

```java
return components-1;
```