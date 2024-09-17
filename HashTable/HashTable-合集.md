# HashTable-合集

|Date\Question|202-E|001-E|454-M|383-E|
|:----:|:----:|:----:|:----:|:----:|
|2024-09-09|Y|Y|X|Y|

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
// 如果反过来用value装nums[n],index虽然是唯一的。但是遍历dic的时候没办法用value拿到key也不能直接返回index

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

## 454 4Sum II
Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:
0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0

Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
Output: 1

 - [ ] 2024-09-17: 00:00
![image](https://github.com/user-attachments/assets/ce82f050-325f-45ab-93a8-b0161afc9169)

```c#
public class Solution {
public int FourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
       Dictionary<int, int> dic = new Dictionary<int, int>();
        // 因为是双层循环，会找到每一个两数组之前的和
        foreach(var i in nums1){
            foreach(var j in nums2){
                int sum = i + j;
                if(dic.ContainsKey(sum)){
                    dic[sum]++;
                }else{
                    dic.Add(sum, 1);
                }
                
            }
        }
        int res = 0;
         foreach(var a in nums3){
            foreach(var b in nums4){
                int sum = a+b;
                if(dic.TryGetValue(-sum, out var result)){
                    res += result;
                }
            }
        }
        return res;
    }
}

```

## 383 Ransom Note
Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.
Each letter in magazine can only be used once in ransomNote.

Input: ransomNote = "a", magazine = "b"
Output: false

- [X] 2024-09-17: 05:33
- [X] 2024-09-17: 02:26

 ```c#
public class Solution {
    public bool CanConstruct(string ransomNote, string magazine) {
        Dictionary<char,int> dic = new Dictionary<char,int>();

        for(int i = 0; i < magazine.Length; i++)
        {
            if(dic.ContainsKey(magazine[i]))dic[magazine[i]]++;
            else dic.Add(magazine[i],1);
        }


        for(int j = 0; j < ransomNote.Length;j++)
        {
            if(!dic.ContainsKey(ransomNote[j])) return false;
            else
            {
                dic[ransomNote[j]]--;
                if(dic[ransomNote[j]]<0)return false;
            }
        }
        return true;

    }
}
```

```c#
public class Solution {
    public bool CanConstruct(string ransomNote, string magazine) {
        List<int> list = new List<int>();

        for(int i = 0; i < magazine.Length; i++)
        {
            list.Add(magazine[i] - 'a');
        }


        for(int j = 0; j < ransomNote.Length;j++)
        {
            if(!list.Contains(ransomNote[j]-'a')) return false;
            else list.Remove(ransomNote[j]-'a');
        }
        return true;
    }
}
```

// 因为只有26个因为字母，可以用index来代表字母，数组存的数组代表字母出现的次数
// magazine应该是更长的数组，因为每个字母只能用一次
// 查了magazine之后可以立刻检查ransomNote
``` c#
public class Solution {
    public bool CanConstruct(string ransomNote, string magazine) {
        if(ransomNote.Length > magazine.Length) return false;

        int[] nums = new int[26];
        for(int i = 0; i < magazine.Length;i++)
        {
            nums[magazine[i] - 'a']++;
            if(i<ransomNote.Length) nums[ransomNote[i] - 'a']--;
        }

        foreach(int i in nums)
        {
            if(i<0) return false;
        }
        return true;
    }
}
```
