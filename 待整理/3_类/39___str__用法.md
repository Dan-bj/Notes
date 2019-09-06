```python
# __str__ 的用法
class People:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self): # 打印类产生的对象时会触发执行
        return '(name: %s, age: %s)' % (self.name, self.age) # 必须返回字符串类型

p1 = People('aaa', 18)
print(p1)
```