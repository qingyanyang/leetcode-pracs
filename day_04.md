# leetcode-pracs
###leetcode problems practices in winter holiday


### **24. Swap Nodes in Pairs**

> **_Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)_**


**Solution: Python 3**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None: return None
        pre = ListNode(-1,head)
        temp,new_head = head,pre
        while temp.next is not None:
            mid = temp.next
            pre.next = mid
            temp.next = mid.next
            mid.next = temp
            pre = temp
            temp = temp.next
            if temp is None:break
        return new_head.next
```

### **Remove Nth Node From End of List**

> **_Given the head of a linked list, remove the nth node from the end of the list and return its head._**


**Solution: Python 3**

```python method 01:
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        # record node
        lst = []
        #count the number of linkedlist, when we count, we can record
        temp = head
        while temp is not None:
            lst.append(temp) 
            temp=temp.next
        length = len(lst)
        #calculate the nth index from the front of the list
        index_front = length-n
        #lst[n-1].next=lst[n+1]
        if index_front < 1: return head.next
        lst[index_front-1].next=lst[index_front].next
        return head
```

```python method 02:
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        # two pointers
        # remove: have to get pre 
        # pre: pre->target--n step-->have to have last position
        # last position> easy!
        # edge case
        pre = ListNode(-1,head)
        new_cur = pre
        last_position = head
        # last_position move n steps
        for i in range(n):
            last_position=last_position.next
        # last_position and pre move froward untill last_position is none
        while last_position is not None:
            pre = pre.next
            last_position=last_position.next
        pre.next = pre.next.next
        return new_cur.next
```
### **160. Intersection of Two Linked Lists**

> **_Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null._**


**Solution: Python 3**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        d = {}
        tempA = headA
        i=0
        while tempA is not None:
            d[tempA]=i
            i+=1
            tempA=tempA.next
        tempB=headB
        while tempB is not None:
            if d.get(tempB) is not None:
                return tempB
            tempB = tempB.next
        return None
```
### **1142. Linked List Cycle II**

> **_Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.
Do not modify the linked list._**


**Solution: Python 3**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        s = set()
        while head is not None:
            if head in s:
                return head
            s.add(head)
            head=head.next
        return None

```
