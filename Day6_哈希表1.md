# 哈希表｜理论基础、242.有效的字母异位词、349. 两个数组的交集、202. 快乐数、1. 两数之和

## 理论基础
### 哈希碰撞
- 拉链法
冲突的元素都被存储在链表中，拉链法就是要选择适当的哈希表的大小，这样既不会因为数组空值而浪费大量内存，也不会因为链表太长而在查找上浪费太多时间。
- 线性探测法

### 总结
当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法。
哈希法也是牺牲了空间换取了时间，因为我们要使用额外的数组，set或者是map来存放数据，才能实现快速的查找。

## 242 有效的字母异位词
```python
def isAnagram(s, t):
    record = [0]*26
    for astr in s:
        record[ord(astr)-ord('a')] += 1

    for bstr in t:
        record[ord(bstr)-ord('a')] -= 1

    for n in record:
        if n != 0:
            return False
    return True
```

## 349 两个数组的交集
```python
def intersection(nums1, nums2):
    record = [0]*1000
    res = []
    for n in nums1:
        if record[n] == 0:
            record[n] = 1

    for m in nums2:
        if record[m] == 1 and m not in res:
            res.append(m)
    return res
```


## 202 快乐数
无限循环，那么也就是说求和的过程中，sum会重复出现
使用集合记录出现的平方和，如果一个中间重复出现则该数不是快乐数

```python
def isHappy(n):
    aset = set()
    while n != 1:
        n_str = str(n)

        square_sum = 0
        for i in n_str:
            square_sum += int(i)**2

        if square_sum in aset:
            return False
        else:
            aset.add(square_sum)
            n = square_sum
    else:
        return True
```

## 1 两数之和
```python
def twoSum(nums, target):
    '''每种输入只会对应一个答案
    数组中同一个元素在答案里不能重复出现
    返回索引'''

    record_dict = {}

    for i in range(len(nums)):
        if nums[i] not in record_dict:
            record_dict[target-nums[i]] = i
        else:
            return [i, record_dict[nums[i]]]
```