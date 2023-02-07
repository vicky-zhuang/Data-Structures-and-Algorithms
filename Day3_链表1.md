# 链表｜ 203.移除链表元素、707.设计链表、 206.反转链表

## 203.移除链表元素
```python
def removeElements(head,val):
    dummy_head = ListNode('dummy')
    dummy_head.next = head

    pre = dummy_head
    cur = head
    while cur:
        if cur.val == val:
            pre.next = cur.next
            cur = cur.next
        else:
            pre = cur
            cur = cur.next
    return dummy_head.next
```

## 707.设计链表
```python
class Node:
    def __init__(self, val=0, next=None) -> None:
        self.val = val
        self.next = next


class MyLinkedList:

    def __init__(self):
        self.dummy_head = Node('dummy')
        self.length = 0

    def get(self, index: int) -> int:
        '''返回链表上对应索引的数值，如果索引无效返回-1'''
        if index < 0:
            return -1
        i = 0
        cur = self.dummy_head.next
        while i < index and cur:
            cur = cur.next
            i += 1

        if cur is None:
            return -1
        else:
            return cur.val

    def addAtHead(self, val: int) -> None:
        node = Node(val)
        node.next = self.dummy_head.next
        self.dummy_head.next = node
        self.length += 1

    def addAtTail(self, val: int) -> None:
        cur = self.dummy_head
        while cur.next:
            cur = cur.next
        cur.next = Node(val)
        self.length += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index <= 0:
            self.addAtHead(val)
        elif index == self.length:
            self.addAtTail(val)
        elif index > self.length:
            pass
        else:
            # 找到index-1位置上的节点
            i = -1
            cur = self.dummy_head
            while i < index-1 and cur:
                cur = cur.next
                i += 1

            node = Node(val)
            node.next = cur.next
            cur.next = node
            self.length += 1

    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or index >= self.length:
            return

        # 找到index-1位置上的节点
        i = -1
        cur = self.dummy_head
        while i < index-1 and cur:
            cur = cur.next
            i += 1

        cur.next = cur.next.next
        self.length -= 1


if __name__ == '__main__':
    # Your MyLinkedList object will be instantiated and called as such:
    obj = MyLinkedList()
    # param_1 = obj.get(index)

    obj.addAtHead(86)
    obj.addAtIndex(1, 54)
    obj.addAtIndex(1, 14)
    obj.addAtHead(83)
    obj.deleteAtIndex(4)
    obj.addAtIndex(3, 18)
    obj.addAtHead(46)
    obj.addAtTail(3)
    obj.addAtTail(76)
    print(obj.get(5))
```

## 206.反转链表
```python
def reverseList(head):
    left = None
    right = head
    while right:
        tmp = right.next
        right.next = left
        left = right
        right = tmp
    return left
```