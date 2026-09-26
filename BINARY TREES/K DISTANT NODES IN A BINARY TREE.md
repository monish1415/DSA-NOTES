```java
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        Queue<TreeNode> queue = new ArrayDeque<>();
        Map<TreeNode,TreeNode> map = new HashMap<>(); //parent map
        queue.add(root);
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if(node.left!=null) {
                map.put(node.left,node);
                queue.add(node.left);
            }
            if(node.right!=null) {
                map.put(node.right,node);
                queue.add(node.right);
            }
        } List<Integer> list = new ArrayList<>();
        Set<TreeNode> set = new HashSet<>();
        queue.add(target);
        set.add(target);
        int d=0;
        while(!queue.isEmpty()) {
            int size = queue.size();
            if(d==k) break;
            for(int i=0;i<size;i++) {
        
                TreeNode node = queue.poll();
                if(node.left!=null&&!set.contains(node.left)) {
                    set.add(node.left);
                    queue.add(node.left);
                } 
                if(node.right!=null&&!set.contains(node.right)) {
                    set.add(node.right);
                    queue.add(node.right);
                }
                if(map.containsKey(node)&&!set.contains(map.get(node))) {
                    set.add(map.get(node));
                    queue.add(map.get(node));
                } 
            } d++;
        } while(!queue.isEmpty()) {
            list.add(queue.poll().val);
        } return list;
    }
}
```