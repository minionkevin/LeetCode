给定一个长度为 n 的 0 索引整数数组 nums。初始位置为 nums[0]。
每个元素 nums[i] 表示从索引 i 向前跳转的最大长度。换句话说，如果你在 nums[i] 处，你可以跳转到任意 nums[i + j] 处:
0 <= j <= nums[i] 
i + j < n
返回到达 nums[n - 1] 的最小跳跃次数。生成的测试用例可以到达 nums[n - 1]。

示例 1:
输入: nums = [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。

- [ ] 2024-08-07: 15:31

```c#
public class Solution {
    public int Jump(int[] nums) {
        int border = 0;
        int maxPosition = 0;
        int steps = 0;

        for(int i = 0; i < nums.Length-1;i++)
        {
            // 找出目前位置能到的max index
            maxPosition = Math.Max(maxPosition, nums[i]+i);
            // 如果在遍历的过程中已经到了此index的边界
            if(i == border)
            {
                // 设置到此位置可以到的max
                border=maxPosition;
                steps++;
               // 多做一个if省略for，直接break也可以
                if(border == nums.Length-1) return steps;
            }
        }
        return steps;
    }
}
```
