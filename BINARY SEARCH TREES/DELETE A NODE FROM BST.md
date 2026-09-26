```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root==null) return null;
        if(root.val>key) {
            root.left = deleteNode(root.left,key);
        } else if(root.val<key) root.right = deleteNode(root.right,key);
        else {
            if(root.left==null) return root.right;
            if(root.right==null) return root.left;

            TreeNode right = root.right;
            TreeNode lastRight = lastRight(root.left);
            lastRight.right = right;
           return root.left;
        } return root;
    } 
    private TreeNode lastRight(TreeNode node) {
        while(node.right!=null) {
            node = node.right;
        }
        return node;
    }
}
```
## Intuition

- Search for the node recursively.
- If one child is null, return the other child.
- If both children exist:
  - Save `root.right`.
  - Find the rightmost node of `root.left`.
  - Attach the saved right subtree there.
  - Return `root.left`.

**Remember:** Only the node with `root.val == key` is deleted. All previous recursive calls just reconnect the returned subtree.