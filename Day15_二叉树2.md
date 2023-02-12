# 二叉树｜层序遍历、226.翻转二叉树、101.对称二叉树

层序遍历
- 102二叉树的层序遍历
- 107 二叉树的层次遍历II
- 199.二叉树的右视图
- 637.二叉树的层平均值
- 429.N叉树的层序遍历
- 515.在每个树行中找最大值
- 116.填充每个节点的下一个右侧节点指针

## 层序遍历

### 102二叉树的层序遍历
```python
def levelOrder(root):
    if root is None:
        return []
    res = []
    queue = [root]
    while queue:
        cnt = len(queue)
        layer = []

        for _ in range(cnt): # 层元素遍历
            node = queue.pop(0)
            layer.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        res.append(layer[:])
    return res
```

### 107 二叉树的层次遍历II
```python
def levelOrder(root):
    if root is None:
        return []
    res = []
    queue = [root]
    while queue:
        cnt = len(queue)
        layer = []

        for _ in range(cnt): # 层元素遍历
            node = queue.pop(0)
            layer.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        res.append(layer[:])
    res.reverse()
    return res
```

### 199.二叉树的右视图
```python
def rightSideView(root):
    if root is None:
        return []
    res = []
    queue = [root]

    while queue:
        cnt=len(queue)

        for i in range(cnt):
            node = queue.pop(0)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
            if i == cnt-1:
                res.append(node.val)
    return res
```

### 637.二叉树的层平均值
```python
def averageOfLevels(root):
    if root is None:
        return []
    
    res = []
    queue = [root]
    while queue:
        cnt = len(queue)

        summ = 0
        for _ in range(cnt):
            node = queue.pop(0)
            summ += node.val
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        res.append(summ/cnt)
    return res
```

### 429.N叉树的层序遍历
```python
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children


def levelOrder(root):
    if root is None:
        return []

    res = []
    queue = [root]
    while queue:
        cnt = len(queue)

        layer = []
        for _ in range(cnt):
            node = queue.pop(0)
            layer.append(node.val)
            if node.children:
                queue.extend(node.children)
        res.append(layer[:])
    return res
```

### 515.在每个树行中找最大值
```python
def largestValues(root):
    import math
    if root is None:
        return []

    res = []
    queue = [root]

    while queue:
        cnt = len(queue)

        max_num = -math.inf
        for _ in range(cnt):
            node = queue.pop(0)
            if node.val > max_num:
                max_num = node.val
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        res.append(max_num)
    return res
```

### 116.填充每个节点的下一个右侧节点指针
```python
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next


def connect(root):
    if root is None:
        return None
    
    queue = [root]
    while queue:
        cnt = len(queue) # 层中包含的节点总数

        i = 0 # 处理的节点计数
        before_node = None # 前一个节点（指针1）
        cur_node = None # 当前处理的节点（指针2）
        while i < cnt:
            node = queue.pop(0)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
            
            if cur_node is None and before_node is None: # 第一个节点
                cur_node = node
            elif i!=cnt: # 其中一个节点不为空
                before_node = cur_node
                cur_node = node
                before_node.next = cur_node
            i += 1
    return root
```



## 226 翻转二叉树 
```python
def invertTree(root):
    if root is None:
        return None
    if root.left or root.right:
        root.left, root.right = root.right, root.left
        if root.left:
            invertTree(root.left)
        if root.right:
            invertTree(root.right)
    return root
```

## 101 对称二叉树
```python
def isSymmetric(root):
    return cmp(root.left, root.right)


def cmp(left_root, right_root):
    if left_root is None and right_root is None:  # 两个节点均为空
        return True
    elif left_root is None or right_root is None:  # 两个节点一个为空
        return False
    elif left_root.val == right_root.val:
        return cmp(left_root.left, right_root.right) and cmp(left_root.right, right_root.left)
    else:
        return False
```