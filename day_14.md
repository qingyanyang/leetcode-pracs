# leetcode-pracs
###leetcode problems practices in winter holiday


### **102. Binary Tree Level Order Traversal**

> **_Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level)._**

**Solution: Python 3**

```python recursion
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        dqe = deque()
        res=[]
        if root:
            dqe.append(root)

        while dqe:
            temp =[]
            dqeTemp=deque()
            while dqe:
                node = dqe.popleft()
                temp.append(node.val)
                if node.left:
                    dqeTemp.append(node.left)
                if node.right:
                    dqeTemp.append(node.right)
            res.append(temp)
            dqe=dqeTemp
        return res
        
```

### **107. Binary Tree Level Order Traversal II**

> **_Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root)._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrderBottom(self, root: Optional[TreeNode]) -> List[List[int]]:
        res=[]
        dqe=deque()
        if not root: return []
        dqe.append(root)
        while dqe:
            temp=[]
            dqeTemp=deque()
            while dqe:
                node = dqe.popleft()
                temp.append(node.val)
                if node.left:
                    dqeTemp.append(node.left)
                if node.right:
                    dqeTemp.append(node.right)
            res.append(temp)
            dqe=dqeTemp
        res.reverse()
        return res
        
```
### **199. Binary Tree Right Side View**

> **_Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        dqe=deque()
        if not root: return []
        dqe.append(root)

        while dqe:
            temp=0
            dqeTemp=deque()
            while dqe:
                node = dqe.popleft()
                temp=node.val
                if node.left:
                    dqeTemp.append(node.left)
                if node.right:
                    dqeTemp.append(node.right)
            res.append(temp)
            dqe=dqeTemp
        return res
```
### **637. Average of Levels in Binary Tree**

> **_Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. Answers within 10-5 of the actual answer will be accepted._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def averageOfLevels(self, root: Optional[TreeNode]) -> List[float]:
        res=[]
        dqe=deque()
        if not root: return []
        dqe.append(root)
        while dqe:
            tempDqe=deque()
            sumRow = 0
            count=0
            while dqe:
                node=dqe.popleft()
                sumRow+=node.val
                count+=1
                if node.left:
                    tempDqe.append(node.left)
                if node.right:
                    tempDqe.append(node.right) 
            res.append(sumRow/count)
            dqe=tempDqe
        return res
```
### **429. N-ary Tree Level Order Traversal**

> **_Given an n-ary tree, return the level order traversal of its nodes' values.
Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples)._**


**Solution: Python 3**

```python :
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        res=[]
        dqe=deque()
        if not root: return []
        dqe.append(root)

        while dqe:
            tempdqe=deque()
            temp=[]
            while dqe:
                node = dqe.popleft()
                temp.append(node.val)
                for child in node.children:
                    tempdqe.append(child)
            res.append(temp)   
            dqe=tempdqe
            
        return res

```
### **226. Invert Binary Tree**

> **_Given the root of a binary tree, invert the tree, and return its root._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root: return None
        if not root.left and not root.right: return root
        temp = self.invertTree(root.left)
        root.left=self.invertTree(root.right)
        root.right=temp
        return root

   
```
### **101. Symmetric Tree**

> **_Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center)._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        return self.compare(root.left,root.right)
    def compare(self, left: Optional[TreeNode],right: Optional[TreeNode]) -> bool:
        if left and not right:return False
        if not left and right:return False
        if not left and not right: return True
        if left.val != right.val: return False
        return self.compare(left.left,right.right) and self.compare(left.right,right.left)
        
```
