```java
class Tuple {

    TreeNode node;
    int row;
    int col;

    public Tuple(TreeNode node,int col,int row) {

        this.row=row;
        this.col=col;
        this.node=node;
    }
 }

class Solution {

    public List<List<Integer>> verticalTraversal(TreeNode root) {
        TreeMap<Integer,TreeMap<Integer,PriorityQueue<Integer>>> map = new TreeMap<>();
        Queue<Tuple> queue = new ArrayDeque<>();

        queue.add(new Tuple(root,0,0));

        while(!queue.isEmpty()) {

            Tuple tuple = queue.poll();
            TreeNode node = tuple.node;
            int col = tuple.col;
            int row = tuple.row;

            if(!map.containsKey(col)) map.put(col,new TreeMap<>());
            if(!map.get(col).containsKey(row)) map.get(col).put(row,new PriorityQueue<>());

            map.get(col).get(row).add(node.val);

            if(node.left!=null) queue.add(new Tuple(node.left,col-1,row+1));
            if(node.right!=null) queue.add(new Tuple(node.right,col+1,row+1));

        }

        List<List<Integer>> ans = new ArrayList<>();

        for(TreeMap<Integer,PriorityQueue<Integer>> rowsMap:map.values()) {
            List<Integer> col = new ArrayList<>();

            for(PriorityQueue<Integer> pq: rowsMap.values()) {
                while(!pq.isEmpty()){
                col.add(pq.poll());
                }
            } ans.add(col);
        }  return ans;
    }
}
```
THIS IS USED TO STORE THE **'X'** AND **'Y'** POSITION OF A TREENODE.
A ROW MAP AND A COL MAP ARE CREATED TO STORE THE VALUES. THE ROW MAP STORES THE VALUES, AND THE COL MAP STORES THE ROW MAPS
**EX:** 2 -> {2 -> [4]}
-  1 -> {1 -> [2]}
   0 -> {0 -> [1], 2 -> [5,6]}
   1 -> {1 -> [3]}
*****C->{R->[ ]}***** 

**TOP VIEW:**
INSTEAD OF MAKING A DOUBLE TREE MAP, MAP A SINGLE TREEMAP AND STORE ONLY THE FIRST VALUE OF EACH COLUMN BY, CHECKING IF MAP EXISTS, IF NOT CREATE THE MAP AND STORE THAT ELEMENT IN THE LIST, OR ELSE JUST GET TO THE NEXT NODE.

**BOTTOM VIEW:**
SIMILAR TO TOP VIEW BUT, CHECK THE COLUMN OF THE NODE, IF THE COL DOES NOT EXIST IN MAP CREATE A KEY OF THAT COLUMN ANS ASSIGN IT THE NODE. IF COL EXISTS REPLACE THE PREVIOUS VALUE WITH THE NEW VALUE. THIS STORES THE LAST NODE OF THAT COLUMN IN THE KEY. AT LAST ITERATE THROUGH THE TREE MAP AND STORE THE VALUES IN A LIST. 