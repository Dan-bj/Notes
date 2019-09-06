```python
import pickle

d = {'name': 'Jack'}

s = pickle.dumps(d) # 将d转换成pickle形式
print(s)
d1 = pickle.loads(s) # 将pickle转换成字典

print(d1)
```