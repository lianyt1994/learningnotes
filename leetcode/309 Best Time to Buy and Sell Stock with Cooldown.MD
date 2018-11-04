```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length<2)return 0;
        //buy[i]表示在第i天之前最后一个操作是买，此时的最大收益。
        //sell[i]表示在第i天之前最后一个操作是卖，此时的最大收益。
        int[] sell = new int[prices.length];
        int[] buy = new int[prices.length];
        
        //处理好前几天的情况
        buy[0]=-prices[0];
        buy[1]=Math.max(-prices[1],-prices[0]);
        sell[1]=Math.max(buy[0]+prices[1],0);
        
        for(int i=2;i<prices.length;i++){
            buy[i]=Math.max(sell[i-2]-prices[i],buy[i-1]);
            sell[i]=Math.max(buy[i-1]+prices[i],sell[i-1]);
        }
        return sell[prices.length-1] ;
    }
}
```
