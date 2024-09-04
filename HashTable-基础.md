# HashTable-基础

|Date\Question|242-E|383-E|
|:----:|:----:|:----:|
|2024-09-04|Y| |

## 242 Valid Anagram
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

Example 1:
Input: s = "anagram", t = "nagaram"
Output: true

- [X] 2024-09-04: 3:53

```c#
public class Solution {
    public bool IsAnagram(string s, string t) {
        Dictionary<char,int> dic = new Dictionary<char,int>();

        for(int i = 0; i < s.Length;i++)
        {
            if(dic.ContainsKey(s[i]))dic[s[i]]++;
            else dic.Add(s[i],1);
        }

        for(int i = 0 ; i < t.Length;i++)
        {
            if(dic.ContainsKey(t[i]))
            {
                if(dic[t[i]]-1>0) dic[t[i]]--;
                else dic.Remove(t[i]);
            }
            else return false;
        }
        return dic.Count == 0;
    }
}
```
题解
// 通用统计，不一定非要统计每个字母
```C#
public class Solution {
    public bool IsAnagram(string s, string t) {
        int sl = s.Length, tl = t.Length;
        if(sl!=tl) return false;

        int[] a = new int[26];
        for(int i = 0; i < sl; i++)
        {
            a[s[i]- 'a']++;
            a[t[i]- 'a']--;
        }

        foreach(int i in a )
        {
            if(i!=0) return false;
        }
        return true;
    }
}
```

## 383 Ransom Note
Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.
Each letter in magazine can only be used once in ransomNote.

Input: ransomNote = "a", magazine = "b"
Output: false

- [X] 2024-09-04: 07:23

```c#
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
