# String-合集

|Date\Question|334-E|541-E|151-M|28-E|459-E|
|:----:|:----:|:----:|:----:|:----:|:----:|
|2024-09-17/23/30|Y|X|Y|X|X|


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

## Reverse Words in a String
Given an input string s, reverse the order of the words.
A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.
Return a string of the words in reverse order concatenated by a single space.
Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

Input: s = "the sky is blue"
Output: "blue is sky the"

- [X] 2024-09-23 : 5:00

```c#
public class Solution {
    public string ReverseWords(string s) {
        char[] chs = { ' ' };
        string[] tmp = s.Split(chs,options:StringSplitOptions.RemoveEmptyEntries);
        StringBuilder sb = new StringBuilder();

        for(int i = tmp.Length - 1; i >=0 ; i--)
        {
            sb.Append(tmp[i]);
            if(i !=0 )sb.Append(' ');
        }

    return sb.ToString();
    }
}
```

## 28 Find the Index of the First Occurrence in a String
Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.

- [X] 2024-09-23 : 07:21

// KMP ?
// 就算不用kmp也可以省去一个for，用一个while loop中的fast和slow来表示
```c#
public class Solution {
    public int StrStr(string haystack, string needle) {
        if(needle.Length > haystack.Length) return -1;

        for(int i = 0; i < haystack.Length; i++)
        {
            int tmp = i;
            int needlePoint = 0;
            while(needlePoint < needle.Length && tmp < haystack.Length)
            {
                if(needle[needlePoint]==haystack[tmp])
                {
                    if(needlePoint == needle.Length-1) return i;
                    tmp++;
                    needlePoint++;
                }
                else break;
            }
        }
        return -1;
    }
}
```

```c#
public class Solution {
    public int StrStr(string haystack, string needle) {
        int slow = 0, fast =0;
        int needleCount = 0;
        if(needle.Length > haystack.Length) return -1;

        while(fast < haystack.Length && needleCount < needle.Length)
        {
            if(haystack[fast] == needle[needleCount])
            {
                fast++;
                needleCount++;
            }
            else
            {
                slow++;
                fast = slow;
                needleCount = 0;
            }
        }

        return needleCount == needle.Length ? slow : -1;
    }
}
```

## 459 Repeated Substring Pattern
Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.

- [ ] 2024-09-30 : 05:03

![image](https://github.com/user-attachments/assets/8b893568-6304-414c-bbf5-513311d73ab7)
```c#
public class Solution {
    public bool RepeatedSubstringPattern(string s) {
        string t = s + s;

        t = t.Substring(1, t.Length - 2);

        if (t.Contains(s)) {
            return true;
        }
        return false;
    }
}
```
//KMP
```C#
public class Solution {
public bool RepeatedSubstringPattern(string s)
{
    if (s.Length == 0)
        return false;
    int[] next = GetNext(s);
    int len = s.Length;
    if (next[len - 1] != 0 && len % (len - next[len - 1]) == 0) return true;
    return false;
}
public int[] GetNext(string s)
{
    int[] next = Enumerable.Repeat(0, s.Length).ToArray();
    for (int i = 1, j = 0; i < s.Length; i++)
    {
        while (j > 0 && s[i] != s[j])
            j = next[j - 1];
        if (s[i] == s[j])
            j++;
        next[i] = j;
    }
    return next;
}
}
```
