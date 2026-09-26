```java
class Solution {
    int max=0;
    public int diameterOfBinaryTree(TreeNode root) {
        Depth(root);
        return max;
    } 
    private int Depth(TreeNode root) {
        if(root==null) return 0;
        int left =Depth(root.left);
        int right = Depth(root.right);
        max=Math.max(max,left+right);
        return 1+Math.max(left,right);
    }
}
```
DIAMETER IS THE LONGEST PATH BETWEEN 2 NODES IN A BINARY TREE. DEPTH CHECKS THE DEPTH OF THE BINARY TREE. THE TOTAL IS COMPARED TO THE TOTAL OF LEFT AND RIGHT NODES OF THE ROOT. MAX NUMBER IS STORED IN THE GLOBAL VARIABLE
