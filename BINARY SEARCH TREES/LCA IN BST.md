```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while(root!=null) {
            if(root.val>p.val&&root.val>q.val) {
                root=root.left;
            }
            else if(root.val<p.val&&root.val<q.val) {
                root=root.right;
            }
            else break;
        } return root;
    }
}
```
## Intuition

- If both nodes are smaller, go left.
- If both nodes are larger, go right.
- Otherwise, the current node is the split point (LCA).