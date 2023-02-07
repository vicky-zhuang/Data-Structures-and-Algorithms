# 链表｜24. 两两交换链表中的节点、19.删除链表的倒数第N个节点、面试题 02.07. 链表相交、142.环形链表II 

## 24. 两两交换链表中的节点
```python
def swapPairs(head):
    if head is None:
        return head
    dummy_head = ListNode('dummy')
    dummy_head.next = head

    pre = dummy_head
    node1 = head
    while node1 and node1.next:
        node2 = node1.next
        tmp = node2.next
        node2.next = node1
        pre.next = node2
        pre = node1
        node1 = tmp
    pre.next = node1
    return dummy_head.next
```

## 19.删除链表的倒数第N个节点
```python
def removeNthFromEnd(head, n):
    dummy_head = ListNode('dummy')
    dummy_head.next = head

    # node1先走几步
    node1 = dummy_head
    i = 0
    while i < n:
        node1 = node1.next
        i += 1

    # node1和node2一直走到，node2到删除节点的前一个节点
    node2 = dummy_head
    while node1.next:
        node1 = node1.next
        node2 = node2.next

    # 删除节点
    node2.next = node2.next.next
    return dummy_head.next
```

## 面试题 02.07. 链表相交
```python
def getIntersectionNode(headA,headB):
    if headA is None or headB is None:
        return None
    nodeA = headA
    nodeB = headB

    while nodeA or nodeB:
        if nodeA is None:
            nodeA = headB
        if nodeB is None:
            nodeB = headA
        if nodeA == nodeB:
            return nodeA
        else:
            nodeA = nodeA.next
            nodeB = nodeB.next
```

## 142.环形链表II
```python
def detectCycle(head):
    fast = head
    slow = head

    while fast and fast.next and fast.next.next:
        fast = fast.next.next
        slow = slow.next
        if fast == slow:
            break
    else:
        return None

    fast = head
    while fast != slow:
        fast = fast.next
        slow = slow.next
    return fast
```