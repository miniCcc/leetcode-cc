### 0221. 最大正方形

#### 题目地址：https://leetcode-cn.com/problems/maximal-square/

在一个由 `'0'` 和 `'1'` 组成的二维矩阵内，找到只包含 `'1'` 的最大正方形，并返回其面积。

 **示例 1：**

![img](max1grid.jpg)

```
输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
输出：4
```

**示例 2：**

![img](max2grid.jpg)

```
输入：matrix = [["0","1"],["1","0"]]
输出：1
```

**示例 3：**

```
输入：matrix = [["0"]]
输出：0
```

**提示：**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 300`
- `matrix[i][j]` 为` '0'` 或` '1'`

---

**Java**

``` java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null || matrix.length < 1 || matrix[0].length < 1) return 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] dp = new int[m + 1][n + 1];
        int maxSize = 0;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(matrix[i][j] == '1'){
                    dp[i+1][j+1] = Math.min(dp[i][j], Math.min(dp[i][j+1], dp[i+1][j])) + 1;
                    maxSize = Math.max(maxSize, dp[i+1][j+1]);
                }
            }
        }
        return maxSize * maxSize;
    }
}
```

参考：https://leetcode-cn.com/problems/maximal-square/solution/li-jie-san-zhe-qu-zui-xiao-1-by-lzhlyle/

想不到，直接记，无语