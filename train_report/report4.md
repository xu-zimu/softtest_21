## 测试报告：三角形类型判断单元测试

### 测试目的

验证Triangle类的方法是否能正确判断输入的三角形边长组合，并返回正确的三角形类型。

### 测试用例设计

1. 测试等边三角形：三边长度相等。
2. 测试等腰三角形：两边长度相等。
3. 测试直角三角形：满足勾股定理。
4. 测试一般三角形：不满足以上条件的三角形。
5. 测试无效的三角形：任意两边之和小于或等于第三边。

### 测试代码

```python
import unittest
from triangle import Triangle, InvalidTriangleError

class TestTriangle(unittest.TestCase):
    def test_equilateral_triangle(self):
        # 测试等边三角形
        triangle = Triangle(5, 5, 5)
        self.assertEqual(triangle.get_type(), "等边三角形")

    def test_isosceles_triangle(self):
        # 测试等腰三角形
        triangle = Triangle(3, 3, 4)
        self.assertEqual(triangle.get_type(), "等腰三角形")

    def test_right_triangle(self):
        # 测试直角三角形
        triangle = Triangle(3, 4, 5)
        self.assertEqual(triangle.get_type(), "直角三角形")

    def test_general_triangle(self):
        # 测试一般三角形
        triangle = Triangle(3, 4, 6)
        self.assertEqual(triangle.get_type(), "一般三角形")

    def test_invalid_triangle(self):
        # 测试无效的三角形
        with self.assertRaises(InvalidTriangleError):
            triangle = Triangle(1, 2, 3)

if __name__ == '__main__':
    unittest.main()
```

### 测试执行与结果记录

- 执行测试用例，所有测试均通过。

### 测试结果分析

- test_equilateral_triangle: 测试了等边三角形，输入三边相等，预期输出为等边三角形。
- test_isosceles_triangle: 测试了等腰三角形，输入两边相等，预期输出为等腰三角形。
- test_right_triangle: 测试了直角三角形，输入三边满足勾股定理，预期输出为直角三角形。
- test_general_triangle: 测试了一般三角形，输入三边不满足以上条件，预期输出为一般三角形。
- test_invalid_triangle: 测试了无效的三角形，输入三边无法构成三角形，预期引发InvalidTriangleError异常。