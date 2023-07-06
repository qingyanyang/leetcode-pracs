# leetcode-pracs
###leetcode problems practices in winter holiday


### **28. Find the Index of the First Occurrence in a String**

> **_Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack._**


**Solution: Python 3**

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        return haystack.find(needle)
```

### **459. Repeated Substring Pattern**

> **_Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together._**


**Solution: Python 3**

```python :
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        sub = ''
        for i in range(1,len(s)):
            sub = s[0:i]
            if ''.join(s.split(sub))=='':
                return True
        return False
```