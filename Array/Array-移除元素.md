# 数组-移除元素

|Date\Question|27-E|26-E|283-E|844-E|977-E|
|:----:|:----:|:----:|:----:|:----:|:----:|
|2024-08-13|Y|Y|Y|Y|Y|

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
## 283 Move Zeroes

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

- [x] 2024-08-13: 16:05

```c#
public class Solution {
    public void MoveZeroes(int[] nums) {
        int curr = 0;
        for(int i = 0; i < nums.Length; i++)
        {
            if(nums[i]!=0)
            {
                nums[curr] = nums[I];
                // 只有当quick比slow快的时候才用置空本位数
                if(curr < i) nums[i] = 0;
                curr++;
            }
        }
    }
}
```

## 844 Backspace String Compare

Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.
Note that after backspacing an empty text, the text will continue empty.

Example 1:
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".

- [x] 2024-08-13: 05:29

```c#
public class Solution {
    public bool BackspaceCompare(string s, string t) {
        return RemoveCharacters(s).ToString() == RemoveCharacters(t).ToString();
    }

    public StringBuilder RemoveCharacters(string input)
    {
        StringBuilder sb = new StringBuilder();

        int curr = 0;

        for(int i = 0; i < input.Length;i++)
        {
            if(input[i]!='#')
            {
                sb.Append(input[i]);
                curr++;
            }
            else
            {
                if(sb.Length>0) sb.Remove(sb.Length-1,1);
            }
        }
        return sb;
    }
}
```
因为类似于取一个放一个，也可以用stack解决
```c#
public class Solution {
    public bool BackspaceCompare(string s, string t) {
        return RemoveCharacters(s) == RemoveCharacters(t);
    }

    public string  RemoveCharacters(string input)
    {
        Stack<char> s = new Stack<char>();
        for(int i = 0; i < input.Length; i++)
        {
            if(input[i] != '#') s.Push(input[i]);
            else if(s.Count > 0) s.Pop();
        }
        char[] res = s.ToArray();
        return new string(res);
    }
}
```
## 977 Squares of a Sorted Array

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example 1:
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].

- [x] 2024-08-13: 16:47

```c#
public class Solution {
    public int[] SortedSquares(int[] nums) {
        
        for(int i = 0; i< nums.Length; i++)
        {
            nums[i] = nums[i] * nums[i];
        }

        Array.Sort(nums);
        return nums;
    }
}
```
题解：双指针思路，把最小的（大概率是负数后的平方）和右边最大的对比，然后放回数组中
```c#
public class Solution {
    public int[] SortedSquares(int[] nums) {
        int k = nums.Length - 1;
        int[] result = new int[nums.Length];
        for (int i = 0, j = nums.Length - 1;i <= j;){
            if (nums[i] * nums[i] < nums[j] * nums[j]) {
                result[k--] = nums[j] * nums[j];
                j--;
            } else {
                result[k--] = nums[i] * nums[i];
                i++;
            }
        }
        return result;
    }
}
```
