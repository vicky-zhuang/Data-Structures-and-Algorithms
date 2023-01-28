# 代码随想录算法训练营 第二天|977.有序数组的平方、209.长度最小的子数组、59.螺旋矩阵I

## 977 有序数组的平方

### [题目描述](https://leetcode.cn/problems/squares-of-a-sorted-array/)

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

### 思路

**双指针法**

原始数据以从小到大的顺序排列，那么平方之后元素的数值从数组的两端到中间从大到小。

设定两个指针，分别指向数组的两端，比较两个数值的绝对值的大小，将最大的数放入最后的列表中。

### 代码

```python
def sortedSquares(nums):
    length = len(nums)
    left, right = 0, length-1
    res = [-1]*length
    k = length-1
    while left <= right:
        if abs(nums[left]) >= abs(nums[right]):
            res[k] = nums[left]**2
            left += 1
        else:
            res[k] = nums[right]**2   
            right -= 1
        k -= 1
    return res


if __name__ == '__main__':
    nums = [-4, -1, 0, 3, 10]
    print(sortedSquares(nums))
```



## 209 长度最小的子数组

### [题目描述](https://leetcode.cn/problems/minimum-size-subarray-sum/)

给定一个含有 `n` 个正整数的数组和一个正整数 `target` **。**

找出该数组中满足其和 `≥ target` 的长度最小的 **连续子数组** `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度**。**如果不存在符合条件的子数组，返回 `0` 。

### 思路

设定左右两个指针，两个指针形成的闭区间即连续子数组。

- 如果整个数组的和都小于`target`,那么直接返回`0`。否则进入下面的循环：

  - 如果子数组的和`<target`,右指针后移，和增加；

  - 如果子数组的和`>=target`,减去左指针指向的元素，左指针右移；

  - 上述循环重复进行直到右指针移到最右端。

### 代码

```python
def minSubArrayLen(target,nums):
    length = len(nums)
    if sum(nums)<target: # 整个数组的和都小于target的话，直接返回0
        return 0
    left,right = 0,0 # 此处的right是闭区间
    summ = nums[right] 
    min_len = length
    while right<length:
        while right<length and summ<target: 
            right += 1
            if right>=length:
                return min_len
            else:
                summ += nums[right]
        while right<length and summ>=target:
            min_len = min(min_len,right-left+1)
            summ -= nums[left]
            left += 1


if __name__ == '__main__':
    target = 7
    nums = [2,3,1,2,4,3]
    print(minSubArrayLen(target,nums))
```



## 59 螺旋矩阵I

### [题目描述](https://leetcode.cn/problems/spiral-matrix-ii/)

给你一个正整数 `n` ，生成一个包含 1到 $n^2$ 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

### 思路

将生成螺旋矩阵的整个过程简化为顺时针填充矩阵四周中的数值，按圈填充。

在进行每一圈的填充的时候，有以下细节：

- 指定左上、右下的位置和开始填充的数字
- 按照顺指针顺序设定四个循环，在每一行或者列的填充中最后一个总是放在下个循环中填充

### 代码

```python
def generateMatrix(n):
    mat = [[0 for _ in range(n)] for _ in range(n)]
    num = 1
    for i in range(n//2+1):
        if i != n-i-1:
            num = circle(mat,i,n-i-1,num)
        else:
            mat[i][i]=num
    return mat

def circle(mat,up,down,num):
    '''设定上下左右边界
    和准备填充的数字'''
    left,right = up,down
    # 从左到右
    for i in range(left,right):
        mat[up][i]=num
        num += 1
    # 从上到下
    for j in range(up,down):
        mat[j][right]=num
        num += 1
    # 从右到左
    for k in range(right,left,-1):
        mat[down][k]=num
        num += 1
    # 从下到上
    for l in range(down,up,-1):
        mat[l][left]=num
        num += 1
    return num


if __name__ == '__main__':
    generateMatrix(3)
```

