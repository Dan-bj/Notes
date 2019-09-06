```python
import time

# time.sleep(1) # 停一秒

# 时间戳
t = time.time() # 返回当前的时间戳，1970年到现在走过多少秒

# 字符串
d = time.strftime('%Y-%m-%d %X')
d = time.strftime('%Y-%m-%d %H:%M:%S')

# 时间元组
t = time.localtime()

# 时间类型转换
# 时间戳 -> 时间元组 -> 字符串
# 字符串 -> 时间元组 -> 时间戳

# 时间戳 -> 时间元组
time.localtime(time.time())

# 时间元组 -> 时间戳
time.mktime(time.localtime())

# 时间元组 -> 字符串
time.strftime('%Y-%m-%d %X', time.localtime())

# 字符串 -> 时间元组
time.strptime('2017-03-03', '%Y-%m-%d')
```