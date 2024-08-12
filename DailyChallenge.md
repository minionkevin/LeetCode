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
