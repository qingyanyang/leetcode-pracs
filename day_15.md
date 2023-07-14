# leetcode-pracs
###leetcode problems practices in winter holiday


### **104. Maximum Depth of Binary Tree**

> **_Given the root of a binary tree, return its maximum depth.
A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node._**

**Solution: Python 3**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root:
            if not root.left and not root.right:
                return 1
            else:
                return max(self.maxDepth(root.left)+1,self.maxDepth(root.right)+1)
        else:
            return 0
```
### **111. Minimum Depth of Binary Tree**

> **_Given a binary tree, find its minimum depth.
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
Note: A leaf is a node with no children._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        
        if root:
            if not root.left and not root.right:
                return 1
            elif not root.left and root.right:
                return self.minDepth(root.right)+1
            elif root.left and not root.right:
                return self.minDepth(root.left)+1
            else:
                return min(self.minDepth(root.left)+1,self.minDepth(root.right)+1)
        else:
            return 0
```
### **559. Maximum Depth of N-ary Tree**

> **_Given a n-ary tree, find its maximum depth.
The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
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
    def maxDepth(self, root: 'Node') -> int:
        if root:
            maxLevel=1
            for child in root.children:
                 maxLevel = max(maxLevel,self.maxDepth(child)+1)
            return maxLevel
        else:
            return 0
```
### **222. Count Complete Tree Nodes**

> **_Given the root of a complete binary tree, return the number of the nodes in the tree.
According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.
Design an algorithm that runs in less than O(n) time complexity._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        res=0
        dqe=deque()
        if not root:return 0
        dqe.append(root)

        while dqe:
            tempDqe=deque()
            count=0
            while dqe:
                node = dqe.popleft()
                count+=1
                if node.left:
                    tempDqe.append(node.left)
                if node.right:
                    tempDqe.append(node.right)
            res+=count
            dqe=tempDqe
        return res

```
```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if root:
            return self.countNodes(root.left)+1+self.countNodes(root.right)
        else:
            return 0

```
```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root: return 0
        left = root.left
        right = root.right
        leftLevel=1
        rightLevel=1
        while left:
            left=left.left
            leftLevel+=1
        while right:
            right=right.right
            rightLevel+=1
        if leftLevel==rightLevel:
            return 2 ** leftLevel -1

        return self.countNodes(root.left)+1+self.countNodes(root.right)

```