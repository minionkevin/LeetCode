给定一个整数数组 nums，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。

示例 1:
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]

- [ ] 2024-08-07：19:05

```c#
//超出时间限制 理论可行
public class Solution {
    public void Rotate(int[] nums, int k) {
        for(int i = 0 ; i< k;i++)
        {
            RotateNums(nums);
        }
    }

    public void RotateNums(int[] nums)
    {
        int last = nums[nums.Length-1];
        for(int i = nums.Length-1 ; i > 0 ; i--)
        {
            nums[i] = nums[i-1];
        }
        nums[0] = last;
    }
}
```

```c#
public class Solution {
    public void Rotate(int[] nums, int k) {

        Dictionary<int,int> dic = new Dictionary<int,int>();
        // 记录每个数字和对应的index
        // 用index做key唯一性
        for(int i = 0; i < nums.Length;i++)
        {
            dic.Add(i,nums[i]);
        }
        
        foreach(var item in dic)
        {
            // 计算每个value的位置直接将数组中的数字替换
            nums[(item.Key + k) % nums.Length] = item.Value;
        }
    }
}
```
