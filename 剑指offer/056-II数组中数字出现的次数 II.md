### [56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

**示例 1：**

```
输入：nums = [3,4,3,3]
输出：4
```

**示例 2：**

```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

**限制：**

- `1 <= nums.length <= 10000`
- `1 <= nums[i] < 2^31`

---

**Java**

``` java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        // int 是 32 位，统计每一位 1 的个数
        for(int i = 0; i < 32; i++){
            int count = 0;
            for(int j = 0; j < nums.length; j++){
                count += (nums[j] >>> i) & 1;
            }
            // 不是 3 的倍数，那么就代表这位多的这个 1 是属于结果的
            if(count % 3 == 1){
                // 这里用 |= 也是一样的
                res ^= (1 << i);
            }
        }
        return res;
    }
}
```

上面一般想不到，一般还是用 map 来做

``` java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(int n : map.keySet()){
            if(map.get(n) == 1) return n;
        }
        return -1;
    }
}
```



