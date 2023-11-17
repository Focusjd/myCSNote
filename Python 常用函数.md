# Python 常用函数

1. **len(s)**: 返回字符串的长度。

   ```python
   pythonCopy code
   s = "algorithm"
   length = len(s)  # 9
   ```

2. **s[index]**: 访问指定索引处的字符。

   ```python
   pythonCopy code
   char = s[3]  # 'o'
   ```

3. **s[start:end]**: 切片操作，返回一个子字符串。

   ```python
   pythonCopy code
   sub = s[1:4]  # "lgo"
   ```

4. **s.find(sub)**: 返回子字符串第一次出现的索引，如果没有找到返回-1。

   ```python
   pythonCopy code
   index = s.find("go")  # 6
   ```

5. **s.rfind(sub)**: 返回子字符串最后一次出现的索引，如果没有找到返回-1。

   ```python
   pythonCopy code
   rindex = s.rfind("o")  # 7
   ```

6. **s.split(delimiter)**: 使用给定的分隔符将字符串分割为列表。

   ```python
   pythonCopy code
   parts = "a-b-c".split("-")  # ['a', 'b', 'c']
   ```

7. **s.replace(old, new)**: 返回一个新字符串，结果是通过替换其字符而产生的。

   ```python
   pythonCopy code
   replaced = s.replace('a', 'z')  # "zlgorithm"
   ```

8. **s.startswith(prefix)** 和 **s.endswith(suffix)**: 检查字符串是否以指定的前缀或后缀开始或结束。

   ```python
   pythonCopy code
   start = s.startswith("alg")  # True
   end = s.endswith("rithm")    # True
   ```

9. **s.lower()** 和 **s.upper()**: 分别转换为小写或大写。

   ```python
   pythonCopy code
   lower = s.lower()  # "algorithm"
   upper = s.upper()  # "ALGORITHM"
   ```

10. **s.strip(chars)**: 返回字符串的副本，删除前导和尾部的字符，默认删除空白字符。

```python
pythonCopy code
trimmed = "  trim me  ".strip()  # "trim me"
```

1. **s == other**: 比较两个字符串是否相等。

```python
pythonCopy code
isEqual = s == "algorithm"  # True
```

1. **s in other**: 检查一个字符串是否包含另一个子字符串。

```python
pythonCopy code
contains = "go" in s  # True
```

1. **s.join(iterable)**: 使用字符串将可迭代对象中的元素连接成一个新字符串。

```python
pythonCopy code
joined = "-".join(['a', 'b', 'c'])  # "a-b-c"
```