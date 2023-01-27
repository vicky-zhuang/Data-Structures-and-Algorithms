# 代码随想录算法训练营 第三天|203.移除链表元素、707.设计链表、 206.反转链表

## 链表节点定义、常用构建和展示链表的操作

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


def build_linkedlist(alist):
    '''依照列表中的元素构建一个链表'''
    length = len(alist)
    rear = ListNode(alist[length-1])
    for i in range(length-2, -1, -1):
        head = ListNode(alist[i])
        head.next = rear
        rear = head
    return head


def show_linkedlist(head):
    '''展示链表中的数据'''
    current_node = head
    res = ''
    while current_node:
        res += str(current_node.val)+' '
        current_node = current_node.next
    return res.strip()
```



## 203 移除链表元素

### [题目描述](https://leetcode.cn/problems/remove-linked-list-elements/)

### 思路

链表中删除头节点和非头节点的实现方式是不同的，为了简化操作，设置虚拟头节点。

设定一个活动指针`cur`指向处理节点的前一个节点（方面对处理节点进行删除），如果`cur.next=val`,就删除`cur.next`这个节点，`cur`指向`cur.next.next`。然后再对`cur.next`这个节点进行判断。

### 代码

```python
def removeElements1(head, val):
    '''移除链表中值为val的节点'''
    dummy_head = ListNode('')  # 新建一个虚拟头节点
    dummy_head.next = head

    # 设定两个指针，node2寻找满足条件的节点,node1指向节点连接的位置
    node1 = dummy_head
    node2 = head

    while node2:
        # 节点等于val,node2后移
        while node2 and node2.val == val:
            node2 = node2.next

        # 节点不等于val,将该节点连到node1,node1,node2均后移一位
        if node2 and node2.val != val:
            node1.next = node2
            node1 = node2
            node2 = node2.next
    node1.next = None  # 最后处理链表的尾节点
    return dummy_head.next

  
  def removeElements2(head, val):
    '''不使用虚拟头节点,对于不满足条件的节点逐个删除'''
    while head and head.val == val: # 找到第一个不等于val的节点作为头节点
        head = head.next
    
    cur = head
    while cur and cur.next:
        if cur.next.val == val:
            cur.next = cur.next.next # 删除cur.next节点
        else:
            cur = cur.next # 移动cur到下一个节点
    return head


def removeElements3(head, val):
    '''使用虚拟头节点,对于不满足条件的节点逐个删除'''
    dummy_head = ListNode('')
    dummy_head.next = head
    
    cur = dummy_head
    while cur and cur.next:
        if cur.next.val == val:
            cur.next = cur.next.next # 删除cur.next节点
        else:
            cur = cur.next # 移动cur到下一个节点
    return dummy_head.next
 

if __name__ == '__main__':
    alist = [7, 7, 7, 7]
    head = build_linkedlist(alist)
    print(show_linkedlist(head))
    new_head = removeElements(head, val=7)
    print(show_linkedlist(new_head))
    # print(new_head.next.next.next.next.next.val)

```






## 707 设计链表

### [题目描述](https://leetcode.cn/problems/design-linked-list/)


### 思路

### 代码


## 206 反转链表

### [题目描述](https://leetcode.cn/problems/reverse-linked-list/)


### 思路


### 代码