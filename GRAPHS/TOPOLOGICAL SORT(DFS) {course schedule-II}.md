```java
class Solution {
    Stack<Integer> stack = new Stack<>();
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adjList = new ArrayList<>();
        for(int i=0;i<numCourses;i++){
            adjList.add(new ArrayList<>());
        }
        for(int i=0;i<prerequisites.length;i++){
            adjList.get(prerequisites[i][1]).add(prerequisites[i][0]);
        }
        boolean[] vis = new boolean[numCourses];
        boolean[] pathVis = new boolean[numCourses];
        for(int i=0;i<numCourses;i++){
            if(!vis[i]) {
                if(topo(adjList,vis,pathVis,i)) return new int[0];
            }
        }
        int order[] = new int[numCourses];
        int i=0;
        while(!stack.isEmpty()){
            order[i++]=stack.pop();
        } return order;
    }
    private boolean topo(List<List<Integer>> adjList,boolean[] vis,boolean[] pathVis,int i) {
        vis[i] =true;
        pathVis[i]=true;
        for(int j:adjList.get(i)){
            if(!vis[j]){
                if(topo(adjList,vis,pathVis,j)) return true;
            } else if(pathVis[j]) return true;
        } stack.push(i);
        pathVis[i]=false;
        return false;
    }
}
```