# Leetcode 416. Partition Equal Subset Sum

[Explanation Video Link on Youtube](https://youtu.be/iuGhv6iNlHo)

[B站英文解说视频链接](https://www.bilibili.com/video/BV1ZP4y187Gm)

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        
        if (sum % 2 != 0) {
            return false;
        }
        
        int target = sum / 2;
        vector<bool> dp(target + 1, false);
        dp[0] = true;
        
        for (int i = 0; i < nums.size(); i++) {
            for (int j = target - nums[i]; j >= 0; j--) {
                if (dp[j]) {
                    dp[nums[i] + j] = true;
                }
            }
        }
        
        return dp[target];
    }
};
```
