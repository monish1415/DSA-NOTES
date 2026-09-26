```java
class Solution {
    public int countNodes(TreeNode root) {
        if(root==null) return 0;
        int left=lHeight(root.left);
        int right=rHeight(root.right);

        if(left==right) return (int)(Math.pow(2,left+1))-1;
        return countNodes(root.left)+countNodes(root.right) +1;
    }
    private int lHeight(TreeNode root) {
        int count=0;
        while(root!=null) {
            root=root.left;
            count++;
        } return count;
    }
     private int rHeight(TreeNode root) {
        int count=0;
        while(root!=null) {
            root=root.right;
            count++;
        } return count;
    }
}
```