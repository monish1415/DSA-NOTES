USING A DP ARRAY (SPACE->O(N))
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int dp[] = new int[triangle.get(triangle.size()-1).size()];
        for(int i=0;i<dp.length;i++) {
            dp[i]=triangle.get(triangle.size()-1).get(i);
        }
        for(int i=triangle.size()-2;i>=0;i--) {
            int val=dp[i+1];
            for(int j=i;j>=0;j--) {
                int newVal=triangle.get(i).get(j)+Math.min(dp[j],val);
                val=dp[j];
                dp[j]=newVal;
            }
        }
        return dp[0];
    }
}
```
EACH CELL CAN TAKE A VALUE FROM EITHER THEIR SAME COL OR THEIR +1 COL FROM THEIR NEXT ROW. USE A DP ARRAY TO STORE THE ELEMENTS FROM THE LAST ROW AND USE A 'VAL' VARIABLE TO STORE THE +1 COL VALUE BEFORE CHANGING ITS VALUE. THEN TAKE THE MIN OF THE VALUE AT SAME COL IN THE NEXT ROW AND ITS NEXT COL VALUE WHICH IS STORED IN VAL VARIABLE. ADD THE MIN VALUE TO THE CURRENT VALUE AND STORE THE VALUE AT THE SAME INDEX IN DP ARRAY.

CHANGING IN-PLACE(CHANGES THE INPUT ARRAY)
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        for(int i=triangle.size()-2;i>=0;i--) {
            for(int j=i;j>=0;j--) {
                int newVal = Math.min(triangle.get(i+1).get(j),triangle.get(i+1).get(j+1));
                triangle.get(i).set(j,triangle.get(i).get(j)+newVal);
            }
        }
        return triangle.get(0).get(0);
    }
}
```