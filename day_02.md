# leetcode-pracs
###leetcode problems practices in winter holiday


### **977. Squares of a Sorted Array**

> **_Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order._**


**Solution: Python 3**

```python
# nums=[-5,-1,-1,2,4,4,5]
# nums=[-5,-4,-2]
# nums_temp = [1,1,4,16,16,25,25]
# two-pointers
# a->left b->right
# while(a<b)
# if abs(nums[a])>abs(nums[b])
# nums_sorted.insert(len(nums_sorted),nums[a]**2)
# a+1
# else
# nums_sorted.insert(len(nums_sorted),nums[b]**2)
# b-1
# O(n)
# O(n)
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        # two-pointers
        # a->left b->right  
        a,b=0,len(nums)-1
        nums_sorted=[0]*len(nums)
        index = b
        while a<=b:
            if abs(nums[a]) < abs(nums[b]):
                nums_sorted[index]=nums[b]**2
                b-=1
            else:
                nums_sorted[index]=nums[a]**2
                a+=1
            index-=1
        return nums_sorted 
        
```

### **209. Minimum Size Subarray Sum**

> **_Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead._**


**Solution: Python 3**

```python
# slide window
# two pointers
# a-> start b->end  of window
# loop until a->end index+1
# get min window size
# a+1 (check sum>=target)ifnot->b++
# time: O(n)
# space: O(1)

class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:

        a,b = 0,0
        l=len(nums)
        count = 0
        # set a max value which real length could not be
        lw_min = l+1
        # stop when a out of range: but some improvement to be more efficient, when b reached the last element, and count < target, now just get out of the loop
        while a < l:
            # ++right until meet constraint
            while b<l and count < target:
                count+=nums[b]
                b+=1
            # if out of range and could not meet constraint -> break
            if b==l and count < target: break
            # else: get min value of len evey iteration
            lw_min = min(lw_min,b-a)
            # --left
            count-=nums[a]
            a+=1
        # if lw_min is unchange, which means no such subarray
        return lw_min if lw_min != (l+1) else 0
            
```
### **59. Spiral Matrix II**

> **_Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order._**


**Solution: Python 3**

```python
# 1   2   3   4
# 12  13  14  5 
# 11  16  15  6
# 10  9   8   7  
# [0][0]..[0][3]->[1][3],[2][3],[3][3]-> [3][2],[3][1],[3][0]->[2][0],[1][0]->[1][1],[1][2]
# initialize 2d list with 1
# for range (1,n*n+1):
#   for 
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        #4 different loops
        #n-> n-1->n-1->n-2
        #stop condition: loptimes reached
        
        lst_2d = [[0]*n for _ in range(n)]

        loop_times = math.ceil(n/2)
        value = 1
        i,j,k=0,0,0
        while loop_times>0:
            k+=1
            #01
            while j<n and lst_2d[i][j]==0:
                lst_2d[i][j]=value
                j+=1
                value+=1
            #02
            
            j-=1
            i+=1
            while i<n and lst_2d[i][j]==0:
                lst_2d[i][j]=value
                i+=1
                value+=1
            #03
            i-=1
            j-=1
            while j>=0 and lst_2d[i][j]==0:
                lst_2d[i][j]=value
                j-=1
                value+=1
            #04
            i-=1
            j+=1
            while i>=0 and lst_2d[i][j]==0:
                lst_2d[i][j]=value
                i-=1
                value+=1
            
            loop_times-=1
            i=k
            j=k
        return lst_2d
            
```