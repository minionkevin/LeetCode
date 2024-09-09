# HashTable-合集

|Date\Question|202-E|001-E|
|:----:|:----:|:----:|
|2024-09-09|Y| |

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

- [ ] 2024-09-09:
