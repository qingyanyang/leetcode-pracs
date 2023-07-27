# leetcode-pracs
###leetcode problems practices in winter holiday


### **654. Maximum Binary Tree**

> **_You are given an integer array nums with no duplicates. A maximum binary tree can be built recursively from nums using the following algorithm:
Create a root node whose value is the maximum value in nums.
Recursively build the left subtree on the subarray prefix to the left of the maximum value.
Recursively build the right subtree on the subarray suffix to the right of the maximum value.
Return the maximum binary tree built from nums._**

**Solution: Python 3**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        maxIndex = nums.index(max(nums))
        root = TreeNode(nums[maxIndex])
        self.constructMaximumBinaryTreeRec(maxIndex,0,len(nums),nums,root)
        return root
    
    def constructMaximumBinaryTreeRec(self,maxIndex:int,start:int, end:int, nums: List[int],root:TreeNode) -> Optional[TreeNode]:
         
        if maxIndex==start:
            root.left=None
        else :
            maxIndexLeft=nums.index(max(nums[start:maxIndex]))
            root.left = TreeNode(nums[maxIndexLeft])
            self.constructMaximumBinaryTreeRec(maxIndexLeft,start,maxIndex,nums,root.left)
        if maxIndex==end-1:
            root.right=None
        else:
            maxIndexRight=nums.index(max(nums[maxIndex+1:end]))
            root.right = TreeNode(nums[maxIndexRight])
            self.constructMaximumBinaryTreeRec(maxIndexRight,maxIndex+1,end,nums,root.right)
        return
```
### **617. Merge Two Binary Trees**

> **_You are given two binary trees root1 and root2.
Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.
Return the merged tree.
Note: The merging process must start from the root nodes of both trees_**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        root3 = None
        if root1 and root2:
            root3 = TreeNode(root1.val+root2.val)
            root3.left=self.mergeTrees(root1.left,root2.left)
            root3.right=self.mergeTrees(root1.right,root2.right)
        if root1 and not root2:
            root3 = root1

        if root2 and not root1:
            root3 = root2

        return root3
```
### **98. Validate Binary Search Tree**

> **_Given the root of a binary tree, determine if it is a valid binary search tree (BST).
A valid BST is defined as follows:
The left 
subtree
 of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        lst=[-2**31-1,1]
        self.isValidBSTRec(root,lst)

        if lst[1]==0: return False

        return True
    def isValidBSTRec(self, root: Optional[TreeNode],lst:[int]):
        if root:
            self.isValidBSTRec(root.left,lst)
            if root.val>lst[0]: 
                lst[0] = root.val
            else: 
                lst[1]=0
                return
            self.isValidBSTRec(root.right,lst)
        else:
            return
    
```
### **700. Search in a Binary Search Tree**

> **_You are given the root of a binary search tree (BST) and an integer val.
Find the node in the BST that the node's value equals val and return the subtree rooted with that node. If such a node does not exist, return null._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        if root:
            if root.val==val:
                return root

            nodeRight = self.searchBST(root.right,val)
            nodeLeft = self.searchBST(root.left,val)

            if nodeRight: return nodeRight
            if nodeLeft: return nodeLeft
            
            return None
            
        else:
            return None
```