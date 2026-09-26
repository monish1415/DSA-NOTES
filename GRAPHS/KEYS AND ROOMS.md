```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        int max=0;
        HashSet<Integer> set = new HashSet<>();
        Queue<Integer> queue = new ArrayDeque<>();
        queue.add(0);
        set.add(0);
        while(!queue.isEmpty()) {
            int key = queue.poll();
            set.add(key);
            for(int i:rooms.get(key)) {
                if(!set.contains(i)) {
                    set.add(i);
                    queue.add(i);
                }
            }
        } return rooms.size()==set.size();
    }
}
```
A BFS SOLUTION. ADDS EVERY ROOM NUMBER IN THE SET IF ITS KEY IS FOUND. RETURN IF ROOM SIZE = SET SIZE. THIS GIVES US IF EVERY ROOM IS VISITED OR NOT.