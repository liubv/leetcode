#### 关键词
数组，滑动窗口
### 题目描述

<html>
<a href = "https://leetcode-cn.com/problems/grumpy-bookstore-owner/">1052. 爱生气的书店老板</a>
</html>

### 思路
用数组fuckOff[i] = customer[i] * grumpy[i]确定发飙赶走的客人。

然后用滑动窗口统计哪个时间段赶走的客人最多
### 代码
```java
class Solution {
    public int maxSatisfied(int[] customers, int[] grumpy, int X) {
        int[] fuckOff = new int[customers.length];
        int total = 0;
        for(int i = 0; i < fuckOff.length;i++){
            fuckOff[i] = customers[i] * grumpy[i];
            total += customers[i];
        }
        if(X >= customers.length){
            return total;
        }

        int count = 0;
        for(int p : fuckOff){
            count += p;
        }
        int max = 0;
        for(int i = 0; i < X;i++){
            max += fuckOff[i];
        }
        int temp = max;
        for(int i = X;i < fuckOff.length;i++){
            temp = temp + fuckOff[i] - fuckOff[i-X];
            if(temp > max){
                max = temp;
            }
        }
       
        
        count -= max;
        return total - count;
        
    }
}
```