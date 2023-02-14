# 栈和队列｜232.用栈实现队列、225. 用队列实现栈

## 232.用栈实现队列
```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, x):
        self.items.append(x)

    def pop(self):
        return self.items.pop()

    def peek(self):
        return self.items[-1]

    def empty(self):
        return self.items == []


class MyQueue:

    def __init__(self):
        self.stack_in = Stack()
        self.stack_out = Stack()

    def push(self, x: int) -> None:
        self.stack_in.push(x)

    def pop(self) -> int:
        if self.stack_out.empty():  # 如果stack_out不为空那么就把stack_in中的元素全部加入
            while not self.stack_in.empty():
                num = self.stack_in.pop()
                self.stack_out.push(num)
        return self.stack_out.pop()

    def peek(self) -> int:
        if self.stack_out.empty():  # 如果stack_out不为空那么就把stack_in中的元素全部加入
            while not self.stack_in.empty():
                num = self.stack_in.pop()
                self.stack_out.push(num)
        return self.stack_out.peek()

    def empty(self) -> bool:
        return self.stack_in or self.stack_out


if __name__ == '__main__':
    q = MyQueue()
    q.push(1)
    q.push(2)
    print(q.peek())
    print(q.pop())
    q.push(3)
    q.push(4)
    q.push(5)
    print(q.pop())
    print(q.pop())
    print(q.peek())

```

## 225. 用队列实现栈
```python
class Queue:
    def __init__(self) -> None:
        self.items = []

    def push(self, x):
        self.items.append(x)

    def empty(self):
        return self.items == []

    def peek(self):
        if not self.empty():
            return self.items[0]
        else:
            return 'Queue is empty!'

    def pop(self):
        if not self.empty():
            return self.items.pop(0)
        else:
            return 'Queue is empty!'

    def size(self):
        return len(self.items)


class MyStack:
    '''用队列实现栈'''

    def __init__(self):
        self.queue = Queue()

    def push(self, x: int) -> None:
        self.queue.push(x)

    def pop(self) -> int:
        size = self.queue.size()
        for i in range(size-1):
            num = self.queue.pop()
            self.queue.push(num)
        return self.queue.pop()

    def top(self) -> int:
        size = self.queue.size()
        for i in range(size-1):
            num = self.queue.pop()
            self.queue.push(num)
        res = self.queue.peek()
        num = self.queue.pop()
        self.queue.push(num)
        return res

    def empty(self) -> bool:
        return self.queue.empty()


if __name__ == '__main__':
    # q = Queue()
    # q.push(1)
    # q.push(2)
    # print(q.peek())
    # print(q.pop())
    # print(q.size())
    # print(q.empty())
    # print(q.pop())
    # print(q.empty())
    s = MyStack()
    s.push(1)
    s.push(2)
    s.push(3)
    print(s.top())
    print(s.pop())
    print(s.empty())
    s.push(2)
    print(s.pop())

```