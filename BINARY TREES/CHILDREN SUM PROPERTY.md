```java
class Solution {

    public static void changeTree(BinaryTreeNode<Integer> root) {

        if (root == null)
            return;

        int child = 0;

        if (root.left != null)
            child += root.left.data;

        if (root.right != null)
            child += root.right.data;

        // Push parent's value down
        if (child < root.data) {
            if (root.left != null)
                root.left.data = root.data;

            if (root.right != null)
                root.right.data = root.data;
        }
        // Pull children's sum up
        else {
            root.data = child;
        }

        changeTree(root.left);
        changeTree(root.right);

        int total = 0;

        if (root.left != null)
            total += root.left.data;

        if (root.right != null)
            total += root.right.data;

        if (root.left != null || root.right != null)
            root.data = total;
    }
}
```
