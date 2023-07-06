# leetcode-pracs
###leetcode problems practices in winter holiday


### **344. Reverse String**

> **_Write a function that reverses a string. The input string is given as an array of characters s.
You must do this by modifying the input array in-place with O(1) extra memory._**


**Solution: Python 3**

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        a,b=0,len(s)-1
        while a<b:
            c = s[a]
            s[a]=s[b]
            s[b]=c
            a+=1
            b-=1
```

### **541. Reverse String II**

> **_Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.
If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original._**


**Solution: Python 3**

```python :
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        return self.reverseStrRec(list(s),0,k)
         
    def reverseStrRec(self, s: list[str], start: int, k:int) -> str:
        l=len(s)-start
        if l<k:
            return ''.join(s[:start]+s[start:][::-1])
        elif l<2*k and l>=k:
            return ''.join(s[:start]+s[start:start+k][::-1]+s[start+k:])
        else:
            s=s[:start]+s[start:start+k][::-1]+s[start+k:]
            return self.reverseStrRec(s,start+2*k,k)
```
### **剑指 Offer 05. 替换空格**

> **_请实现一个函数，把字符串 s 中的每个空格替换成"%20"。_**


**Solution: Python 3**

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        s = s.replace(' ','%20')
        return s 
```

### **剑指 Offer 58 - II. 左旋转字符串**

> **_字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。_**


**Solution: Python 3**

```python
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        return s[n:]+s[0:n]
```
