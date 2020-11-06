#### 关键词
动态规划
### 题目描述
小扣出去秋游，途中收集了一些红叶和黄叶，他利用这些叶子初步整理了一份秋叶收藏集 leaves， 字符串 leaves 仅包含小写字符 r 和 y， 其中字符 r 表示一片红叶，字符 y 表示一片黄叶。
出于美观整齐的考虑，小扣想要将收藏集中树叶的排列调整成「红、黄、红」三部分。每部分树叶数量可以不相等，但均需大于等于 1。每次调整操作，小扣可以将一片红叶替换成黄叶或者将一片黄叶替换成红叶。请问小扣最少需要多少次调整操作才能将秋叶收藏集调整完毕。

### 思路
动态规划，使用一个n*3的数组，0储存这片叶子为第一部分红色需要调整的最小此处，1储存这片叶子为第二部分黄叶需要调整的次数，2储存这片叶子为第三部分红叶需要调整的最小次数。

初始条件 第一片叶子一定是红的，第二片叶子一定是黄的。
### 代码
```java
class Solution {
    //动态规划
    public int minimumOperations(String leaves) {
        int n = leaves.length();
        int[][] dp = new int[n][3];
        dp[0][0] = leaves.charAt(0) == 'y' ? 1 : 0;
        dp[0][1] = dp[0][2] = dp[1][2] = Integer.MAX_VALUE;
        for(int i = 1;i < n;i++){
            int isRed = leaves.charAt(i) == 'r' ? 1 : 0;
            int isYellow = leaves.charAt(i) == 'y' ? 1 : 0;
            dp[i][0] = dp[i-1][0] + isYellow;
            dp[i][1] = Math.min(dp[i-1][0],dp[i-1][1])  + isRed;
            if(i > 1){
                dp[i][2] = Math.min(dp[i-1][1],dp[i-1][2]) + isYellow;
            }
        }
        return dp[n-1][2];
    }
}
```
优化空间
```java
class Solution {
    //动态规划
    public int minimumOperations(String leaves) {
        int n = leaves.length();
        int red1,yellow,red2;
        red1 = leaves.charAt(0) == 'y' ? 1 : 0;
        yellow = red2 = Integer.MAX_VALUE;
        for(int i = 1; i < n;i++){
            int isRed = leaves.charAt(i) == 'r' ? 1 : 0;
            int isYellow = leaves.charAt(i) == 'y' ? 1 : 0;
            int currRed1,currYellow,currRed2;
            currRed1 = red1 + isYellow;
            currYellow = Math.min(red1,yellow) + isRed;
            if(i == 1){
                currRed2 = Integer.MAX_VALUE;
            }else{
                currRed2 = Math.min(yellow,red2) + isYellow;
            }
            red1 = currRed1;
            red2 = currRed2;
            yellow = currYellow;
        }
        return red2;
    }
}
```