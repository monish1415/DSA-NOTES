```java
Stack<TreeNode> stack = new Stack<>();
List<Integer> ans = new ArrayList<>();

if (root != null)
    stack.push(root);

while (!stack.isEmpty()) {

    TreeNode node = stack.pop();
    ans.add(node.val);

    if (node.left != null)
        stack.push(node.left);

    if (node.right != null)
        stack.push(node.right);
}

Collections.reverse(ans);
```
