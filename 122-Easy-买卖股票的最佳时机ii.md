链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii
# 题目
给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。
- 1 <= prices.length <= 10^5
- 0 <= prices[i] <= 10^4

示例 1：  
输入: [7,1,5,3,6,4]  
输出: 7  
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。  
随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。

# 解题思路
## 方法一 动态规划
本题要求的其实是卖出时与买入时的最大差值。我们不妨假设f(i)表示以第i天为结尾时卖出股票获得的最大收入（差值），那么最后要求的是：
>f(i) = max{f(i)| 1 <= i <= n};

假定前i-1天中最小价格为min_price，我们可以得到如下关系：
>f(i) = max (f(i-1), price[i] - min_price);  

时间复杂度：O(N)； 空间复杂度：O(1)。

```c++
int maxProfit(vector<int>& prices) {
    int min_price =  prices[0];
    vector<int> dp(prices.size());
    dp[0] = 0;
    for (int i = 1; i < prices.size(); ++i)
    {
        min_price = min(min_price, prices[i]);
        dp[i] = max(dp[i - 1], prices[i] - min_price);
    }
    return dp[prices.size() - 1];
}
```
