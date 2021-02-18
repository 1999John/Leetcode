# [K站中转内最便宜的航班](!https://leetcode-cn.com/problems/cheapest-flights-within-k-stops/)

### 解题思路

最短路径，最自然的方法一定是迪杰斯特拉算法，但是这里要求了在K站中转内最便宜的航班，因此，不能用普通的迪杰斯特拉算法，因此我们暂时不用迪杰斯特拉算法，用动态规划。

我们使用两个vector，第一个vector pre[j]表示T-1时刻从src到j的最短距离，第二个vector dp[j] 表示T时刻从src到j的最短距离，那么状态转移方程为
```python
dp[i] = min(dp[i],pre[j]+w for  _,j,w   in  flights)
```



### 代码

```java
class Solution{
    public int findCheapestPrice(int n,int[][] flights,int src,int dst,int K) {
        int[][] dp = new int[2][n];
        int INF = Integer.MAX_VALUE/2;
        Arrays.fill(dp[0],INF);			
        Arrays.fill(dp[1],INF);
        
        dp[0][src] = dp[1][src] = 0;
        
        for(int i=0;i<=K;i++) {
            for(int[] flight:flights) {
                dp[i&1][flight[1]] = Math.min(dp[i&1][flight[1]],dp[~i&1][flight[0]]+flight[2]);
            }
        }
        return dp[K&1][dst]<INF?dp[K&1][dst]:-1;
    }
}
```

