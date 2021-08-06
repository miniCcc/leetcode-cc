### 0264. 丑数 II

#### https://leetcode-cn.com/problems/ugly-number-ii/

给你一个整数 `n` ，请你找出并返回第 `n` 个 **丑数** 。

**丑数** 就是只包含质因数 `2`、`3` 和/或 `5` 的正整数。

**示例 1：**

```
输入：n = 10
输出：12
解释：[1, 2, 3, 4, 5, 6, 8, 9, 10, 12] 是由前 10 个丑数组成的序列。
```

**示例 2：**

```
输入：n = 1
输出：1
解释：1 通常被视为丑数。
```

**提示：**

- `1 <= n <= 1690`

---

**Java**

``` java
class Solution {
    public int nthUglyNumber(int n) {
        // 建立一个最小堆
        Queue<Long> pq = new PriorityQueue<>();
        // 用于去重
        Set<Long> set = new HashSet<>();
        int[] temp = {2, 3, 5};
        pq.add(1L);
        int count = 1;
        while(count < n){
            // 每次都取最小的值
            long num = pq.remove();
            count++;
            for(int i = 0; i < 3; i++){
                if(!set.contains(num * temp[i])){
                    set.add(num * temp[i]);
                    pq.add(num * temp[i]);
                }
            }
        }
        long res = pq.peek();
        return (int) res;
    }
}
```

官方题解1（https://leetcode-cn.com/problems/ugly-number-ii/solution/chou-shu-ii-by-leetcode-solution-uoqd/），非动态规划，重点在于用最小堆来做，每次都取的最小值，最后不能直接返回`pq.peek()`，因为前面声明的是`Long`，`Long`可以转换为`long`，但是不可以再自动帮我们转成`int`,所以我手动实现了一下，先转`long`，最后自动拆箱转`int`

动态规划

``` java
class Solution {
    public int nthUglyNumber(int n) {
        int[] dp = new int[n + 1];
        dp[1] = 1;
        int p1 = 1, p2 = 1, p3 = 1;
        for(int i = 2; i < dp.length; i++){
            int num1 = dp[p1] * 2, num2 = dp[p2] * 3, num3 = dp[p3] * 5;
            dp[i] = Math.min(Math.min(num1, num2), num3);
            if(dp[i] == num1) p1++;
            if(dp[i] == num2) p2++;
            if(dp[i] == num3) p3++;
        }
        return dp[n];
    }
}
```

想不到，硬背