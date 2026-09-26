```java
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;

        while (root != null) {
            if (p.val < root.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }

        return successor;
    }
}
```
## Intuition

- Right subtree exists → successor = leftmost node of right subtree.
- Otherwise, search from root.
- Every time you go left, store current node as a potential successor.
- Last stored node is the answer.