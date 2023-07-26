# leetcode-pracs
###leetcode problems practices in winter holiday


### **513. Find Bottom Left Tree Value**

> **_Given the root of a binary tree, return the leftmost value in the last row of the tree._**

**Solution: Python 3**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        
        dqe=deque()
        dqe.append(root)

        while dqe:
            lst=[]
            tempDqe = deque()
            while dqe:
                node = dqe.popleft()
                lst.append(node.val)
                if node.left:
                    tempDqe.append(node.left)
                if node.right:
                    tempDqe.append(node.right)
            dqe=tempDqe
            if not dqe:
                return lst[0]
        
```
### **112. Path Sum**

> **_Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.
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
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        path=[]
        if not root:
            return False
        path.append(root.val)
        return self.hasPathSumBacktracing(root,targetSum,path)
    
    def hasPathSumBacktracing(self, root: Optional[TreeNode], targetSum: int, path:List[int])-> bool:
        if not root:
            return 
        if not root.left and not root.right:
            print(sum(path),targetSum)
            if sum(path) == targetSum:
                return True
            else: 
                return
        else:
            if root.left:
                path.append(root.left.val)
                if(self.hasPathSumBacktracing(root.left,targetSum,path)): return True
                path.pop()
            if root.right:
                path.append(root.right.val)
                if(self.hasPathSumBacktracing(root.right,targetSum,path)): return True           
                path.pop()        
        return False
```