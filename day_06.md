# leetcode-pracs
###leetcode problems practices in winter holiday


### **454. 4Sum II**

> **_Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:_**

0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0

**Solution: Python 3**

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        # -1 -1 0 2
        # numsA[a] + numsB[b] == abs(numsC[c] + numsD[d])
        # get combinations from numsA and numsB, traverse numsC, minus ele in numsC see if can find the value in numsD
        #get combinations
        lst1 = {}
        for i in nums1:
            count = i
            for j in nums2:
                count+=j
                lst1[count]=lst1.get(count,0)+1
                count = i
        #traverse nums3
        lst2 = {}
        for k in nums3:
            count = k
            for l in nums4:
                count+=l
                lst2[count]=lst2.get(count,0)+1
                count = k

        res = 0
        for ele in lst1.keys():
            if -ele in lst2:
                res+= lst1[ele]*lst2[-ele]

        return res
```

### **383. Ransom Note**

> **_Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.
Each letter in magazine can only be used once in ransomNote._**


**Solution: Python 3**

```python :
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        if len(ransomNote) > len(magazine): return False
        lst=[0]*26
        for e in magazine:
            lst[ord(e)-ord("a")]+=1
        
        for e in ransomNote:
            lst[ord(e)-ord("a")]-=1
        
        for e in lst:
            if e < 0:
                return False
        return True
```
### **15. 3Sum**

> **_Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.
Notice that the solution set must not contain duplicate triplets._**


**Solution: Python 3**

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # two pointers
        ans=[]
        nums.sort()
        for a in range(len(nums)-2):
            if a>0 and nums[a]==nums[a-1]:
                continue
            b=a+1
            c = len(nums)-1
            while b<c:
                if (nums[a]+nums[b]+nums[c])==0:
                    ans.append([nums[a], nums[b], nums[c]])
                    while b<c and nums[b]==nums[b+1]:b+=1
                    while b<c and nums[c-1]==nums[c]:c-=1
                    b+=1
                    c-=1
                elif (nums[a]+nums[b]+nums[c]) < 0:
                    b+=1
                else:
                    c-=1
        return ans
                    
```
### **18. 4Sum**

> **_Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:
0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order._**


**Solution: Python 3**

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        # convert to 3 sum
        nums.sort()
        ans=[]
        for a in range(len(nums)-3):
            if a > 0 and nums[a]==nums[a-1]:continue
            new_target = target-nums[a]
            for b in range(a+1, len(nums)-2):
                if b > a+1 and nums[b]==nums[b-1]:continue
                c = b+1
                d = len(nums)-1
                while c<d:
                    s = nums[b]+nums[c]+nums[d]
                    if s==new_target:
                        ans.append([nums[a],nums[b],nums[c],nums[d]])
                        while c<d and nums[c+1]==nums[c]:c+=1
                        while c<d and nums[d-1]==nums[d]:d-=1
                        c+=1
                        d-=1
                    elif s>new_target:
                        d-=1
                    else:
                        c+=1
        return ans
```
