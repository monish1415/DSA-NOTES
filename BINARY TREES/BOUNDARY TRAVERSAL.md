```java
class Solution {

    ArrayList<Integer> ans = new ArrayList<>();

    public ArrayList<Integer> boundary(Node root) {

        if(root == null)
            return ans;

        // Root
        if(!(root.left == null && root.right == null))
            ans.add(root.data);

        leftBoundary(root.left);
        leaves(root);
        rightBoundary(root.right);

        return ans;
    }

    void leftBoundary(Node root){

        while(root != null){

            if(!(root.left == null && root.right == null))
                ans.add(root.data);

            if(root.left != null)
                root = root.left;
            else
                root = root.right;
        }
    }

    void leaves(Node root){

        if(root == null)
            return;

        if(root.left == null && root.right == null){
            ans.add(root.data);
            return;
        }

        leaves(root.left);
        leaves(root.right);
    }

    void rightBoundary(Node root){

        Stack<Integer> stack = new Stack<>();

        while(root != null){

            if(!(root.left == null && root.right == null))
                stack.push(root.data);

            if(root.right != null)
                root = root.right;
            else
                root = root.left;
        }

        while(!stack.isEmpty())
            ans.add(stack.pop());
    }
}
```
**3 STEPS:**
->TRAVERSE LEFT BOUNDARY AND ADD THEM TO LIST EXCLUDING LEAF NODES
->TRAVERSE THROUGH THE TREE AGAIN AND ADD LEAF NODES TO THE LIST BY RECURSION
->TRAVERSE RIGHT BOUNDARY AND ADD THEM TO THE LIST

REQUIRES 3 TRAVERSES THROUGH THE TREE