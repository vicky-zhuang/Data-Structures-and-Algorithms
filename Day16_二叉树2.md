# 二叉树｜层序遍历、226.翻转二叉树、101.对称二叉树

## 104 二叉树的最大深度
```python
def maxDepth(root):
    '''层序遍历'''
    if root is None:
        return 0

    queue = [root]
    depth = 0
    while queue:
        cnt = len(queue)

        for _ in range(cnt):
            node = queue.pop(0)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        depth += 1
    return depth
```

## 559 n叉树的最大深度
```python
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children


def maxDepth(root):
    if root is None:
        return 0

    depth = 0
    queue = [root]
    while queue:
        cnt = len(queue)
        depth += 1
        for _ in range(cnt):
            node = queue.pop(0)
            if node.children:
                queue.extend(node.children)
    return depth
```

## 111 二叉树的最小深度
```python
def minDepth1(root):
    '''层序遍历'''
    if root is None:
        return 0
    
    depth = 0
    queue = [root]
    while queue:
        cnt = len(queue)
        depth += 1
        for _ in range(cnt):
            node = queue.pop(0)
            if node.left is None and node.right is None:
                return depth
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
```

## 222 完全二叉树的节点个数
```python
    if root is None:
        return 0
    
    queue = [root]
    node_num = 0
    while queue:
        cnt = len(queue)

        for _ in range(cnt):
            node = queue.pop(0)
            node_num += 1
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    return node_num
```
