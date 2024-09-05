# HashTable-数组交集

|Date\Question|349-E|
|:----:|:----:|
|2024-09-03|Y|


## 349 Intersection of Two Arrays
Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

- [X] 2024-09-05: 17:25

```c#
public class Solution {
    public int[] Intersection(int[] nums1, int[] nums2) {
        Dictionary<int,int> dic = new Dictionary<int,int>();
        for(int i = 0; i < nums1.Length; i++)
        {
            if(dic.ContainsKey(nums1[i])) dic[nums1[i]]++;
            else dic.Add(nums1[i],1);
        }

        Dictionary<int,int> dic1 = new Dictionary<int,int>();
        for(int i = 0; i < nums2.Length;i++)
        {
            if(dic1.ContainsKey(nums2[i])) dic1[nums2[i]]++;
            else dic1.Add(nums2[i],1);
        }

        List<int> result = new List<int>();

        foreach(var item in dic)
        {
            if(dic1.ContainsKey(item.Key) && dic1[item.Key] > 0)
            {
                result.Add(item.Key);
                dic1[item.Key]--;
            }
        }

        return result.ToArray();
    }
}
```
