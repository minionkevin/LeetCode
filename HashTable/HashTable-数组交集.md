# HashTable-数组交集

|Date\Question|349-E|350-E|
|:----:|:----:|:----:|
|2024-09-03|Y|Y|


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
## 350 Intersection of Two Arrays II
Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]

- [X] 2024-09-05: 07:41

```c#
public class Solution {
    public int[] Intersect(int[] nums1, int[] nums2) {
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
                    int max = dic1[item.Key] == dic[item.Key] ? item.Value : Math.Min(dic1[item.Key] , dic[item.Key]);

                    for(int i = 0; i < max;i++)
                    {
                        result.Add(item.Key);
                    }   
                    dic1[item.Key] = 0;
            }
        }

        return result.ToArray();
    }
}
```
题解
// 用一个dictionary装nums1的东西
// 直接遍历nums2找相同，没必要再用另一个dictionary装了来对比
```c#
public class Solution {
    public int[] Intersect(int[] nums1, int[] nums2) {
        Dictionary<int, int> map = new();
        foreach (int num in nums1) {
            if (!map.TryAdd(num, 1)) {
                map[num]++;
            }
        }
        List<int> result = new();
        foreach (int num in nums2) {
            if (map.ContainsKey(num) && map[num]-- > 0) {
                result.Add(num);
            }
        }
        return result.ToArray();
    }
}
```
