给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使得出现次数超过两次的元素只出现两次 ，返回删除后数组的新长度。
不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

示例 1：
输入：nums = [1,1,1,2,2,3]
输出：5, nums = [1,1,2,2,3]
解释：函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3。 不需要考虑数组中超出新长度后面的元素。

用时： 26:20
第一次未作出



```c#
public class Solution {
    public int RemoveDuplicates(int[] nums) {
        if(nums.Length <= 2) return nums.Length;
        int result = 1;
        //还是用curr来代表现在更新到的index
        int curr = 1;
        bool isPass = true;

        for(int i = 1; i < nums.Length; i++)
        {
            // 如果前后两位不相同，直接到下一位
            if(nums[i] != nums[i-1])
            {
                result++;
                nums[curr++] = nums[i];
                isPass= true;
            }
            else
            {
                // isPass == true代表前面只有一个此数字
                // 两个相同数字是被允许的
                if(isPass)
                {
                    result++;
                    nums[curr++] = nums[i];
                    isPass = !isPass;
                }
            }
        }
        return result;

    }
}
```

