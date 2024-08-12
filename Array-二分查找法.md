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


## 34 Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.
If target is not found in the array, return [-1, -1].
You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

- [ ] 2024-08-12: 16:42

```c#
public class Solution {
    public int[] SearchRange(int[] nums, int target) {

        // left和right是不包含target的最近位置
        int leftBorder = GetLeftBorder(nums,target);
        int rightBorder = GetRightBorder(nums,target);
        if(leftBorder == -2 || rightBorder == -2) return new int[]{-1,-1};
        if(rightBorder - leftBorder > 1) return new int[]{leftBorder + 1, rightBorder -1};
        return new int[]{-1,-1};
    }

    public int GetRightBorder(int[] nums, int target)
    {
        int left = 0;
        int right = nums.Length - 1;
        int rightBorder = -2;

        while(left<=right)
        {
            int middle = left + ((right-left)/2);
            if(nums[middle] > target)
            {
                right = middle - 1;
            }
            else
            {
                left = middle + 1;
                rightBorder = left;
            }
        }
        return rightBorder;
    }

    public int GetLeftBorder(int[] nums, int target)
    {
        int left = 0;
        int right = nums.Length - 1;
        int leftBorder = -2;

        while(left <= right)
        {
            int middle = left + ((right-left)/2);
            if(nums[middle] >= target)
            {
                right = middle - 1;
                leftBorder = right;
            }
            else 
            {
                left = middle + 1;
            }
        }
        return leftBorder;
    }
}
```

## 69 Sqrt(x)
Given a non-negative integer x, return the square root of x rounded down to the nearest integer. The returned integer should be non-negative as well.
You must not use any built-in exponent function or operator.
For example, do not use pow(x, 0.5) in c++ or x ** 0.5 in python.

Example 1:

Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.

- [ ]2024-08-12: 06:56

```c#
public class Solution {
    public int MySqrt(int x) {
        if(x == 0) return 0;

        int left = 1;
        int right = x;

        while(left<=right)
        {
            int middle = (right+left)/2;
            // 除法防止溢出
            if(middle < x/middle)
            {
                left = middle + 1;
            }
            else if(middle > x/middle)
            {
                right = middle - 1;
            }
            else return middle;
        }
        // 返回右边因为用的左闭右开
        return right;
    }
}
```







