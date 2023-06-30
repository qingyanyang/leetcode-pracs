# leetcode-pracs
###leetcode problems practices in winter holiday


### **203. Remove Linked List Elements**

> **_Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head._**


**Solution: Python 3**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        # tranvase
        temp = head
        pre = head

        while temp is not None and temp.val == val:
            pre = temp
            temp=temp.next

        new_head = temp

        while temp != None:
            if temp.val == val:
                pre.next = temp.next
            else: 
                pre = temp

            temp=temp.next
            
        return new_head
```

### **206. Reverse Linked List**

> **_Given the head of a singly linked list, reverse the list, and return the reversed list._**


**Solution: Python 3**

```python method 01:
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        lst=[]
        temp = head
        if temp is None:return None
        while temp.next is not None:
            lst.append(temp.val)
            temp=temp.next
        new_head = temp
        for i in range(len(lst)-1,-1,-1):
            temp.next = ListNode(lst[i],None)
            temp = temp.next
        return new_head

```

```python method 02:
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:return None
        temp = head
        pre = ListNode(temp.val,None)
        while temp.next is not None:
            temp=temp.next
            pre = ListNode(temp.val,pre)
        return pre

```
