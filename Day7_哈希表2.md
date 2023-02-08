# 哈希表｜454.四数相加II、383. 赎金信、15. 三数之和、18. 四数之和

## 454 四数相加II
```python
def fourSumCount(nums1, nums2, nums3, nums4):
    cnt = 0
    adict = {}
    for n in nums1:
        for m in nums2:
            adict[n+m] = adict.get(n+m, 0)+1

    for a in nums3:
        for b in nums4:
            cnt += adict.get(0-(a+b), 0)
    return cnt
```

## 383 赎金信
- 使用字典作为哈希表
- 还可以使用数组作为哈希表
```python
def canConstruct(ransomNote, magazine):
    adict = {}

    for m in magazine:
        adict[m] = adict.get(m, 0)+1

    for r in ransomNote:
        if adict.get(r, 0) == 0:
            return False
        else:
            adict[r] = adict.get(r, 0)-1
    return True

```
## 15 三数之和
```python
def threeSum(nums):
    res = []
    length = len(nums)
    nums.sort()

    for i in range(length):
        # nums[i]去重
        if i > 0 and nums[i] == nums[i-1]:
            continue
        # 如果第一个数大于0，后面的和只能是大于0
        if nums[i] > 0:
            break
        left = i+1
        right = length-1

        while left < right:
            summ = nums[i]+nums[left]+nums[right]
            if summ < 0:
                # 左指针右移+去重
                while left < right and nums[left] == nums[left+1]:
                    left += 1
                left += 1
            elif summ > 0:
                # 右指针左移+去重
                while left < right and nums[right] == nums[right-1]:
                    right -= 1
                right -= 1
            else:
                res.append([nums[i], nums[left], nums[right]])
                # 左指针右移+去重
                while left < right and nums[left] == nums[left+1]:
                    left += 1
                left += 1
                # 右指针左移+去重
                while left < right and nums[right] == nums[right-1]:
                    right -= 1
                right -= 1
    return res
```

## 18 四数之和
```python
def fourSum(nums, target):
    nums.sort()
    length = len(nums)
    res = []

    for i in range(length-3):
        # 第一个数去重
        if i > 0 and nums[i] == nums[i-1]:
            continue
        # 第一个数剪枝
        if nums[i] > target > 0:
            break
        for j in range(i+1, length-2):
            # 第二个数去重
            if j > i+1 and nums[j] == nums[j-1]:
                continue
            # 第二个数剪枝
            if nums[i]+nums[j]>target>0:
                break

            # 双指针遍历
            left = j+1
            right = length - 1

            while left < right:
                summ = nums[i]+nums[j]+nums[left]+nums[right]
                if summ < target:
                    left += 1
                elif summ > target:
                    right -= 1
                else:
                    res.append([nums[i], nums[j], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left+1]:
                        left += 1
                    left += 1
                    while left < right and nums[right] == nums[right-1]:
                        right -= 1
                    right -= 1
    return res
```