给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。
请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。
注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。


示例 1：
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。

用时：21:05
```c#

public class Solution {
    public void Merge(int[] nums1, int m, int[] nums2, int n) {
            int a = m-1;
            int b = n-1;
            int k = m+n-1;

            // 从nums1尾部添加避免失去nums1中本身有的数据
            // a和b作为指针
            // 对比指针元素下nums1和nums2中的数据加入到nums1尾部
        
            while(a >= 0 && b >=0)
            {
                if(nums1[a] >= nums2[b]) nums1[k--] = nums1[a--];
                else nums1[k--] = nums2[b--];
            }

            // 将剩余多出来的部分直接添加进结果中
            while(a>=0) nums1[k--] = nums1[a--];
            while(b>=0) nums1[k--] = nums2[b--];
        }
    }

