### [56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/)

以数组 `intervals `表示若干个区间的集合，其中单个区间为` intervals[i] = [starti, endi]` 。请你合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间。

**示例 1：**

```
输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
输出：[[1,6],[8,10],[15,18]]
解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```

**示例 2：**

```
输入：intervals = [[1,4],[4,5]]
输出：[[1,5]]
解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。
```

**提示：**

- 1 <= intervals.length <= 104
- intervals[i].length == 2
- 0 <= starti <= endi <= 104

---

**Java**

``` java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> intervalslist = Arrays.asList(intervals);
        List<int[]> newInter = new ArrayList<>(intervalslist);
        newInter.sort((o1, o2) -> o1[0] - o2[0]);

        List<int[]> res = new ArrayList<>();
        for(int i = 0; i < newInter.size(); ){
            // 取的是第二位
            int t = newInter.get(i)[1];
            // 开始寻找
            int j = i + 1;
            // 表示在区间内，可以合并
            while(j < newInter.size() && newInter.get(j)[0] <= t){
                // 同时更新 t
                t = Math.max(t, newInter.get(j)[1]);
                j++;
            }
            // 合并完毕加入结果集
            res.add(new int[]{newInter.get(i)[0], t});
            // 更新 i
            i = j;
        }
        int[][] ans = new int[res.size()][2];
        for(int i = 0; i < res.size(); i++){
            ans[i][0] = res.get(i)[0];
            ans[i][1] = res.get(i)[1];
        }
        return ans;
    } 
}
```

参考：https://leetcode-cn.com/problems/merge-intervals/solution/merge-intervals-by-ikaruga/