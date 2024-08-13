## 27 Remove Element

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.
Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:
Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.

Example 1:
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

- [x] 2024-08-13: 01:22

```c#
  public class Solution {
    public int RemoveElement(int[] nums, int val) {
    
        int result = 0;

        for(int i = 0; i < nums.Length; i++)
        {
            if(nums[i] != val) 
            {
                // 可以直接用 nums[result++] = num[i]
                nums[result] = nums[i];
                result++;
            }
        }
        return result;
    }
  }
```

## 26 Remove Duplicates from Sorted Array

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.
Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:
Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.

Example 1:
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

- [x] 2024-08-13: 01:05

```c#
public class Solution {
    public int RemoveDuplicates(int[] nums) {
        int result = 1;

        for(int i = result; i < nums.Length; i++)
        {
            if(nums[i]!=nums[i-1]) nums[result++] = nums[i];
        }
        return result;
    }
}
```







