# String-合集

|Date\Question|334-E|541-E|
|:----:|:----:|:----:|
|2024-09-17/23|Y|X|


## 344 Reverse String
Write a function that reverses a string. The input string is given as an array of characters s.
You must do this by modifying the input array in-place with O(1) extra memory.

Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]

- [X] 2024-09-17 : 05:47

```c#
public class Solution {
    public void ReverseString(char[] s) {

        for(int i =0; i < s.Length/2;i++)
        {
            char tmp = s[i];
            s[i] = s[s.Length-1-i];
            s[s.Length-1-i] = tmp;
        }
    }
}
```

## 541 Reverse String II
Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.
If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Input: s = "abcdefg", k = 2
Output: "bacdfeg"

- [ ] 2024-09-23 : 09:29

// 没仔细读题，计数为2k，反转前k个，不到k个就翻转所有
```c#
public class Solution {
    public string ReverseStr(string s, int k) {
        char[] ch = s.ToCharArray();
        for(int i = 0; i < ch.Length; i += 2*k)
        {
            int start = i;
            int end = Math.Min(ch.Length-1,start +k -1);

            while(start<end)
            {
                char tmp = ch[start];
                ch[start] = ch[end];
                ch[end] = tmp;

                start++;
                end--;
            }
        }
        return new string(ch);
    }
}
```
