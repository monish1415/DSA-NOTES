```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        if(root==null) return ans;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        int flag=0;
        while(!queue.isEmpty()) {
            int n = queue.size();
            List<Integer> temp = new ArrayList<>();
            for(int i=0;i<n;i++) {
                TreeNode node = queue.poll();
                temp.add(node.val);
                if(node.left!=null) queue.add(node.left);
                if(node.right!=null) queue.add(node.right);
            }
            if(flag==1) {
                Collections.reverse(temp);
                ans.add(temp);
                flag=0;
            } else {
                ans.add(temp);
                flag=1;
            }
        } return ans;
    }
}
```
TRAVERSES THROUGH THE BINARY TREE LEVEL BY LEVEL. ROOT IS STORED IN A QUEUE AND A WHILE LOOP IS RUNNED TILL THE QUEUE IS EMPTY. A TEMPORARY LIST IS CREATED TO STORE THE VALUES OF THE NODES. A FOR LOOP OF SIZE OF QUEUE IS CREATED AND ALL THE NODES IN THE QUEUE ARE STORED IN THE TEMP LIST BY THEIR VALUES. THE LEFT AND RIGHT NODES ARE ADDED TO THE QUEUE IF THEY ARE NOT NULL.
