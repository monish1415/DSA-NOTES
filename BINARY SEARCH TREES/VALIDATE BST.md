```java
class Solution {
    long val = Long.MIN_VALUE;
    public boolean isValidBST(TreeNode root) {
        return inorder(root);
    }
    private boolean inorder(TreeNode root) {
        if(root==null) return true;
        boolean prev = inorder(root.left);
        if(prev&&root.val>val) {
            val = root.val;
            return inorder(root.right);
        } 
        return false;
    }
}
```
## Intuition

- Inorder traversal of a valid BST is **strictly increasing**.
- Compare each node with the previously visited node.
- If `current <= previous`, it's **not** a BST.
- Store the current value as the new previous.
- Use `long prev = Long.MIN_VALUE` since node values are `int`.