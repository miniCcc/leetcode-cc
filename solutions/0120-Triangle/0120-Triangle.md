### 0120. 三角形最小路径和

#### 题目地址：https://leetcode-cn.com/problems/triangle/

给定一个三角形 `triangle `，找出自顶向下的最小路径和。

每一步只能移动到下一行中相邻的结点上。**相邻的结点** 在这里指的是 **下标** 与 **上一层结点下标** 相同或者等于 **上一层结点下标 + 1** 的两个结点。也就是说，如果正位于当前行的下标` i` ，那么下一步可以移动到下一行的下标 `i `或 `i + 1 `。

**示例 1：**

```
输入：triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
输出：11
解释：如下面简图所示：
   2
  3 4
 6 5 7
4 1 8 3
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。
```

**示例 2：**

```
输入：triangle = [[-10]]
输出：-10
```

**提示：**

- `1 <= triangle.length <= 200`
- `triangle[0].length == 1`
- `triangle[i].length == triangle[i - 1].length + 1`
- `-104 <= triangle[i][j] <= 104`

**进阶：**

- 你可以只使用 `O(n)` 的额外空间（`n` 为三角形的总行数）来解决这个问题吗？

---

**Java**

``` java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int[] dp = new int[triangle.size()];
        dp[0] = triangle.get(0).get(0);
        int [] pre = new int[dp.length];
        pre[0] = dp[0];
        boolean flage = false;
        for(List<Integer> list : triangle){
            if(!flage){
                flage = true;
                continue;
            }
            int index = 0;
            while(index < list.size() && flage){
                int num = list.get(index);
                if(index == 0) dp[index] = num + pre[0];
                else if(index == list.size() - 1) dp[index] = num + pre[index - 1];
                else dp[index] = Math.min(num + pre[index], num + pre[index - 1]);
                index++;
            }
            for(int i = 0; i < dp.length; i++){
                pre[i] = dp[i];
            }
        }
        int min = dp[0];
        for(int i = 1; i < dp.length; i++){
            if(dp[i] < min) min = dp[i];
        }
        return min;
    }
}
```

我的方法是从上到下，而下面这个解法是从下到上：

``` java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        // dp[i][j] 表示从点 (i, j) 到底边的最小路径和。
        int[][] dp = new int[n + 1][n + 1];
        // 从三角形的最后一行开始递推。
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j <= i; j++) {
                dp[i][j] = Math.min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle.get(i).get(j);
            }
        }
        return dp[0][0];
    }
}
```

参考链接：https://leetcode-cn.com/problems/triangle/solution/di-gui-ji-yi-hua-dp-bi-xu-miao-dong-by-sweetiee/