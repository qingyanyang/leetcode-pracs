# leetcode-pracs
###leetcode problems practices in winter holiday


### **704. Binary Search**

> **_Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.
You must write an algorithm with O(log n) runtime complexity._**


**Solution: Python 3**

```python
"""algorithm: 
    recursive(a,b,nums,target)
        if(a<=b)
            mid = (b-a)/2
            if(nums[mid]==target)
                return mid
            elif (nums[mid]>target)
                return recursive(a,mid-1,target)
            elif
                return recursive(mid+1,b,target)
     
"""
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        return self.searchRec(nums,target,0,len(nums)-1)
    def searchRec(self, nums: List[int], target: int, a:int, b:int) -> int:
        if a <= b:
            mid = a+(b-a)//2
            if nums[mid]==target:
                return mid
            elif nums[mid]>target:
                return self.searchRec(nums,target,a,mid-1)
            else:
                return self.searchRec(nums,target,mid+1,b)
        else:
            return -1

```

### **35. Search Insert Position**

> **_Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.You must write an algorithm with O(log n) runtime complexity._**


**Solution: Python 3**

```python
# binary search
# rec(nums, target, start, end)
# if start <= end:
#   mid = start+(end-start)//2
#   if nums[mid]==target: return mid
#   if nums[mid]>target: return rec(nums, target, start, mid-1)
#   else: return rec(nums, target, mid+1,end)
# else:
#   return start
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        return self.searchInsertRec(nums,target,0,len(nums)-1)
    def searchInsertRec(self, nums: List[int], target: int, start:int,end:int) -> int:
        if start <= end:
            mid = start + (end-start)//2
            if nums[mid]==target:
                return mid
            elif nums[mid]>target:
                return self.searchInsertRec(nums,target, start, mid-1)
            else:
                return self.searchInsertRec(nums,target, mid+1, end)
        else:
            return start

```
### **34. Find First and Last Position of Element in Sorted Array**

> **_Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.
If target is not found in the array, return [-1, -1].
You must write an algorithm with O(log n) runtime complexity._**


**Solution: Python 3**

```python
# [1,2,3,2,3] false
# [1,2,2,3,4] true
# condition for identifying the start is nums[start]==target&& (start-1>=0&&nums[start-1]!=target)|| start-1==-1-> start found
# condition for identifying the end is nums[end]==target&& (end+1<len(nums)&&nums[end+1]!=target)|| end+1==len(nums)-> start found

class Solution:
    def __init__(self):
        self.start_index = -1
        self.end_index = -1
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        self.searchRangeRec(nums,target, 0, len(nums)-1)
        return [self.start_index,self.end_index]
    def searchRangeRec(self, nums: List[int], target: int, start:int,end:int):
        if start<=end:
            mid=start+(end-start)//2
            # 1. equals to target
            if nums[mid]==target:
                # 2. identify start
                if mid-1 < 0 or nums[mid-1]!=target:
                    self.start_index = mid
                else:
                    self.searchRangeRec(nums,target,start,mid-1)
                # 3. identify end
                if mid+1 == len(nums) or nums[mid+1]!=target:
                    self.end_index = mid
                else:
                    self.searchRangeRec(nums,target,mid+1,end)
            elif nums[mid]>target:
                self.searchRangeRec(nums,target,start,mid-1)
            else:
                self.searchRangeRec(nums,target,mid+1,end)
        else:
            return
```
### **69. Sqrt(x)**

> **_Given a non-negative integer x, return the square root of x rounded down to the nearest integer. The returned integer should be non-negative as well.
You must not use any built-in exponent function or operator.
For example, do not use pow(x, 0.5) in c++ or x ** 0.5 in python._**


**Solution: Python 3**

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        return self.mySqrtRec(0,x,x)
    def mySqrtRec(self, start: int, end: int, target:int)->int:
        med = start + int((end-start)/2)
        if med*med<=target and (med+1)*(med+1)>target:
            return med
        elif med*med<target and (med+1)*(med+1)==target:
            return med+1
        elif med*med<target and (med+1)*(med+1)<target:
            return self.mySqrtRec(med+1,end,target)
        elif med*med>target:
            return self.mySqrtRec(start,med-1,target)

```
### **367. Valid Perfect Square**

> **_Given a positive integer num, return true if num is a perfect square or false otherwise.
A perfect square is an integer that is the square of an integer. In other words, it is the product of some integer with itself.
You must not use any built-in library function, such as sqrt._**


**Solution: Python 3**

```python
class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        if self.isPerfectSquareRec(0,num,num) != -1:
            return True
        else:
            return False
    def isPerfectSquareRec(self, start: int, end: int, target: int) -> int:
        med = start + int((end-start)/2)
        if start <= end:
            if med * med == target:
                return med
            elif med * med > target:
                return self.isPerfectSquareRec(start, med-1, target)
            else:
                return self.isPerfectSquareRec(med+1, end, target)
        else:
            return -1
```
### **844. Backspace String Compare**

> **_Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.
Note that after backspacing an empty text, the text will continue empty._**


**Solution: Python 3**

```python
from collections import deque
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        stack_s = deque()
        stack_t = deque()
        self.remove_helper(s,stack_s)
        self.remove_helper(t,stack_t)
        return stack_s==stack_t

    def remove_helper(self,s:str,stack_s:deque)->deque:
        for e in s:
            if e != '#':
                stack_s.append(e)
            elif stack_s:
                stack_s.pop()
        return stack_s
```
