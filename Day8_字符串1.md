# 字符串｜344.反转字符串、541. 反转字符串II、剑指Offer 05.替换空格、151.翻转字符串里的单词、剑指Offer58-II.左旋转字符串

## 344 反转字符串
```python
def reverseString(s):
    left = 0
    right = len(s)-1

    while left <= right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
```

## 541 反转字符串II
```python
def _reverse(slist, left, right):
    while left < right:
        slist[left], slist[right] = slist[right], slist[left]
        left += 1
        right -= 1


def reverseStr(s, k):
    slist = list(s)

    for start in range(0, len(slist), 2*k):
        end = min(start+2*k-1, len(slist)-1)

        if end - start+1 < k:
            _reverse(slist, start, end)
        elif k <= end-start+1 <= 2*k:
            _reverse(slist, start, start+k-1)
    return ''.join(slist)
```
## 剑指Offer 05.替换空格
```python
def replaceSpace(s):
    res = ''
    for astr in s:
        if astr == ' ':
            res += '%20'
        else:
            res += astr
    return res
```

## 151.翻转字符串里的单词
- 去除多余的空格
- 翻转整个字符串
- 翻转每个单词

```python
def reverse_list(slist, left, right):
    '''反转slist[left:right+1]部分的列表'''
    while left < right:
        slist[left], slist[right] = slist[right], slist[left]
        left += 1
        right -= 1


def remove_spaces(slist):
    '''移除多余的空格'''
    fast = 0
    slow = 0

    while fast < len(slist):
        # 不为空格的情况
        if slist[fast] != ' ':
            slist[slow] = slist[fast]
            slow += 1
            fast += 1
        # 保留空格的情况
        elif slist[fast] == ' ' and slow > 0 and slist[slow-1] != ' ':
            slist[slow] = slist[fast]
            slow += 1
            fast += 1
        else:
            fast += 1
    if slist[slow-1] == ' ':
        return slist[:slow-1]
    else:
        return slist[:slow]


def _reverse_words(slist):
    '''反转列表中的每个单词'''
    left = 0
    right = 0
    while left < len(slist):
        while right < len(slist) and slist[right] != ' ':
            right += 1
        else:
            reverse_list(slist, left, right-1)
        right += 1
        left = right


def reverseWords(s):
    slist = list(s)
    # 移除前后空格和中间多余的空格
    slist = remove_spaces(slist)
    # 反转整个列表
    reverse_list(slist, 0, len(slist)-1)
    # 反转列表中的单词
    _reverse_words(slist)
    return ''.join(slist)


if __name__ == '__main__':
    s = "  aa bb  "
    slist = list(s)
    print(repr(reverseWords(slist)))
```

## 剑指Offer58-II.左旋转字符串
```python
def reverseLeftWords(s, n):
    k = n % len(s)
    return s[k:]+s[:k]
```