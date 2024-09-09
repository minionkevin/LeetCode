# HashTable-合集

|Date\Question|202-E|001-E|
|:----:|:----:|:----:|
|2024-09-09|Y|Y|

## 202 Happy Number
Write an algorithm to determine if a number n is happy.
A happy number is a number defined by the following process:
Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not.

Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

- [X] 2024-09-09: 13:25

```c#
public class Solution {
    public bool IsHappy(int n) {
        List<int> tmpList = new List<int>();
        int curr =0;
        while(curr!=1)
        {
            curr = Convert(n);
            n = curr;
            if(tmpList.Contains(curr)) return false;
            tmpList.Add(curr);
        }
        return true;
    }

    private int Convert(int num)
    {
        int result = 0;
        while(num>=10)
        {
            int n = num%10;
            num /= 10;
            result += n*n;
        }
        result += num*num;
        return result;
    }
}
```

题解
// hashset O(1), list O(n)
```c#
public class Solution {
    private int getSum(int n) {
        int sum = 0;
        //每位数的换算
        while (n > 0) {
            sum += (n % 10) * (n % 10);
            n /= 10;
        }
        return sum;
    }
    public bool IsHappy(int n) {
        HashSet <int> set = new HashSet<int>();
        while(n != 1 && !set.Contains(n)) { //判断避免循环
            set.Add(n);
            n = getSum(n);
        }
        return n == 1;
    }
}
```

## 1 Two Sum
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

- [X] 2024-09-09: 02:42

```c#
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        for(int i = 0; i < nums.Length;i++)
        {
            for(int j = i+1; j < nums.Length;j++)
            {
                if(nums[i] + nums[j] == target)
                {
                    return new int[]{i,j};
                }
            }
        }

        return new int[]{-1};

    }
}
```
// 这里用的是key装nums[n],value装index
// 不用担心重复是因为先检查答案后存入
// 什么时候用哈希表,当我们需要查询一个元素是否出现过，或者一个元素是否在集合里的时候

题解
```c#
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        Dictionary<int ,int> dic= new Dictionary<int,int>();
        for(int i=0;i<nums.Length;i++){
            
            // 计算要找的另一半
            int imp= target-nums[i];

            // 如果另一半已经存在dic而且不是本身
            // 直接返回答案
            if(dic.ContainsKey(imp)&&dic[imp]!=i){
               return new int[]{i, dic[imp]};
            }

            // 存新的元素
            // 如果这个已经存在不再添加
            // 假设index0,value4和1,4,如果target是8上一步应该已经return了,所以不用存
            if(!dic.ContainsKey(nums[i])){
                dic.Add(nums[i],i);
            }
        }
        return new int[]{0, 0};
    }
}
```
