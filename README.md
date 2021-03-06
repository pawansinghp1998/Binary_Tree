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

M2

class Solution {

boolean result = false;

public boolean hasPathSum(TreeNode root, int targetSum) {
    if(root == null) 
    return false;
    helper(root,targetSum,0);
   
    return result;
}

public void helper(TreeNode node,int targetSum,int currentSum){
    if(node == null)
       return ;
    currentSum += node.val;
    if(currentSum == targetSum && node.left == null && node.right == null)
    {
        result = true;
        return ;
    }
    helper(node.left,targetSum,currentSum);
    helper(node.right,targetSum,currentSum);
}
}

Q.3.(129).You are given the root of a binary tree containing digits from 0 to 9 only.

Each root-to-leaf path in the tree represents a number.

For example, the root-to-leaf path 1 -> 2 -> 3 represents the number 123.
Return the total sum of all root-to-leaf numbers. Test cases are generated so that the answer will fit in a 32-bit integer.

A leaf node is a node with no children.

Input: root = [1,2,3]
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.

Input: root = [4,9,0,5,1]
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.

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
    public int sumNumbers(TreeNode root) {
        if(root==null)
            return 0;
     sum(root,0);
        return sum1;
        }
    int sum1=0;
    public void sum(TreeNode root,int sum2)
    {
        if(root==null)
            return;
        if(root.left==null && root.right==null)               //Checking if node is leaf node or not
        {
             sum1=sum1+(sum2*10+root.val);                    //if it is leaf node adding sum of this path to sum1;
        }
        
       sum(root.left,sum2*10+root.val);                   //Searching for all possible path
           sum(root.right,sum2*10+root.val);
       
    }
}

Q.4.(101).Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

Input: root = [1,2,2,3,4,4,3]
Output: true

Input: root = [1,2,2,null,3,null,3]
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
    public boolean isSymmetric(TreeNode root) {
        boolean z=true;
        leftside(root.left);                               //Calling the left portion of tree
        rightside(root.right);                             //Calling right portion of tree
        if(arr1.size()!=arr2.size())
            return false;
        for(int i=0;i<arr1.size();i++)
            if(arr1.get(i)!=arr2.get(i))
            {                                             //Comparing both the arraylist for checking symmetricity 
                z=false;
                break;
            }
        return z;
    }
        ArrayList<Integer> arr1=new ArrayList<Integer>();
        ArrayList<Integer> arr2=new ArrayList<Integer>();
        
        void leftside(TreeNode root)
        {
            if(root==null)
            {
                arr1.add(0);
                return;
            }                                                   //Storing the left side of tree in an arraylist(from left to right)
            arr1.add(root.val);
            leftside(root.left);
            leftside(root.right);
        }
        void rightside(TreeNode root)
        {
            if(root==null)
            {
                arr2.add(0);
                return;                                         //Storing the right side of tree in an arraylist(from right to lefty)
            }
            arr2.add(root.val);
            rightside(root.right);
            rightside(root.left);
        }
    }


Q.5.(108)Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

 Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:

Input: nums = [1,3]
Output: [3,1]
Explanation: [1,3] and [3,1] are both a height-balanced BSTs.

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
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums.length == 0)
            return null;
        TreeNode head = dfs(nums, 0, nums.length - 1);
        return head;
    }
    private TreeNode dfs(int[] nums, int start, int end) {
        if(start > end) 
            return null;
        int middle = start + (end - start) / 2;
        TreeNode root = new TreeNode(nums[middle]);
        root.left = dfs(nums, start, middle - 1);
        root.right = dfs(nums, middle + 1, end);
        return root;
        
    }
}

Q.6.(102).Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]

Input: root = [1]
Output: [[1]]

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> out=new ArrayList<List<Integer>>();
        if (root==null)
            return out;
        Queue<TreeNode> queue=new LinkedList<TreeNode>();
        TreeNode temp=root;
        queue.add(temp);
      
        while(!queue.isEmpty())
        {
            List<Integer> list=new ArrayList<Integer>();
            List<TreeNode> list1=new ArrayList<TreeNode>();
                while(!queue.isEmpty())
            {                                                   //Polling all the nodes of a level
            TreeNode d=queue.poll();
                    list1.add(d);
            list.add(d.val);
            }
            for(TreeNode t:list1)                               //Adding all the children of the polled out nodes of above level
            {
            if(t.left!=null)
                queue.add(t.left);
            if(t.right!=null)
                queue.add(t.right);
            }
            out.add(list);                                     //Adding list that contain node value level wise
        }
      
        return out;
    }
}

Q.7.(107).Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).

Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]

Input: root = [1]
Output: [[1]]

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        
        List<List<Integer>> out=new ArrayList<List<Integer>>();
         List<List<Integer>> out1=new ArrayList<List<Integer>>();
        Stack<List> stack=new Stack<List>();
        if (root==null)
            return out;
        Queue<TreeNode> queue=new LinkedList<TreeNode>();
        TreeNode temp=root;
        queue.add(temp);
      
        while(!queue.isEmpty())
        {
            List<Integer> list=new ArrayList<Integer>();
            List<TreeNode> list1=new ArrayList<TreeNode>();
                while(!queue.isEmpty())
            {                                                  
            TreeNode d=queue.poll();
                    list1.add(d);
            list.add(d.val);
            }
            for(TreeNode t:list1)                             
            {
            if(t.left!=null)
                queue.add(t.left);
            if(t.right!=null)
                queue.add(t.right);
            }
            out.add(list);                                  
        }
      for(List t:out)                                        //reversing the list using stack
          stack.push(t);
        while(!stack.isEmpty())
            out1.add(stack.pop());
        return out1;
    }
}

Q.8.(226).Given the root of a binary tree, invert the tree, and return its root.

Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]

Input: root = [2,1,3]
Output: [2,3,1]

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
    public TreeNode invertTree(TreeNode root) {
        if(root==null )
            return root;
        TreeNode temp1=root.left;
        TreeNode temp2=root.right;
       
        root.left=temp2;                         //Swapping the left and right node of each node begining from root
        root.right=temp1;
        invertTree(root.left);
            invertTree(root.right);
        return root;
        
    }
}

Q.9.Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

Input: p = [1,2,3], q = [1,2,3]
Output: true

Input: p = [1,2], q = [1,null,2]
Output: false

Input: p = [1,2,1], q = [1,1,2]
Output: false

class Solution {
    
    public boolean isSameTree(TreeNode p, TreeNode q) {
  if(p==null && q==null)                                                   //if both root are null
      return true;
        else if(p==null || q==null)                                        //if one node is null but other is not
      return false;
       else if(p.val==q.val)                                               //if node value are equal then check for left and right node recursively
        {
            return (isSameTree(p.left , q.left) && isSameTree(p.right , q.right));
        }
        else
            return false;                                                   //if both have different node value then return false
}
}

Q.10.(113).Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where each path's sum equals targetSum.

A leaf is a node with no children.
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]

Input: root = [1,2,3], targetSum = 5
Output: []

Input: root = [1,2], targetSum = 0
Output: []

class Solution {
     List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
       
        helperPathSum(root, targetSum, new ArrayList<Integer>());
        return result;
    }
    
    private void helperPathSum(TreeNode root, int targetSum, List<Integer> temp) {
        
        if (root == null)                                               //base case
            return;
        
        if (root.left == null && root.right == null) {                  //if it is leaf node
            
    
            if(targetSum - root.val == 0) {                           //If path sum is equal to target value
    
                temp.add(root.val);
                result.add(new ArrayList<Integer>(temp));                  //adding list into result

                temp.remove(temp.size() - 1);                               //removing last added element
            }
            return;                                                    //if it is leaf node but not path,in this case last element is not added so no need of removing
        }
        
        temp.add(root.val);
        helperPathSum(root.left, targetSum - root.val, temp);
        helperPathSum(root.right, targetSum - root.val, temp);
        temp.remove(temp.size() - 1);                                // removing element
        
    }
     }

   Q.11.(98).Given the root of a binary tree, determine if it is a valid binary search tree (BST).A valid BST is defined as follows:The left subtree of 
   a node contains only  nodes with keys less than the node's key.The right subtree of a node contains only nodes with keys greater than 
    the node's key.Both the left and right subtrees must also be binary search trees.
   
   Input: root = [2,1,3]
Output: true
   
   Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
   
   class Solution {
    public boolean isValidBST(TreeNode root) 
    {
        return helper(root,Long.MIN_VALUE,Long.MAX_VALUE);
        
    }
   boolean helper(TreeNode root,long min,long max)
    {
        if (root==null)
            return true;
        if(root.val>min && root.val<max)                         \\checking if it satisfy the condition of BST
            
        {
                   return( helper(root.left,min,root.val) && helper(root.right,root.val,max));
                
        }
       else
       {
           return false;
       }
    }
    
}
                                         
Q.12.(111).Given a binary tree, find its minimum depth.
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
Note: A leaf is a node with no children.
                                         
Input: root = [3,9,20,null,null,15,7]
Output: 2
                                         
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5
         
          class Solution {
    public int minDepth(TreeNode root) {
        if(root==null)
            return 0;
        if(root.left==null && root.right==null)
            return 1;
        if(root.left==null)
            return 1+minDepth(root.right);
         if(root.right==null)
            return 1+minDepth(root.left);
        return Math.min(1+minDepth(root.left),1+minDepth(root.right));
    }
}

                                         
Q.13.(404).Given the root of a binary tree, return the sum of all left leaves.
Input: root = [3,9,20,null,null,15,7]
Output: 24
Explanation: There are two left leaves in the binary tree, with values 9 and 15 respectively.
                                         
Input: root = [1]
Output: 0
                                         
 class Solution {
    int sum;
    
    public int sumOfLeftLeaves(TreeNode root) {
        helper(root);
        
        return sum;
    }
    
    private void helper(TreeNode root) {
        if (root == null) {
            return;
        }
        
        if (root.left != null && root.left.left == null && root.left.right == null) {      //condition to check if it root.left is left leave or not
            sum += root.left.val;
        }
        
        helper(root.left);
        helper(root.right);
    }
}
                                         
Q.14.(116).You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:
      Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.
Initially, all next pointers are set to NULL.
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
                                         
   class Solution {
    public Node connect(Node root) {
        
        if(root==null)
        {
            return root;
        }
        Queue<Node> q = new LinkedList<Node>();
        q.add(root);
        Node prev = null;
        while(q.size()>0)
        {
            int count = q.size();
            for(int i=0;i<count;i++)
            {
                Node curr = q.remove();
                if(i==count-1)
                {
                    curr.next=null;
                }
                else
                {
                    curr.next = q.peek();
                }
                if(curr.left!=null)
                {
                    q.add(curr.left);
                }
                if(curr.right!=null)
                {
                    q.add(curr.right);
                }
            }
        }
        return root;
    
        
    }
}
                                     
Q.15.(236).Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: ???The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).???

 Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
                                     
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
                                     
Input: root = [1,2], p = 1, q = 2
Output: 1
                                     
class Solution {
    int min=Integer.MAX_VALUE;TreeNode minnode;int cmax;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) 
    {
        if(root==null)
            return minnode;
        cmax=0;
    int d= ancestor(root,0,p,q);
        if(d==2)                                                       //checking whther this particular node is ancestor or not
        {
            min=root.val;
            minnode=root;
        }
        lowestCommonAncestor(root.left,p,q);
        lowestCommonAncestor(root.right,p,q);
        return minnode;
    }  
        int ancestor(TreeNode root,int c,TreeNode p,TreeNode q)                //method to check if it is ancestor of two given node or not
        {
            
           if(root==null) 
               return c;
          
           if(root.val==p.val || root.val==q.val)
           {
            c++;
               if(cmax<c)
               cmax=c;
           }
            ancestor(root.left,cmax,p,q);
            ancestor(root.right,cmax,p,q);
            return cmax;
        }
}
   
   Q.16.(257).Given the root of a binary tree, return all root-to-leaf paths in any order.A leaf is a node with no children.
   Input: root = [1,2,3,null,5]
   Output: ["1->2->5","1->3"]
   
   Input: root = [1]
   Output: ["1"]
   class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result=new ArrayList<String>();
       helper(root,new ArrayList<>(),result);
     return result;
    }
        public void helper(TreeNode root, List<TreeNode> path,List<String> result)
        {
           if(root==null)
               return;
            path.add(root);
            if(root.left==null && root.right==null)        //if it is leaf node
            {
                result.add(helper1(path));                 //converting whole path into list format
                 }
            else
            {
            helper(root.left,path,result);                //traversing through the complete tree
            helper(root.right,path,result);
            }
            path.remove(path.size()-1);                  //removing the node if the pointer is going back
        }
    String helper1(List<TreeNode> list1)
    {
        String delim = "->";
        StringBuilder sb = new StringBuilder();
        int i = 0;
        while (i < list1.size() - 1)
        {
            sb.append((list1.get(i)).val);
            sb.append(delim);
            i++;
        }
        sb.append((list1.get(i)).val);
      String res = sb.toString();
        return res;
    }
}
                               
 Q.17.(230).Given the root of a binary search tree, and an integer k, return the kth (1-indexed) smallest element in the tree.
   Input: root = [3,1,4,null,2], k = 1
   Output: 1
                               
  Input: root = [5,3,6,2,4,null,null,1], k = 3
  Output: 3
                               
  class Solution {
   
ArrayList<Integer> arr=new ArrayList<>();
    public int kthSmallest(TreeNode root, int k) {
         helper(root);
             return arr.get(k-1);      //return kthsmallest element fromm arraylist
         }
   public void helper(TreeNode root)
    {
        if(root==null)
            return ;
        helper(root.left);
        arr.add(root.val);    //inorder traversal and storing element of tree in ascending order
        helper(root.right);
     
        }
    }

