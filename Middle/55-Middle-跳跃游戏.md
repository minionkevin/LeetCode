给你一个非负整数数组 nums ，你最初位于数组的 第一个下标 。数组中的每个元素代表你在该位置可以跳跃的最大长度。
判断你是否能够到达最后一个下标，如果可以，返回 true ；否则，返回 false 。

示例 1：
输入：nums = [2,3,1,1,4]
输出：true
解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。

- [x] 2024-08-08: 28:26

```c#
public class Solution {
    public bool CanJump(int[] nums) {
        // 处理特殊情况
        if(nums.Length == 1) return true;

        int[] dp = new int[nums.Length];
        int keeper = 0;

        for(int i = 0; i < nums.Length; i++)
        {
            // dp==0代表之前的步骤到不了这一步
            if(i>=1 && dp[i] ==0) return false;
            keeper = i+1;
            // 计算现在的index可以到哪一步存在dp中
            for(int j = nums[i]; j > 0; j--)
            {
                if(keeper >= nums.Length) break;
                dp[keeper]++;
                keeper++;
            }
        }

        return dp[nums.Length-1] != 0;
    }
}
```

官方题解
```c
public class Solution {
    public bool CanJump(int[] nums) {
        int n = nums.Length;
        int rightmost = 0;

        for(int i = 0; i < n; i++)
        {
            if(i <= rightmost)
            {
                // 更新最大可达位置
                rightmost = Math.Max(rightmost, i + nums[i]);
                // 如果最大可抵达位置比数组长，直接成功
                if(rightmost > n-1) return true;
            }
        }
        return false;
    }
}
```

      
