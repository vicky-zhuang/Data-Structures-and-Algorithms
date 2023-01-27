# 代码随想录算法训练营 第二十五天|216.组合总和III、17.电话号码的字母组合

## 216 组合III

### [题目描述](https://leetcode.cn/problems/combination-sum-iii/submissions/)

### 代码
```python
def combinationSum3(k, n):
    result = []
    path = []

    def backtracking(k, target_sum, current_sum, start_idx):
        if len(path) == k and current_sum == target_sum:  # 路径满足条件
            result.append(path[:])
            return
        elif current_sum > target_sum:  # 和超出了范围，剪枝
            return
        elif len(path) == k:  # 长度超过范围，剪枝
            return

        # 单层搜索
        for i in range(start_idx, 10-k+len(path)+1):  # 不能满足路径所需的元素个数，剪枝
            current_sum += i  # 记录当前路径的元素的和
            path.append(i)  # 处理节点
            backtracking(k, target_sum, current_sum, i+1)  # 递归
            current_sum -= i
            path.pop()  # 回溯，节点弹出
    backtracking(k, n, 0, 1)
    return result


if __name__ == '__main__':
    print(combinationSum3(k=3, n=7))
```

## 17 电话号码的字母组合

### [题目描述](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

### 代码
```python
# 电话号码的数字组合
def letterCombinations(digits):
    if digits == '':
        return []
    DICT = {'2': 'abc', '3': 'def',
            '4': 'ghi', '5': 'jkl',
            '6': 'mno', '7': 'pqrs',
            '8': 'tuv', '9': 'wxyz'}
    global path
    path = ''
    result = []

    def backtracking(start_idx):
        global path
        if len(path) == len(digits):  # 终止条件：字母的长度等于数字的长度
            result.append(path)
            return

        slist = DICT[digits[start_idx]]  # 待选的字母列表
        for s in slist:
            path += s
            backtracking(start_idx+1)
            path = path[:-1]
    backtracking(0)
    return result


if __name__ == '__main__':
    print(letterCombinations(''))
```