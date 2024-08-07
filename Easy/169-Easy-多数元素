给定一个大小为 n 的数组 nums ，返回其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。
你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1：
输入：nums = [3,2,3]
输出：3

用时： 07:03
日期：2024-08-07



```c#
public class Solution {
    public int MajorityElement(int[] nums) {
        Dictionary<int,int> dic = new Dictionary<int,int>();

        // 统计每个数字出现多少次
        for(int i = 0; i < nums.Length; i++)
        {
            if(dic.ContainsKey(nums[i]))dic[nums[i]]++;
            else dic.Add(nums[i],1);
        }

        int holder = 0;
        int result = 0;

        // 找到出现最多的数字
        foreach(KeyValuePair<int,int> num in dic)
        {
            if(num.Value > holder)
            {
                result = num.Key;
                holder = num.Value;
            }
        }
        return result;

    }
}
```
