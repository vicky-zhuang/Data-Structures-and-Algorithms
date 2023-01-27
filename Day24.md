# 代码随想录算法训练营 第二十四天|回溯算法理论基础、77.组合

## 回溯算法理论基础
回溯法就是解决k层for循环嵌套的问题

### 可解决的问题
- 组合(无序)：N个数里面按照一定规则找出k个数的集合
- 切割：一个字符串按一定规则有几种切割方式
- 子集：一个N个数的集合里有多少符合条件的子集
- 排列(有序)：N个数按一定规则全排列，有几种排列方式
- 棋盘问题：N皇后，数独

### 回溯搜索的遍历过程
回溯法一般是在集合中递归搜索，集合的大小构成了树的宽度，递归的深度构成了数的深度

### 回溯法的算法模板
```
void backtracking(参数) {
    if (终止条件) {
        存放结果; # 收集结果
        return;
    }
    # 单层搜索
    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); #递归
        回溯，撤销处理结果
    }
}
```

### 回溯三部曲
- 递归参数，返回值
- 终止条件
- 单层搜索的逻辑


## 77 组合

### [题目描述](https://leetcode.cn/problems/combinations/submissions/397390284/）

### 代码1

```python
def combine(n, k):
    '''不剪枝版本'''
    result = []  # 二维数组：存放最终结果
    path = []  # 一维数组：记录单条路径

    # 回溯函数
    def backtracking(n, k, start_idx):
        if len(path) == k:  # 终止条件
            result.append(path[:])  # 存放结果
            return  # 结束函数

        for i in range(start_idx, n+1):  # 单层搜索
            path.append(i)  # 处理节点
            backtracking(n, k, i+1)  # 递归
            path.pop()  # 回溯，撤销处理节点

    backtracking(n, k, 1)  # 调用回溯算法，解决问题
    return result
```

```python
def combine(n, k):
    '''剪枝版本'''
    result = []  # 二维数组：存放最终结果
    path = []  # 一维数组：记录单条路径

    # 回溯函数
    def backtracking(n, k, start_idx):
        if len(path) == k:  # 终止条件
            result.append(path[:])  # 存放结果
            return  # 结束函数

        # 剪枝处理的是子节点，找到对于当前的path最右的startidx
        # 需要的元素：k-len(path)
        # 每个startidx提供的节点数：n-startidx+1
        # k-len(path)=n-startidx+1
        # 最右的startidx=n-k+len(path)+1
        for i in range(start_idx, n-k+len(path)+2):  # 单层搜索
            path.append(i)  # 处理节点
            backtracking(n, k, i+1)  # 递归
            path.pop()  # 回溯，撤销处理节点

    backtracking(n, k, 1)  # 调用回溯算法，解决问题
    return result
```

