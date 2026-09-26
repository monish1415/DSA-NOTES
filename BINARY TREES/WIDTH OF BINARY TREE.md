```java

class Pair {
    TreeNode node;
    long index;

    public Pair(TreeNode node, long index) {
        this.index = index;
        this.node = node;
    }
}

class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        Queue<Pair> queue = new ArrayDeque<>();
        queue.add(new Pair(root, 0));
        int ans = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            long first = 0;
            long last = 0;
            int min = (int) queue.peek().index;
            for (int i = 0; i < size; i++) {
                Pair p = queue.poll();
                TreeNode node = p.node;
                long index = p.index;
                if (i == 0)
                    first = index;
                if (i == size - 1)
                    last = index;
                if (node.left != null)
                    queue.add(new Pair(node.left, 2 * (index - min) + 1));
                if (node.right != null)
                    queue.add(new Pair(node.right, 2 * (index - min) + 2));
            }
            int newAns = (int) (last - first + 1);
            ans = Math.max(ans, newAns);
        }
        return ans;
    }
}
```
