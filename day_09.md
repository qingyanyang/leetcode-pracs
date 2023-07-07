# leetcode-pracs
###leetcode problems practices in winter holiday


### **232. Implement Queue using Stacks**

> **_Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).
Implement the MyQueue class:
void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.
Notes:
You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations._**


**Solution: Python 3**

```python
class MyQueue:

    def __init__(self):
        self.in_stk=[]
        self.out_stk=[]

    def push(self, x: int) -> None:
        self.in_stk.append(x)

    def pop(self) -> int:
        self.peek()
        if self.out_stk:
            return self.out_stk.pop()

    def peek(self) -> int:
        if not self.out_stk:
            while self.in_stk:
                self.out_stk.append(self.in_stk.pop())
        return self.out_stk[-1]

    def empty(self) -> bool:
        # both in and out are empty
        return not self.out_stk and not self.in_stk


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```

### **225. Implement Stack using Queues**

> **_Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).
Implement the MyStack class:
void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.
Notes:
You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.
Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations._**


**Solution: Python 3**

```python :
class MyStack:

    def __init__(self):
        self.main_lst=[]
        self.temp_lst=[]

    def push(self, x: int) -> None:
        if not self.main_lst and self.temp_lst:
            self.temp_lst.append(x)
        else:
            self.main_lst.append(x)
       

    def pop(self) -> int:
        node = None
        if not self.main_lst and self.temp_lst:
            while len(self.temp_lst)>1:
                self.main_lst.append(self.temp_lst.pop(0))
            node = self.temp_lst.pop(0)

        elif not self.temp_lst and self.main_lst:
            while len(self.main_lst)>1:
                self.temp_lst.append(self.main_lst.pop(0))
            node = self.main_lst.pop(0)

        return node

    def top(self) -> int:
        node = self.pop()
        self.push(node)
        return node
    
    def empty(self) -> bool:
        return not self.temp_lst and not self.main_lst


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```