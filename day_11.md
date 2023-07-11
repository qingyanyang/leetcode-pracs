# leetcode-pracs
###leetcode problems practices in winter holiday


### **239. Sliding Window Maximum**

> **_You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.
Return the max sliding window._**

**Solution: Python 3**

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if k==1:return nums
        #initailization
        maxlst=[]
        window=nums[0:k]
        #
        maxValue = max(window)
        maxIndex = window.index(maxValue)
        maxlst.append(maxValue)
        #traverse
        for i in range(k,len(nums)):
            # see if the first node is the max 
            if (i-k)!=maxIndex:
                if nums[i]>maxlst[-1]:
                    maxIndex=i
                    maxValue=nums[i]
            else:
                maxValue = max(window[1:])
                maxIndex = i-(k-window[1:].index(maxValue)-1)
                if maxValue < nums[i]:
                    maxValue=nums[i]
                    maxIndex=i

            maxlst.append(maxValue)
            window.pop(0)
            window.append(nums[i])

        return maxlst

        time exceed!!!!!!!!! need to review
```

### **347. Top K Frequent Elements**

> **_Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order._**


**Solution: Python 3**

```python :
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        #collect count of each quniue element
        dic = {}
        for ele in nums:
            dic[ele]=dic.get(ele,0)+1
        #sort
        heap=[]
        for keys, frequency in dic.items():
            
            heapq.heappush(heap,(frequency,keys))
            if len(heap) > k:
                #pop out the smallest pair
                heapq.heappop(heap)

        #get the k most frequent elements
        res=[0]*k
        for i in range(k):
            res[i]=heapq.heappop(heap)[1]
        return res
```