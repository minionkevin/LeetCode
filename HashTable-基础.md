# HashTable-基础

|Date\Question|242-E|383-E|49-M|
|:----:|:----:|:----:|:----:|
|2024-09-04\05|Y|Y|X|

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

## 49 Group Anagrams
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
Explanation:
There is no string in strs that can be rearranged to form "bat".
The strings "nat" and "tan" are anagrams as they can be rearranged to form each other.
The strings "ate", "eat", and "tea" are anagrams as they can be rearranged to form each other.

- [ ] 2024-09-05: 11：43

```c#
public class Solution {
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        IDictionary<string, IList<string>> dictionary = new Dictionary<string, IList<string>>();
        foreach (string str in strs) {
            // 将string拆分成char
            char[] array = str.ToCharArray();
            // 按顺序排列
            Array.Sort(array);
            // 返回成string
            string key = new string(array);
            // 添加到结果
            dictionary.TryAdd(key, new List<string>());
            dictionary[key].Add(str);
        }
        return new List<IList<string>>(dictionary.Values);
    }
}
```
