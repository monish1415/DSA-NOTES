```java
class NodeData {
    int max;
    int min;
    int sum;
    public NodeData(int max,int min,int sum) {
        this.max=max;
        this.min=min;
        this.sum=sum;
    }
}
class Solution {
    int maxSum=0;
    public int maxSumBST(TreeNode root) {
        dfs(root);
        return maxSum;
    }
    private NodeData dfs(TreeNode root) {
        if(root==null) return new NodeData(Integer.MIN_VALUE,Integer.MAX_VALUE,0);
        NodeData left = dfs(root.left);
        NodeData right = dfs(root.right);
        if(left.max<root.val&&right.min>root.val) {
            int sum = left.sum+right.sum+root.val;
            maxSum = Math.max(maxSum,sum);
            return new NodeData(Math.max(right.max,root.val),Math.min(left.min,root.val),sum);
        }
        return new NodeData(Integer.MAX_VALUE,Integer.MIN_VALUE,0);
    }
}
```

## Intuition

For every subtree, return enough information so its parent can determine whether the current subtree is a BST.

Each recursive call returns:

- `min` → Smallest value in the subtree.
- `max` → Largest value in the subtree.
- `sum` → Sum of the subtree.

A subtree is a BST only if:

```java
left.max < root.val && root.val < right.min
```

If valid:

```java
sum = left.sum + right.sum + root.val;
```

Update the global answer and return the new `min`, `max`, and `sum`.

If invalid:

- Return impossible `min` and `max` values (`max = +∞`, `min = -∞` in `(max, min)` order) so every ancestor also fails the BST check.
- The `sum` of an invalid subtree is never used again because ancestors first check the BST condition before using `sum`.

## Why this is Tree DP

Each node solves a subproblem:

> "What information should I return so my parent can decide whether we're together a BST?"

The parent combines the results of its left and right children in **O(1)**.

Each subtree is solved exactly once.

## Complexity

- **Time:** `O(n)`
- **Space:** `O(h)` (recursion stack)