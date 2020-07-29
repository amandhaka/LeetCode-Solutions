Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
Example:

Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]

```java
/*
In dp[][] array . 
0th column will reperest we either sell the stock or we hold the previous stock
1th column will represent we either buy the current stock or we hold the previous value
*/

class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length<=1){
            return 0;
        }
        int[][] dp=new int[prices.length][2]; //0 column -> WE have stock in our hand or we don't because we sold it today and 1 column-> we have stock in our hand and carry forward that or we buy a new stock.
        dp[0][0]=0;
        dp[0][1]=-prices[0];
        dp[1][0]=Math.max(dp[0][0],dp[0][1]+prices[1]); // I hold it or i sell it today 
        dp[1][1]=Math.max(dp[0][1],dp[0][0]-prices[1]);//i am buying it today so I have to be at cooldown period in i-1 so I look to i-2 
        for(int i=2;i<prices.length;i++){
            dp[i][0]=Math.max(dp[i-1][0],dp[i-1][1]+prices[i]);
            dp[i][1]=Math.max(dp[i-1][1],dp[i-2][0]-prices[i]);
        }
        return dp[prices.length-1][0];
    }
}
/*
   0  1
1  0  -1
2  1  -1
3  2  -1
0  2   1
2  3   1

*/


```
