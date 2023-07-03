# leetcode-pracs
###leetcode problems practices in winter holiday


### **242. Valid Anagram**

> **_Given two strings s and t, return true if t is an anagram of s, and false otherwise.
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once._**


**Solution: Python 3**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # array applies to limited elements
        l_s = len(s)
        l_t = len(t)
        if l_s != l_t: return False
        lst = [0]*26
        for index in range(0,l_s):
            lst[ord(s[index])-ord("a")]+=1
            lst[ord(t[index])-ord("a")]-=1
        for ele in lst:
            if ele != 0:
                return False
        return True

```
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # hash table
        # special case
        if len(s) != len(t): return False
        d = {}
        # traverse s to count
        for index in range(0,len(s)):
            d[s[index]]=d.get(s[index],0)+1
            d[t[index]]=d.get(t[index],0)-1
        # traverse t to compare
        for value in d.values():
            if value != 0:
                return False
        return True
```


### **349. Intersection of Two Arrays**

> **_Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order._**


**Solution: Python 3**

```python :
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        ans=set()
        s = set()
        s.update(nums1)
        for e in nums2:
            if e in s:
                ans.add(e)
        return list(ans)
```
### **202. Happy Number**

> **_Write an algorithm to determine if a number n is happy.
A happy number is a number defined by the following process:
Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not._**


**Solution: Python 3**

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        # s = set()
        s = set()
        return self.helper(n,s)

    def helper(self, n:int, s:set())->bool:
        # start recursion 
        # stop condition : n == 1 return true
        if n == 1: return True
        # -1. n in s ? -> return false
        if n in s: return False
        # 0. s.add(n)
        s.add(n)
        # 1. separate the digits
        new_n = 0
        for ele in str(n):
            new_n += int(ele)**2
        # 2. fomula caculation -> recursive call
        return self.helper(new_n,s)
```
### **1142. 1. Two Sum**

> **_Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order._**


**Solution: Python 3**

```python
# class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        d={}
        d_backup={}
        for i in range(len(nums)):
            if d.get(nums[i]) is not None:
                d_backup[nums[i]]=i
            else:
                d[nums[i]]=i
                
        for key in set(nums):
            offset = target - key
            index_0=d.get(key)
            del d[key]
            if d.get(offset) is not None:
                return [index_0,d[offset]]
            elif d_backup.get(offset) is not None:
                return [index_0,d_backup[offset]]
```
