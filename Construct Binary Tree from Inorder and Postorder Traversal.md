Given inorder and postorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given
```
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return helper(inorder,postorder,0,inorder.length-1,0,postorder.length-1);  
    }  
    public TreeNode helper(int[] inorder,int[] postorder,int inS,int inE,int pS,int pE){
        if(inS>inE) return null;
        int rootIdx=-1;
        int rootVal=postorder[pE];
        for(int i=0;i<inorder.length;i++){
            if(inorder[i]==rootVal){
                rootIdx=i;
                break;
            }
        }
        int ils = inS;
        int ire = inE;
        int pls = pS;
        int pre = pE-1;
        int ile = rootIdx-1;
        int irs = rootIdx+1;
        int ple = ile-ils+pls;
        int prs = ple+1;
        TreeNode root=new TreeNode(rootVal);
        root.left=helper(inorder,postorder,ils,ile,pls,ple);
        root.right=helper(inorder,postorder,irs,ire,prs,pre);
        return root;
    }
}


```
