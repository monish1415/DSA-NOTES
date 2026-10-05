## Floyd-Warshall
```java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        int[][] dist=new int[n][n];
        for(int i=0;i<n;i++){
            Arrays.fill(dist[i],Integer.MAX_VALUE);
        }
        for(int[] arr: edges){
            int u=arr[0];
            int v=arr[1];
            int wt=arr[2];
            dist[u][v]=wt;
            dist[v][u]=wt;
        }
        // Floyd warshall algo.
        for(int k=0;k<n;k++){
            for(int i=0;i<n;i++){
                if(i==k) continue;
                for(int j=0;j<n;j++){
                    if(j==k) continue;
                    if(dist[i][k]!=Integer.MAX_VALUE && dist[k][j]!=Integer.MAX_VALUE){
                        dist[i][j]=Math.min(dist[i][j], dist[i][k]+dist[k][j]);
                    }                    
                }
            }
        }
        int minCity=-1;
        int minCount=Integer.MAX_VALUE;
        for(int i=0;i<n;i++){
            int count=0;
            for(int j=0;j<n;j++){
                if(i==j) continue;
                if(dist[i][j]<=distanceThreshold) count++;
            }
            if(count<=minCount){
                minCount=count;
                minCity=i;
            }
        }
        return minCity;
    }
}
```

## DJIKSTRA
```java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        List<List<int[]>> adjList = new ArrayList<>();
        int ans[] = new int[n];
        for(int i=0;i<n;i++){
            adjList.add(new ArrayList<>());
        }
        for(int i=0;i<edges.length;i++){
            adjList.get(edges[i][0]).add(new int[]{edges[i][1],edges[i][2]});
            adjList.get(edges[i][1]).add(new int[]{edges[i][0],edges[i][2]});
        }
        int dist[]=new int[n];
        for(int i=0;i<n;i++){
            Arrays.fill(dist,Integer.MAX_VALUE);
            dist[i]=0;
            PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->Integer.compare(a[1],b[1]));
            pq.add(new int[]{i,0});
            while(!pq.isEmpty()){
                int curr[]=pq.poll();
                if(curr[1]>distanceThreshold) continue;
                for(int nei[]:adjList.get(curr[0])){
                    if(curr[1]+nei[1]<dist[nei[0]]){
                        dist[nei[0]]=curr[1]+nei[1];
                        pq.add(new int[]{nei[0],dist[nei[0]]});
                    }
                }
            }
            for(int j=0;j<n;j++){
                if(dist[j]<=distanceThreshold) ans[j]++;
            }
        } 
        int min=0;
        for(int i=1;i<n;i++){
            if(ans[i]<=ans[min]) min=i;
        }
        return min;
    }
}
```