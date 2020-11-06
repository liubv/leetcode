### 题目描述
Given a positive integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

Example:

Input: 3\
Output:\
[\
    [ 1, 2, 3 ],\
    [ 8, 9, 4 ],\
    [ 7, 6, 5 ]\
]

### 思路
填充的路径为向右->向下->向左->向上->向右，**四种状态**。利用一个二维数组来描述这四个状态，当“碰壁”时，切换到下一个状态。
### 代码
```
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int[][] sta = {{0,1},{1,0},{0,-1},{-1,0}};
        int i = 0,j = 0,p = 0;
        boolean flag = false;//判断第一个填了没
        for(int x = 1;x <= n*n;x++){
            if(!flag){//先填上第一个
                res[0][0] = x;
                flag = true;
                continue;
            }
            int di = sta[p%4][0];
            int dj = sta[p%4][1];//当前前进方向
            // System.out.println(di+","+dj);
            if(i+di==-1||i+di==n||j+dj==-1||j+dj==n||res[i+di][j+dj]>0){//是否碰壁
                p++;//拐弯
            }
            i=i+sta[p%4][0];
            j=j+sta[p%4][1];
            System.out.println(i+","+j);
            res[i][j] = x;
        }
        return res;
    }
}
```
