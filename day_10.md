# leetcode-pracs
###leetcode problems practices in winter holiday


### **20. Valid Parentheses**

> **_Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:
Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type._**

**Solution: Python 3**

```python
class Solution:
    def isValid(self, s: str) -> bool:
        # use a stack to hold the elements one by one, then, if the next element coresponse to the peek one, stack.pop(),until traverse all elements, see if the stack is empty, if it is empty, then reutrn true, else: false. #special case: the length should be even
        if len(s) % 2 != 0: return False
        stk =[]
        for e in s:
            if len(stk) != 0:
                if e == ')' and stk[-1]=='(':
                    stk.pop()
                elif e == ']' and stk[-1]=='[':
                    stk.pop()
                elif e == '}' and stk[-1]=='{':
                    stk.pop()
                else:
                    stk.append(e)
            else:
                stk.append(e)
        if len(stk)==0: return True
        return False

```

### **150. Evaluate Reverse Polish Notation**

> **_You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.
Evaluate the expression. Return an integer that represents the value of the expression.
Note that:
The valid operators are '+', '-', '*', and '/'.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer._**


**Solution: Python 3**

```python :
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        # stack, push ele into stack, if detect operator symbols, go back two elements and do operation,then pushback the result, until traverse all tokens
        stk = []
        for e in tokens:
            if e == '+':
                #go back two elements
                b = stk.pop()
                a = stk.pop()
                stk.append(a+b) 
            elif e == '-':
                #go back two elements
                b = stk.pop()
                a = stk.pop()
                stk.append(a-b) 
            elif e == '*':
                #go back two elements
                b = stk.pop()
                a = stk.pop()
                stk.append(a*b) 
                
            elif e == '/':
                #go back two elements
                b = stk.pop()
                a = stk.pop()
                stk.append(int(a/b)) 
            else:
                stk.append(int(e))
        return stk[0]
```