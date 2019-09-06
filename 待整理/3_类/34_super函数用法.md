### 用 super 调用父类方法
```python
class A:
    def foo(self, name):
        print(name)

class B(A):
    def foo(self, name):
        super().foo(name) # 使用父类的方法
        print('B')

b1 = B()
b1.foo(123)
```