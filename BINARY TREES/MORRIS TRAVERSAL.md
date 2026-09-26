```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        TreeNode curr = root;
        while(curr!=null) {
            if(curr.left==null) {
                list.add(curr.val);
                curr=curr.right;
            } else {
            TreeNode prev = curr.left;
            while(prev.right!=null&&prev.right!=curr) prev=prev.right;
            if(prev.right==null) {
                prev.right=curr;
                curr=curr.left;
            } else {
                prev.right=null;
                list.add(curr.val);
                curr=curr.right;
            }
        }
        }
        return list;
    }
}
```

RIGHT MOST NODE OF LEFT SUB-TREE SHOULD POINT TO THE ROOT. TRAVERSE THROUGH THE LEFT SIDE OF THE TREE AND SET UP POINTER TO THE ROOT AT THR RIGHT MOST LEAF NODE. 