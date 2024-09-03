## 59 Spiral Matrix II
Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]、

- [ ] 2024-09-03: 11：55

```c#
public class Solution {
    public int[][] GenerateMatrix(int n) {
        int[][] result = new int[n][];
        for(int i = 0; i<n;i++) result[i] = new int[n];

        int start =0;
        int end = n-1;
        int tmp =1;

        while(tmp<n*n)
        {
            // 第一行
            for(int i = start; i < end;i++) result[start][i] = tmp++;
            // 最后一列
            for(int i = start; i < end;i++) result[i][end] = tmp++;
            // 最后一行
            for(int i = end; i > start;i--) result[end][i] = tmp++;
            // 第一列
            for(int i = end; i > start;i--) result[i][start] = tmp++;
            start++;
            end--;
        }

        // 如果n是奇数，需要单独赋值
        if(n % 2 == 1) result[n / 2][n / 2] = tmp;
        return result;
    }
}
```
