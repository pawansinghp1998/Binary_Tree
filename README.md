Q.1.(199).Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]

Input: root = [1,null,3]
Output: [1,3]

Input: root = []
Output: []

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
   
    public List<Integer> rightSideView(TreeNode root)
    {
        return rightview(root,1);
    }
        
     List<Integer> list=new ArrayList<Integer>(); int maxlevel=0;
    
       public List<Integer> rightview(TreeNode node, int level)
       {
        if(node==null)
            return list;
         if(maxlevel<level)
         {
             list.add(node.val);
             maxlevel=level;
         }
        rightview(node.right,level+1);
        rightview(node.left,level+1);
        
        return list;
    }
}

Q.2.(112).Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.

A leaf is a node with no children.

Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
Output: true

Input: root = [1,2,3], targetSum = 5
Output: false

Input: root = [1,2], targetSum = 0
Output: false

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

    public boolean hasPathSum(TreeNode root, int targetSum) {
      
        if(root==null)
            return false;
         if(targetSum==root.val && root.left==null && root.right==null)  //Checking if this node is last node and sum of this path is equal to targetsum
            return true;
        
     
          return  (hasPathSum(root.left,(targetSum-root.val))  ||  hasPathSum(root.right,(targetSum-root.val)));  //Choosing eiter direction
    }
}
