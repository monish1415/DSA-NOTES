```java
class Solution {
    int dr[]={-1,1,0,0};
    int dc[]={0,0,-1,1};
    int parent[];
    int size[];
    int find(int x) {
        if(parent[x]==x) return x;
        return parent[x]=find(parent[x]);
    }
    void union(int u,int v){
    int a = find(u);
    int b = find(v);
    if(a==b) return;
    if(size[a]<size[b]) {
        parent[a]=b;
        size[b]+=size[a];
    } 
    else {
        parent[b]=a;
        size[a]+=size[b];
    }
    }
    public int largestIsland(int[][] grid) {
        parent=new int[grid.length*grid.length];
        size=new int[parent.length];                   //initializing cells to 
        for(int i=0;i<grid.length;i++){                //their parent number
            for(int j=0;j<grid.length;j++) {
                parent[grid.length*i+j]= grid.length*i+j; //size of all cells set
                size[grid.length*i+j]=1;                  // to '1'
            }
        } 
        for(int i=0;i<grid.length;i++) {
            for(int j=0;j<grid.length;j++) {        //union-ing all the 1's and 
                if(grid[i][j]==1){                  // and storing their total size
                    for(int k=0;k<4;k++) {
                        int nr=dr[k]+i;
                        int nc=dc[k]+j;
                        if(nr>=0&&nr<grid.length&&nc>=0&&nc<grid.length&&grid[nr][nc]==1){
                            union(nr*grid.length+nc,i*grid.length+j);
                        }
                    }  
                }
            }
        }
        int maxSize=0;
        for(int i=0;i<grid.length;i++){
            for(int j=0;j<grid.length;j++){ 
                if(grid[i][j]==1) continue;             //traversing through all 
                HashSet<Integer> set = new HashSet<>(); //all cells which are 0's
                for(int k=0;k<4;k++) {
                    int nr=dr[k]+i;
                    int nc=dc[k]+j;
                    if(nr>=0&&nr<grid.length&&nc>=0&&nc<grid.length&&grid[nr][nc]==1) {
                        set.add(find(nr*grid.length+nc));
                    }                   //adding their uParent num to set so no 
                } int s=0;              // duplicate's size is counted
                for(int p:set) {      
                    s+=size[p];          //adding the sizes of all parents in set
                }
                maxSize=Math.max(maxSize,s+1); 
            } 
        }
        return maxSize==0? grid.length*grid.length:maxSize;
    }     //edge case when all the cells are equal to '1'
}
```
### Making A Large Island — DSU

* Build DSU for all `1` cells by unioning adjacent land.
* `size[root]` = size of that island.
* For every `0`, check its 4 neighbors.
* Use a `HashSet` to avoid counting the same island twice.
* Sum `size[root]` of distinct neighboring islands + `1` for the flipped cell.
* Take maximum.
* If `maxSize == 0`, grid was all `1`s → answer = `n × n`.

**Complexity:** `O(n² α(n²))` time, `O(n²)` space.
