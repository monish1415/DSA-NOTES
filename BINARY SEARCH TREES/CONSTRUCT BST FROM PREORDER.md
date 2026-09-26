```java
class Solution {
    int index=0;
    public TreeNode bstFromPreorder(int[] preorder) {
        return construct(preorder,Integer.MAX_VALUE);
    }
    private TreeNode construct(int[] preorder,int bound) {
        if(index>preorder.length-1||preorder[index]>bound) return null;
        TreeNode root = new TreeNode(preorder[index++]);
        root.left = construct(preorder,root.val);
        root.right = construct(preorder,bound);
        return root;
    }
}
```
## Intuition

- Preorder = Root → Left → Right.
- Use an upper bound to decide if a node belongs to the current subtree.
- If `preorder[index] > bound`, return `null`.
- Left subtree → bound = `root.val`.
- Right subtree → bound = parent's bound.