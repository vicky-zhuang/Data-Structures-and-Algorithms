# 栈和队列｜20. 有效的括号、1047. 删除字符串中的所有相邻重复项、150. 逆波兰表达式求值

## 20. 有效的括号
思路：遍历字符串，向栈中逐个加入字符，如果当前字符可以和栈顶字符匹配，则栈顶元素弹出。最后通过栈是否为空判断是否为有效括号
```python
def isValid(self, s: str) -> bool:
    PAR_DICT = {'(': ")", '[': ']', '{': '}'}
    stack = []
    for astr in s:
        if stack == [] or PAR_DICT.get(stack[-1],' ') != astr:
            stack.append(astr)
        elif PAR_DICT[stack[-1]] == astr:
            stack.pop()
    return stack == []
```

## 1047. 删除字符串中的所有相邻重复项
```python
def removeDuplicates(s):
    '''在字符串上反复执行删除重复项操作'''
    stack = []
    for astr in s:
        if stack == [] or stack[-1] != astr:
            stack.append(astr)
        elif stack[-1] == astr:
            stack.pop()
    return ''.join(stack)
```

## 150. 逆波兰表达式求值
```python
    operators = ['+', '-', '*', '/']
    stack = []
    for t in tokens:
        if t not in operators:
            stack.append(int(t))
        elif t in operators:
            num_tail = stack.pop()
            num_head = stack.pop()
            if t == '+':
                res = num_head+num_tail
            elif t == '-':
                res = num_head-num_tail
            elif t == '*':
                res = num_head*num_tail
            elif t == '/':
                res = num_head/num_tail
                if res>0:
                    res = int(res)
                else:
                    res = -1*int(-res)
            stack.append(res)
    return stack.pop()
```