# Daily challenge

## 3151 Special Array I

An array is considered special if every pair of its adjacent elements contains two numbers with different parity.
You are given an array of integers nums. Return true if nums is a special array, otherwise, return false.

Example 1:
Input: nums = [1]
Output: true
Explanation:
There is only one element. So the answer is true.

- [x] 2024-08-12: 05:51
```c#
public class Solution {
    public bool IsArraySpecial(int[] nums) {

        if(nums.Length ==0) return true;
        // 需要检查前后两个数字是否奇偶一样
        
        List<int> result = new List<int>();
        for(int i = 0; i < nums.Length; i++)
        {
            int curr = nums[i]%2;
            if(result.Count > 0 && result[result.Count-1] == curr) return false;
            else result.Add(curr);
        }
        return true;
    }
}
```
- [x] 2024-08-12: 03:28
```c#
public class Solution {
    public bool IsArraySpecial(int[] nums) {
        if(nums.Length <= 1) return true;
        Stack<int> s = new Stack<int>();

        s.Push(nums[0]%2);
        for(int i = 1; i < nums.Length; i++)
        {
            int result = nums[i]%2;
            if(result!=s.Peek())
            {
                s.Pop();
                s.Push(result);
            }
            else return false;
        }
        return true;
    }
}
```
题解版本，实际不需要一个list去装，只需要一个last来存放之前的答案
```c#
public class Solution {
    public bool IsArraySpecial(int[] nums) {
        var last = -1;
        foreach(var num in nums)
        {
            var current = num % 2;
            if(current == last) return false;
            last = current;
        }
        return true;
    }
}
```

## Special Array II

An array is considered special if every pair of its adjacent elements contains two numbers with different parity.
You are given an array of integer nums and a 2D integer matrix queries, where for queries[i] = [fromi, toi] your task is to check that 
subarray
 nums[fromi..toi] is special or not.
Return an array of booleans answer such that answer[i] is true if nums[fromi..toi] is special.

Example 1:
Input: nums = [3,4,1,2,6], queries = [[0,4]]
Output: [false]
Explanation:
The subarray is [3,4,1,2,6]. 2 and 6 are both even.

- [ ] 2024-08-13: 28:02

官方题解
```c#
public class Solution {
    public bool[] IsArraySpecial(int[] nums, int[][] queries) {
        int n = nums.Length;
        int[] dp = new int[n];
        Array.Fill(dp, 1);
        for (int i = 1; i < n; i++) {
            if (((nums[i] ^ nums[i - 1]) & 1) != 0) {
                dp[i] = dp[i - 1] + 1;
            }
        }

        bool[] res = new bool[queries.Length];
        for (int i = 0; i < queries.Length; i++) {
            int x = queries[i][0], y = queries[i][1];
            res[i] = dp[y] >= y - x + 1;
        }
        return res;
    }
}
```
