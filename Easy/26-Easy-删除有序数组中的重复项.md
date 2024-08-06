给你一个 非严格递增排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数。
考虑 nums 的唯一元素的数量为 k ，你需要做以下事情确保你的题解可以被通过：
更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。nums 的其余元素与 nums 的大小不重要。
返回 k 。

示例 1：
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。

用时： 3:30


```c#
public class Solution {
    public int RemoveDuplicates(int[] nums) {
        int holder = 1;
        int curr = 1;

        //从index=1开始查询，因为index=0的时候这个数字一定是不重复的
        //curr是目前查询的位置
        //holder是插入的位置

        while(curr < nums.Length)
        {
            if(nums[curr] != nums[curr-1])
            {
                nums[holder] = nums[curr];
                holder++;
            }
            curr++;
        }
        return holder;
    }
}
```

```c#
public class Solution {
    public int RemoveDuplicates(int[] nums) {
        int result = 1;
        int curr = 1;

        for(int i = 1; i<nums.Length;i++)
        {
            if(nums[i] != nums[i-1])
            {
                result++;
                nums[curr] = nums[i];
                curr++;
            }
        }
        return result;
    }
}
```
