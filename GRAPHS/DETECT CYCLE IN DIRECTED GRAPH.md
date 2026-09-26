```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adjList = new ArrayList<>();
        for(int i=0;i<numCourses;i++) {
            adjList.add(new ArrayList<>());
        }
        for(int i=0;i<prerequisites.length;i++) {
            adjList.get(prerequisites[i][1]).add(prerequisites[i][0]);
        }
//*******************************************************************************//
        boolean pathVis[] = new boolean[numCourses]; 
        boolean vis[] = new boolean[numCourses];
        for(int i=0;i<numCourses;i++) {
            if(!vis[i]) {
                if(dfs(adjList,pathVis,vis,i)) return false;
            }
        } return true;
    } 
    private boolean dfs(List<List<Integer>> adjList,boolean[] pathVis,boolean[] vis,int i) {
        vis[i]=true;
        pathVis[i]=true;
        for(int j:adjList.get(i)) {
            if(!vis[j]) {
                if(dfs(adjList,pathVis,vis,j)) return true;
            }
            if(pathVis[j]) return true;
        } 
        pathVis[i]=false;
        return false;
    }
}                                                    
```
CHECK IF THE NODE IS VISITED IN THE SAME PATH. IF NOT VISITED, REMOVE AS VISITED FROM THE PATH VISITED ARRAY.
