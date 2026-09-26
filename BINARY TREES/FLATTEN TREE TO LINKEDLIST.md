 
**REVERSE PREORDER** [SPACE O[H]]

```java
class Solution {
    TreeNode prev = null;
    public void flatten(TreeNode root) {
        if(root==null) return;
        flatten(root.right);
        flatten(root.left);
        root.right=prev;
        root.left=null;
        prev = root;
    }
}
```
GO TO THE RIGHT MOST LEAF NODE AND ADD IT TO PREV WHICH IS INITALLY NULL. TRAVERSE THROUGH THE ENTIRE TREE AND ADDING THE NODES TO PREV.

**MORRIS** [SPACE O(1)]

```java
class Solution {
    public void flatten(TreeNode root) {
        TreeNode curr=root;
        while(curr!=null) {
            if(curr.left!=null) {
            TreeNode prev = curr.left;
            while(prev.right!=null) prev=prev.right;
            prev.right=curr.right;
            curr.right=curr.left;
            curr.left=null;
            }
            curr=curr.right;
        }
    }
}
```
GO TO THE RIGHT MOST LEAF NODE IN LEFT SUB-TREE AND ATTACH THE RIGHT SUB-TREE TO IT. NOW PUT THE LEFT SUB-TREE TO RIGHT AND PUT LEFT AS NULL. THEN GO TO THE NEXT NODE IN THE RIGHT SIDE.