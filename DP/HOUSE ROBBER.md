MEMOIZATION
```java
class Solution {
    int[] dp;

    public int rob(int[] nums) {
        dp = new int[nums.length];
        Arrays.fill(dp, -1);
        return solve(nums, nums.length - 1);
    }

    private int solve(int[] nums, int ind) {
        if (ind == 0) return nums[0];
        if (ind < 0) return 0;

        if (dp[ind] != -1) return dp[ind];

        int take = nums[ind] + solve(nums, ind - 2);
        int notTake = solve(nums, ind - 1);

        return dp[ind] = Math.max(take, notTake);
    }
}
```

TABULATION (SPACE OPTIMIZED):
```java
int prev2 = 0;
int prev1 = nums[0];

for (int i = 1; i < nums.length; i++) {
    int curr = Math.max(nums[i] + prev2, prev1);
    prev2 = prev1;
    prev1 = curr;
}

return prev1;
```

ADJACENT HOUSES ARE CONNECTED BY A SECURITY LINK,IF TWO ADJACENT HOUSES ARE ROBBED ALARM GETS TURNED ON. MAX LOOT THE ROBBER CAN STEAL
## INTUTION
WE TARGET TO ROB THE HOUSE WHICH IS AT THE LAST IN THE ARRAY. WE CAN EITHER ROB THE Nth HOUSE OR N-1th HOUSE NOT BOTH. IF WE ROB Nth HOUSE WE CAN THEN ROB ANY HOUSE OTHER THAN N-1th. WE ASSUME WE CAN ROB EITHER N-2th OR N-3rd HOUSE TO BUILD UP A RECURSION WHICH GOES TILL FIRST INDEX LEAVING ITS ADJACENT HOUSES.

BY USING TABULATION WE CAN STORE THE LARGEST AMOUNT OF LOOT ROBBED FROM EACH INDEX (ONLY CONSIDERING HOUSE BEFORE THE INDEX), AND FINALLY WE WILL HAVE 2 HOUSES LEFT i.e N AND N-1 HOUSE. WE CHOOSE THE MAX OF THEM.
USE 2 VARIABLES INSTEAD OF AN ARRAY TO SPACE OPTIMIZE.

**FOR HOUSE ROBBER II WHERE HOUSES ARE IN A CYCLE, CONSIDER TWO CASES WHERE ONLY ONE OF 1ST AND LAST HOUSES ARE ROBBED.**