```python
# 把对象操作属性模拟成字典形式
class Foo:
    def __init__(self, name):
        self.name = name

    def __getitem__(self, item):
        return self.__dict__[item]

    def __setitem__(self, key, value):
        self.__dict__[key] = value

    def __delitem__(self, key):
        self.__dict__.pop(key)

f = Foo('aaa')
f['name'] # 触发getitem运行
f['age'] = 18 # 触发setitem运行
del f['age'] # 触发delitem运行

print(f.__dict__)
```