#### 关键词
树，深度优先搜索，dfs
### 题目描述
给定一个无重复值的二叉树，给定一个节点target和一个整数值K，找出所有距离这个节点为K的节点。
### 思路
先用dfs找到从根节点到此节点路径上的节点，并且更新它们的距离。随后再用dfs或bfs把所有节点的值都更新一遍。
### 代码
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //现用dfs找到从根结点到目标节点的一串节点。
    //计算出他们的距离，然后就可以进行dfs
    Deque<Integer> r2TPath = new LinkedList<>(); //root to target path as r2TPath  
    int[] visited = new int[501];  
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        findPath(root,target.val);
        for(int i = 0;i < 501;i++){
            visited[i] = -1;
        }
        int distance = 0;
        while(!r2TPath.isEmpty()){
            visited[r2TPath.pop()] = distance++;
        }
        dfs(root);
        List<Integer> result = new ArrayList<>();
        for(int i = 0; i < 501;i++){
            if(visited[i] == K){
                result.add(i);
            }
        }
        return result;
    }
    public void findPath(TreeNode root,int target){
        if(root == null){
            return;
        }
        if(!r2TPath.isEmpty()){
            int top1 = r2TPath.pop();
            r2TPath.push(top1);
            if(top1 == target){
                return;
            }
        }
        r2TPath.push(root.val);
        if(root.val == target){
            return;
        }
        findPath(root.right,target);
        findPath(root.left,target);
        if(!r2TPath.isEmpty()){
            int top2 = r2TPath.pop();
            if(top2 == target){
                r2TPath.push(top2);
            }
        }
        
    }
    public void dfs(TreeNode root){
        if(root == null){
            return;
        }
        boolean left = root.left != null? true:false;
        boolean right = root.right != null? true:false;
        if(left && visited[root.left.val] == -1){
            visited[root.left.val] = visited[root.val] + 1;
        }
        if(right && visited[root.right.val] == -1){
            visited[root.right.val] = visited[root.val] + 1;
        }
        if(left){
            dfs(root.left);
        }
        if(right){
            dfs(root.right);
        }
    }
}
```