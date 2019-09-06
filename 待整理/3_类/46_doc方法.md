```python
class Foo:
    '我是描述信息'

class Bar(Foo): # 子类无法继承描述信息
    pass

print(Foo.__doc__)
print(Bar.__doc__)
```

class属性和module属性
```python
class Foo:
    pass

f1 = Foo()
print(f1.__class__) # 查看对象属于哪个类
print(f1.__module__) # 查看对象属于哪个模块
print(Foo.__module__)
print(Foo.__class__)
```

del方法
```python
class Open:
    def __init__(self, file_path, mode='r', encoding='utf-8'):
        self.f = open(file_path, mode=mode, encoding=encoding)

    def __del__(self): # 用来处理要关闭的文件、数据库连接 等等。
        print('---del---')
        self.f.close()

f = Open('a.txt')
del f # 触发del运行
```

call方法
```python
class Foo:
    def __call__(self, *args, **kwargs):
        '''
        对象加括号可以运行。
        '''
        print('call')

f1 = Foo()
f1()
```