# leetcode-pracs
###leetcode problems practices in winter holiday


### **110. Balanced Binary Tree**

> **_Given a binary tree, determine if it is 
height-balanced._**

**Solution: Python 3**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
    # get height of each branch
        if root:
            if abs(self.getHeight(root.left)-self.getHeight(root.right))>1:
                return False
            else:
                return self.isBalanced(root.left) and self.isBalanced(root.right)
        return True

    def getHeight(self, root:Optional[TreeNode])->int:
        if root:
            return 1+max(self.getHeight(root.left),self.getHeight(root.right))
        else:
            return 0
        
```
### **257. Binary Tree Paths**

> **_Given the root of a binary tree, return all root-to-leaf paths in any order.
A leaf is a node with no children._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        # initialize
        path=[]
        lst = []
        path.append(str(root.val))
        print(path)
        self.binaryTreePathsCollect(lst,path,root)
        return lst
        
    def binaryTreePathsCollect(self, lst: List[str], path: List[str], root: Optional[TreeNode]):
        if not root:
            return
        if not root.left and not root.right:
            lst.append(''.join(path))
            print(lst)
            return
        else:

            if root.left:
                path.append('->'+str(root.left.val))
                self.binaryTreePathsCollect(lst,path,root.left)
                path.pop()
            if root.right:
                path.append('->'+str(root.right.val))
                self.binaryTreePathsCollect(lst,path,root.right)
                path.pop()      
            
```
### **559.404. Sum of Left Leaves**

> **_Given the root of a binary tree, return the sum of all left leaves. A leaf is a node with no children. A left leaf is a leaf that is the left child of another node._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if root:
            if root.left and not root.left.left and not root.left.right:
                return root.left.val+self.sumOfLeftLeaves(root.right)
            else:
                return self.sumOfLeftLeaves(root.left)+self.sumOfLeftLeaves(root.right)
            
        else:
            return 0
```