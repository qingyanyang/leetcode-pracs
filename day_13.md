# leetcode-pracs
###leetcode problems practices in winter holiday


### **144. Binary Tree Preorder Traversal**

> **_Given the root of a binary tree, return the preorder traversal of its nodes' values._**

**Solution: Python 3**

```python recursion
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        lst=[]
        self.preorderTraversalRec(root,lst)
        return lst
    def preorderTraversalRec(self, root: Optional[TreeNode], lst:List[int]):
        if root:
            lst.append(root.val)
            if root.left:
                self.preorderTraversalRec(root.left,lst)
            if root.right:
                self.preorderTraversalRec(root.right,lst)
        else:
            return

```
```python iteration
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        stk=[]
        if root: 
            stk.append(root)
        else: return res

        while stk:
            node = stk.pop()
            res.append(node.val)
            if node.right:
                stk.append(node.right)
            if node.left:
                stk.append(node.left)
        return res
```

### **145. Binary Tree Postorder Traversal**

> **_Given the root of a binary tree, return the postorder traversal of its nodes' values._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        lst=[]
        self.postorderTraversalRec(root,lst)
        return lst
    def postorderTraversalRec(self, root: Optional[TreeNode],lst:List[int]):
        if root:
            if root.left:
                self.postorderTraversalRec(root.left,lst)
            if root.right:
                self.postorderTraversalRec(root.right,lst)
            lst.append(root.val)
        else:
            return
        
```
### **94. Binary Tree Inorder Traversal**

> **_Given the root of a binary tree, return the inorder traversal of its nodes' values._**


**Solution: Python 3**

```python :
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        lst=[]
        self.inorderTraversalRec(root,lst)
        return lst
    def inorderTraversalRec(self, root: Optional[TreeNode],lst:List[int]):
        if root:
            if root.left:
                self.inorderTraversalRec(root.left,lst)
            lst.append(root.val)
            if root.right:
                self.inorderTraversalRec(root.right,lst)
        else:
            return

```