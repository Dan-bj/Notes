```python
import json

d = {
    '河北': ['保定', '石家庄', '廊坊'],
    '河南': ['洛阳', '郑州', '开封'],
    '山东': ['济南', '青岛', '枣庄'],
}

j = json.dumps(d) # 将字典变成json字符串
data = json.loads(j) # 将json字符串变成字典
print(data['河北'])

f = open('a.txt', 'w')
json.dump(d, f) # 将d转成json字符串并写入文件
f.close()
```