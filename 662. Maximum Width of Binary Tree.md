Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a full binary tree, but some nodes are null.

The width of one level is defined as the length between the end-nodes (the leftmost and right most non-null nodes in the level, where the null nodes between the end-nodes are also counted into the length calculation.

Example 1:
```
Input: 

           1
         /   \
        3     2
       / \     \  
      5   3     9 

Output: 4
Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).
```
Example 2:
```
Input: 

          1
         /  
        3    
       / \       
      5   3     

Output: 2
Explanation: The maximum width existing in the third level with the length 2 (5,3).
```
Example 3:
```
Input: 

          1
         / \
        3   2 
       /        
      5      

Output: 2
Explanation: The maximum width existing in the second level with the length 2 (3,2).
```
Example 4:
```
Input: 

          1
         / \
        3   2
       /     \  
      5       9 
     /         \
    6           7
Output: 8
Explanation:The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        Queue<TreeNode> q=new LinkedList<>();
        Map<TreeNode,Integer> map=new HashMap<>();
        q.offer(root);
        int max=0;
        map.put(root,1);
        while(!q.isEmpty()){
            int size=q.size();
            int start=0;
            int end=0;
            for(int i=0;i<size;i++){
                TreeNode curr=q.poll();
                if(i==0){
                    start=map.get(curr);
                }
                if(i==size-1){
                    end=map.get(curr);
                }
                if(curr.left!=null){
                    map.put(curr.left,2*map.get(curr));
                    q.offer(curr.left);
                }
                if(curr.right!=null){
                    map.put(curr.right,2*map.get(curr)+1);
                    q.offer(curr.right);
                }
                max=Math.max(max,end-start+1);
            }
        }
        return max;
    }
}
```
