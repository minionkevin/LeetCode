# 数组-螺旋矩阵

|Date\Question|59-M|54-M|
|:----:|:----:|
|2024-09-03|X|X|

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

## 54 Spiral Matrix
Given an m x n matrix, return all elements of the matrix in spiral order.

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]

- [ ] 2024-09-03: 15:40

```c#
public class Solution {
    public IList<int> SpiralOrder(int[][] matrix) {
        List<int> ans = new List<int>();
        int start = 0;
        int rows = matrix.Length;
        int columns = matrix[0].Length;
        int loop = Math.Min(rows,columns)/2;
        int mid = loop;
        int offSet = 1;
        int i,j;

        while(loop-->0)
        {
            i=j=start;
            
            //从左往右
            for(; j < columns - offSet; j++)
                ans.Add(matrix[i][j]);

            //从上往下
            for(; i < rows - offSet; i++)
                ans.Add(matrix[i][j]);

            //从右往左
            for(; j > start; j--)
                ans.Add(matrix[i][j]);
            
            //从下往上
            for(; i > start; i--)
                ans.Add(matrix[i][j]);

            //每循环一次 改变起点位置
            start++;
            //终止条件改变
            offSet++;
        }

        //如果行和列中的最小值是奇数 则会产生中间行或者中间列没有遍历
        if(Math.Min(rows,columns) % 2 != 0) {
            //行大于列则产生中间列
            if(rows > columns) {
                //中间列的行的最大下标的下一位的下标为mid + rows - columns + 1
                for(int k = mid; k < mid + rows - columns + 1; k++) {
                    ans.Add(matrix[k][mid]);
                }
            }else {//列大于等于行则产生中间行
                //中间行的列的最大下标的下一位的下标为mid + columns - rows + 1
                for(int k = mid; k < mid + columns - rows + 1; k++) {
                    ans.Add(matrix[mid][k]);
                }
            }
        }

        return ans;
    }
}
```
