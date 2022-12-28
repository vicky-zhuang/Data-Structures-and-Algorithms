# 代码随想录算法训练营 第一天|704. 二分查找、27. 移除元素

数组理论基础

- 704.二分查找
	- 35.搜索插入位置
	- 34.在排序数组中查找元素的第一个和最后一个位置
- 27. 移除元素
## 704 二分查找
要求：要熟悉 根据 左闭右开，左闭右闭 两种区间规则 写出来的二分法。

### 题目描述：

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，

写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

### 思路

对于有序数组(此处设为升序)通常使用二分查找提高查找效率，首先将元素中间位置的元素`mid`和`target`进行比较，然后根据结果选择其中一半继续寻找`target`

- `mid = target`找到元素，返回索引值
- `mid > target`,在数组的左半部分寻找
- `mid < target`，在数组的右半部分寻找
- 如果`left > right`,则元素不在此数组中

时间复杂度：`O(logn)`

### 代码

```python
def binary_search(nums, target, left, right):
    '''left-right是闭区间'''
    while left <= right:
        mid = (left+right)//2
        if nums[mid] == target:
            return mid
        elif nums[mid] > target:
            return binary_search(nums, target, left, mid-1)
        elif nums[mid] < target:
            return binary_search(nums, target, mid+1, right)
    else:
        return -1


def search(nums, target):
    return binary_search(nums, target, 0, len(nums)-1)


if __name__ == '__main__':
    nums = [-1, 0, 3, 5, 9, 12]
    target = 100
    print(search(nums, target))
```




## 移除元素
要求： 暴力的解法，双指针法

### 题目描述

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

### 思路

#### 双指针法

设定两个指针，指针1寻找不等于`val`的元素，指针2则指向存储元素的位置。

- 如果指针1指向的元素不等于`val`，那么修改指针2对应位置的元素，两个指针都向前移动1
- 如果指针1指向的元素等于`val`，那么指针1继续往前移动寻找不等于`val`的元素，指针1向前移动1

### 代码

```python
def removeElement(nums, val):
    left = 0 # 指针2:存储元素的位置
    right = 0 # 指针1:寻找不等于val的元素

    while right < len(nums):
        if nums[right] != val:
            nums[left] = nums[right]
            left += 1
            right += 1
        else:
            right += 1
    return left


if __name__ == '__main__':
    nums = [0, 1, 2, 2, 3, 0, 4, 2]
    val = 2
    print(removeElement(nums, val))
```



