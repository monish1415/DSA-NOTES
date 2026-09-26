```java
class Solution {
    int target =0,count=0;
    public int kthSmallest(TreeNode root, int k) {
        inorder(root,k);
        return target;
    }
    private void inorder(TreeNode root,int k) {
        if(root==null) return;
        inorder(root.left,k);
        count++;
        if(count==k) target = root.val;
         inorder(root.right,k);
    }
}
```
## Intuition

- Inorder traversal of a BST gives nodes in **sorted order**.
- Count each visited node.
- When `count == k`, that node is the kth smallest.
- (Optional optimization) Stop traversal once the answer is found.