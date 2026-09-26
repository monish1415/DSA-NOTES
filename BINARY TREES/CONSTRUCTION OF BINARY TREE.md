**FROM PREORDER AND INORDER** 

```java
class Solution {
     Map<Integer,Integer> map = new HashMap<>();
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        for(int i=0;i<inorder.length;i++) {
            map.put(inorder[i],i);
        } return build(preorder,0,preorder.length-1,inorder,0,inorder.length-1);
    }
    private TreeNode build(int preorder[],int preStart,int preEnd,int inorder[],int inStart,int inEnd) {
        if(preStart>preEnd||inStart>inEnd) return null;
        TreeNode root= new TreeNode(preorder[preStart]);
        int index = map.get(root.val);
        int left = index - inStart;
        root.left=build(preorder,preStart+1,preStart+left,inorder,inStart,index-1);
        root.right = build(preorder,preStart+left+1,preEnd,inorder,index+1,inEnd);
        return root;
    }
}
```


**FROM POSTORDER AND INORDER**

```java
class Solution {
    Map<Integer,Integer> map = new HashMap<>();
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        for(int i=0;i<inorder.length;i++) {
            map.put(inorder[i],i);
        } 
        return build(postorder,0,postorder.length-1,inorder,0,inorder.length-1);
    } 
    private TreeNode build(int postorder[],int pStart,int pEnd,int inorder[],int inStart,int inEnd) {
        if(pStart>pEnd||inStart>inEnd) return null;
        TreeNode root = new TreeNode(postorder[pEnd]);
        int index = map.get(root.val);
        int left = index-inStart;
        root.left=build(postorder,pStart,pStart+left-1,inorder,inStart,index-1);
        root.right = build(postorder,pStart+left,pEnd-1,inorder,index+1,inEnd);
        return root;
    }
}
```

PASS THE ARGUMENTS OF TRAVERSAL "**ARRAYS**", THEIR "**START AND END INDEX**" (I.E), THE REDUCED TRAVERSALS ARRAYS