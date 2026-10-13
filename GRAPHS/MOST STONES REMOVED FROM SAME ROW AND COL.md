```java
class Solution {
    int parent[];
    int size[];
    int find(int x){
        if(parent[x]==x) return x;
        return parent[x]=find(parent[x]);
    }
    void union(int u,int v){
        int a=find(u);
        int b=find(v);
        if(a==b) return;
        if(size[a]>size[b]) {
            parent[b]=a;
            size[a]+=size[b];
        }
        else{
            parent[a]=b;
            size[b]+=size[a];
        }
    }
    public int removeStones(int[][] stones) {
        int maxRow=0,maxCol=0;
        for(int stone[]:stones) {
            maxRow=Math.max(maxRow,stone[0]);
            maxCol=Math.max(maxCol,stone[1]);
        }
        parent=new int[maxRow+maxCol+2];
        size=new int[parent.length];
        for(int i=0;i<parent.length;i++) {
            parent[i]=i;
            size[i]=1;
        }
        for(int stone[]:stones) union(stone[0],maxRow+1+stone[1]);
        Set<Integer> components = new HashSet<>();
        for(int stone[]:stones) components.add(find(stone[0]));
        return stones.length-components.size();
    }
}
```
## INTUTION
CONSIDER ROWS AND COLS AS SEPARATE NODES (COL=TOTAL ROWS+1+COL). CALCULATE THE TOTAL ROWS AND COLS AND INITIALIZE THE PARENT ARRAY WITH LENGTH ROWS+COLS+2.

RUN A LOOP ON STONES ARRAY AND UNION THE ROW AND VIRTUAL ROW (COL). USE A HASHSET TO COUNT NO.OF UNIQUE VALUES IN THE PARENT ARRAY -> NO.OF COMPONENTS OR NO.OF STONES LEFT (1 COMP LEAVES 1 STONE BEHIND).
RETURN TOTAL STONES-LEFT OUT STONES.