## 704 Binary Search
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.
You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

- [ ] 2024-08-12: 06:11

 ```c#
public class Solution {
    public int Search(int[] nums, int target) {
        int left = 0;
        int right = nums.Length - 1;
        
        while(left <= right)
        {
            int middle = left + ((right-left)/2);

            if(nums[middle] > target)
            {
                right = middle-1;
            }
            else if(nums[middle] < target)
            {
                left = middle + 1;
            }
            else return middle;
        }
        return -1;
    }
}
```


## 35 Search Insert Position
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [1,3,5,6], target = 5
Output: 2

- [x] 2024-08-12: 05:13

```c#
public class Solution {
    public int SearchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.Length - 1;

        while(left<=right)
        {
            int middle = left + ((right-left) / 2);

            if(nums[middle] < target)
            {
                left = middle + 1;
            }
            else if(nums[middle] > target)
            {
                right = middle - 1;
            }
            else return middle;
        }

        return left;
    }
}
```










