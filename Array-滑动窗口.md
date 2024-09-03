# 数组-滑动窗口

|Date\Question|209-M|904-M|76-H|
|:----:|:----:|:----:|:----:|
|2024-08-13|X|X|N|

## 209 Minimum Size Subarray Sum
M
Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray
whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

Example 1:
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

- [ ] 2024-08-14: 08:51
- [ ] 2024-09-03: 12:00

理论上没问题，但是超出时间限制
```c#
public class Solution {
    public int MinSubArrayLen(int target, int[] nums) {
        int result = nums.Length+1;
        for(int i = 0; i < nums.Length; i++)
        {
            int sum = 0;
            for(int j = i; j < nums.Length;j++)
            {
                sum += nums[j];
                int diff = j - i + 1;
                if(sum >= target && diff < result) 
                {
                    result = diff;
                    break;
                } 
            }
        }
        return result == nums.Length+1 ? 0 : result;
    }
}
```
题解:把两个for换成一个for的形式，用滑动窗口
```c#
public class Solution {
    public int MinSubArrayLen(int target, int[] nums) {

        int left = 0;
        int sum = 0;
        int result = nums.Length+1;

        for(int right = 0; right < nums.Length; right++)
        {
            sum += nums[right];
            // 窗口值大于target，start移动
            while(sum>=target)
            {
                result = Math.Min(result, right-left+1);
                sum-=nums[left++];
            }
        }
        return result == nums.Length+1 ? 0 : result;
    }
}
```

## 904 Fruit Into Baskets
M
You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.
You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:
You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
Once you reach a tree with fruit that cannot fit in your baskets, you must stop.
Given the integer array fruits, return the maximum number of fruits you can pick.

Example 1:
Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.

- [ ] 2024-08-14: 41:44
- [ ] 2024-09-03: 08:23

理论没问题但是又超时啦
```c#
public class Solution {
    public int TotalFruit(int[] fruits) {
        if(fruits.Length ==1)return 1;
        int left = 0;
        int right = 0;
        int result = 0;
        int final = 0;

        while(left < fruits.Length && right < fruits.Length)
        {
            result = 0;
            int curr1 = fruits[left];
            int curr2=0;
            right = left;
            while(right < fruits.Length && curr1== fruits[right])
            {
                if(right!=left) result++;
                right++;
            }
            if(right < fruits.Length)curr2 = fruits[right];
            else 
            {
                            left++;
            final = Math.Max(final,result+1);
            continue;
            }
            while(right < fruits.Length && (fruits[right] == curr1 || fruits[right] ==curr2))
            {
                result++;
                right++;
            }
            left++;
            final = Math.Max(final,result+1);
        }
        return final;
    }
}
```
题解
```c#
public class Solution {
    public int TotalFruit(int[] fruits) {
        // 不定长移动窗口
        Dictionary<int, int> dictionary = new Dictionary<int, int>();
        int left = 0, ans = 0;
        for(int right = 0; right < fruits.Length; right++) {
            // 增加水果种类
            dictionary[fruits[right]] = dictionary.GetValueOrDefault(fruits[right], 0) + 1;
            // 判断水果种类
            while(dictionary.Count > 2) {
                dictionary[fruits[left]]--;
                if (dictionary[fruits[left]] == 0) {
                    dictionary.Remove(fruits[left]);
                }
                // 左指针向右移动，缩小窗口
                left++;
            }
            ans = Math.Max(ans, right - left + 1);
        }
        return ans;
    }
}
```
// 用dictionary可以避免用list没法判断left和right中间还有没有这种水果
// key=fruits[index],value=出现的次数
// 当前水果超过两种之后就可以收缩滑动窗口的长度


*** 76
