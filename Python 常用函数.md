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



## 数学运算

Python 在内置的数学模块 `math` 中提供了类似的功能，还包括一些其他的数学相关模块，如 `random`、`numpy`（用于数值计算的第三方库）等。

1. **基本算术运算**：加 (`+`)、减 (`-`)、乘 (`*`)、除 (`/`)、整除 (`//`)、取模 (`%`)、幂 (`**`)。
2. **指数运算**：
   - `pow(x, y)`：计算 `x` 的 `y` 次幂。
   - `math.sqrt(x)`：计算平方根。
3. **三角函数**：
   - `math.sin(x)`、`math.cos(x)`、`math.tan(x)`：正弦、余弦和正切函数。
   - `math.asin(x)`、`math.acos(x)`、`math.atan(x)`：反三角函数。
4. **对数函数**：
   - `math.log(x[, base])`：计算对数，`base` 是可选的底数，默认为 `e`。
5. **取整和绝对值**：
   - `round(x)`：四舍五入。
   - `math.ceil(x)`：向上取整。
   - `math.floor(x)`：向下取整。
   - `abs(x)`：绝对值。
6. **其他**：
   - `max(x1, x2, ...)`、`min(x1, x2, ...)`：最大值和最小值。
   - `random.random()`：生成一个介于 0.0 到 1.0 之间的随机数。