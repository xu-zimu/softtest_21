# 黑盒测试用例设计

## 等价类划分

### 有效等价类

1. 三条边都在1到100之间的正数。
2. 三条边可以构成三角形：
   - 等边三角形：三条边相等。
   - 等腰三角形：两条边相等。
   - 一般三角形：三条边不相等。
   - 直角三角形：满足勾股定理。

### 无效等价类

1. 任意一条边小于1或大于100。
2. 任意一条边为非正数（零或负数）。
3. 输入非数字字符。
4. 三条边不能构成三角形（任意两边之和小于或等于第三边）。
5. 输入2个数。
6. 输入4个数。

## 边界值分析

1. 最小边界值：1
2. 中值边界值 : 50
3. 最大边界值：100

## 黑盒测试用例

| 用例编号 | 用例名称                         | 优先级 | 输入数据      | 预期输出       | 实际输出                        | 是否通过 | 错误级别 |
| -------- | -------------------------------- | ------ | ------------- | -------------- | ------------------------------- | -------- | -------- |
| 001      | 等边,三个数,最小边界值           | 高     | 1, 1, 1       | 等边三角形     | 等边三角形                      | 通过     |          |
| 002      | 等腰三角形,最大边界值,中值边界值 | 高     | 100, 100, 50  | 等腰三角形     | 等腰三角形                      | 通过     |          |
| 003      | 一般三角形                       | 高     | 4, 5, 6       | 一般三角形     | 一般三角形                      | 通过     |          |
| 004      | 直角三角形                       | 高     | 3, 4, 5       | 直角三角形     | 直角三角形                      | 通过     |          |
| 005      | 无法构成三角形                   | 中     | 1, 2, 3       | 不能构成三角形 | 一般三角形                      | 不通过   | 致命     |
| 006      | 边长为零                         | 中     | 0, 5, 5       | 输入不合法     | 提示:三角形边长不在指定范围之内 | 待定     | 需要沟通 |
| 007      | 负数输入                         | 中     | -3, 4, 5      | 输入不合法     | 提示:三角形边长不在指定范围之内 | 待定     | 需要沟通 |
| 008      | 范围外                           | 中     | 101, 50, 50   | 输入不合法     | 提示:三角形边长不在指定范围之内 | 待定     | 需要沟通 |
| 009      | 非数字输入                       | 中     | 'a', 4, 5     | 输入不合法     | 提示:三角形边长不在指定范围之内 | 待定     | 需要沟通 |
| 010      | 小数输入                         | 中     | 3.5, 4.5, 5.5 | 不构成三角形   | 直角三角形                      | 不通过   | 致命     |
| 011      | 2个数                            | 低     | 1, 2, null    | 不能构成三角形 | 不允许提交                      | 待定     | 需要沟通 |
| 012      | 4个数                            | 低     | 1,2,3,4       | 不能构成三角形 | 无法输入                        | 通过     |          |



# 白盒测试用例设计

使用python语言的三角形类型判断逻辑如下：

```python
def is_triangle(a, b, c):
    if a <= 0 or b <= 0 or c <= 0 or a > 100 or b > 100 or c > 100:
        return "输入不合法"
    if a + b <= c or a + c <= b or b + c <= a:
        return "不能构成三角形"
    if a == b == c:
        return "等边三角形"
    if a == b or b == c or a == c:
        if a**2 + b**2 == c**2 or a**2 + c**2 == b**2 or b**2 + c**2 == a**2:
            return "直角三角形"
        return "等腰三角形"
    if a**2 + b**2 == c**2 or a**2 + c**2 == b**2 or b**2 + c**2 == a**2:
        return "直角三角形"
    return "一般三角形"
```

## 白盒测试用例

| 用例编号 | 用例名称       | 优先级 | 输入数据    | 预期输出       | 实际输出                        | 是否通过 | 错误级别 |
| -------- | -------------- | ------ | ----------- | -------------- | ------------------------------- | -------- | -------- |
| 001      | 边长小于等于零 | 高     | 0, 5, 5     | 输入不合法     | 提示:三角形边长不在指定范围之内 | 待定     | 需要沟通 |
| 002      | 边长大于100    | 高     | 101, 50, 50 | 输入不合法     | 提示:三角形边长不在指定范围之内 | 待定     | 需要沟通 |
| 003      | 不能构成三角形 | 高     | 1, 2, 3     | 不能构成三角形 | 一般三角形                      | 不通过   | 致命     |
| 004      | 等边三角形     | 高     | 5, 5, 5     | 等边三角形     | 等边三角形                      | 通过     | 无       |
| 005      | 等腰三角形     | 高     | 5, 5, 8     | 等腰三角形     | 等腰三角形                      | 通过     | 无       |
| 006      | 直角三角形     | 高     | 3, 4, 5     | 直角三角形     | 直角三角形                      | 通过     | 无       |
| 007      | 一般三角形     | 高     | 4, 5, 6     | 一般三角形     | 一般三角形                      | 通过     | 无       |