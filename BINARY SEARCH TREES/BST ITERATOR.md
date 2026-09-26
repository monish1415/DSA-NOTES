```java
class BSTIterator {
    private Stack<TreeNode> stack = new Stack<>();

    public BSTIterator(TreeNode root) {
        pushLeft(root);
    }
    
    public int next() {
        TreeNode node = stack.pop();
        if(node.right!=null) pushLeft(node.right);
        return node.val;
    }
    
    public boolean hasNext() {
        return !stack.isEmpty();
    }
    private void pushLeft(TreeNode node) {
        while(node!=null) {
            stack.push(node);
            node=node.left;
        }
    }
}
```
## Intuition

- Push all left nodes initially.
- `next()` pops the top (next smallest node).
- If the popped node has a right child, push all its left descendants.
- Every node is pushed once and popped once.

Time:
- Constructor: O(h)
- `next()`: Amortized O(1)
- `hasNext()`: O(1)

Space:
- O(h)