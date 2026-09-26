```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {

        List<Integer> ans = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        while(root != null || !stack.isEmpty()){

            while(root != null){
                stack.push(root);
                root = root.left;
            }

            root = stack.pop();
            ans.add(root.val);
            root = root.right;
        }

        return ans;
    }
}
```
GOES TO THE FARTHEST LEFT AND ADDS THE NODE VAL TO THE LIST. THEN ADDS THE ROOT.
GOES TO THE RIGHT ROOT AND REPEATS THE PROCES WHILE STORING ALL THE TRAVERSED ELEMENTS IN A STACK
**INORDER**  **TRAVERSAL** **:** LEFT=>ROOT=>RIGHT    