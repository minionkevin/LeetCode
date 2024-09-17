# String-合集

|Date\Question|334-E|
|:----:|:----:|
|2024-09-017|Y|


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
