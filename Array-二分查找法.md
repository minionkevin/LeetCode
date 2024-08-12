# 数组-二分查找

|Date\Question|704-E|35-E|34-M|69-E|367-E|
|:----:|:----:|:----:|:----:|:----:|:----:|
|2024-08-12|X|Y|X|X|Y|


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

## 367 Valid Perfect Square
Given a positive integer num, return true if num is a perfect square or false otherwise.
A perfect square is an integer that is the square of an integer. In other words, it is the product of some integer with itself.
You must not use any built-in library function, such as sqrt.

Example 1:
Input: num = 16
Output: true
Explanation: We return true because 4 * 4 = 16 and 4 is an integer.

- [x]2024-08-12: 02:06

```c#
public class Solution {
    public bool IsPerfectSquare(int num) {
        if(num == 0) return true;
        int left = 1;
        int right = num;

        while(left <= right)
        {
            int middle = (left+right)/2;

            if(middle < num/middle) left = middle + 1;
            else if(middle > num/middle) right = middle - 1;
            else
            {
                if(middle * middle == num) return true;
                else return false;
            }
        }
        return false;
    }
}
```
简化版本
```c#
public class Solution {
    public bool IsPerfectSquare(int num) {
        if(num == 0) return true;
        int left = 1;
        int right = num;
        int middle = 0;

        while(left <= right)
        {
            middle = (left+right)/2;

            if(middle < num/middle) left = middle + 1;
            else if(middle > num/middle) right = middle - 1;
            else break;
        }
        return middle * middle == num;
    }
}
```c#



