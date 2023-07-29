# leetcode-pracs
###leetcode problems practices in winter holiday


### **530. Minimum Absolute Difference in BST**

> **_Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree._**

**Solution: Python 3**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        minValue=[10**5]
        pre=[-1]
        self.helperRec(root,minValue,pre)
        return minValue[0]
    def helperRec(self, root: Optional[TreeNode],minValue:List[int],pre:List[int]):
        #inorder
        if root:
            self.helperRec(root.left,minValue,pre)
            if pre[0] != -1:
                temp = abs(root.val - pre[0])
                if temp<minValue[0]:
                    minValue[0]=temp
            pre[0]=root.val
            self.helperRec(root.right,minValue,pre)
        else:
            return

```
### **501. Find Mode in Binary Search Tree**

> **_Given the root of a binary search tree (BST) with duplicates, return all the mode(s) (i.e., the most frequently occurred element) in it.
If the tree has more than one mode, return them in any order.
Assume a BST is defined as follows:
The left subtree of a node contains only nodes with keys less than or equal to the node's key.
The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
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
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        dic={}
        self.helper(root,dic)
        maxCount=-1
        lst=[]
        for key,value in dic.items():
            if value>maxCount:
                maxCount=value
                lst.clear()
                lst.append(key)
            elif value==maxCount:
                lst.append(key)

        return lst

    def helper(self, root: Optional[TreeNode],dic: Dict[int, int]):
        # inorder
        # dic{val:count}
        if root:
            self.helper(root.left,dic)
            dic[root.val]=dic.get(root.val,0)+1
            self.helper(root.right,dic)
        else:
            return

```
