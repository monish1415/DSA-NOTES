```java
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root==null) return "";
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if(node==null) sb.append("null,");
            else {
                sb.append(node.val).append(",");
                queue.add(node.left);
                queue.add(node.right);
            }
        } return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if(data.equals("")) return null;
        String arr[] = data.split(",");
        TreeNode root = new TreeNode(Integer.parseInt(arr[0]));
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        int i=0;
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if(!arr[++i].equals("null")) {
                node.left = new TreeNode(Integer.parseInt(arr[i]));
                queue.add(node.left);
            }
            if(!arr[++i].equals("null")) {
                node.right = new TreeNode(Integer.parseInt(arr[i]));
                queue.add(node.right);
            }
        } return root;
    }
}
```
