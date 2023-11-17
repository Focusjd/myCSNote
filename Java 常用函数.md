# Java 常用函数

1. **length()**: 返回字符串的长度。

   ```java
   String str = "algorithm";
   int len = str.length();  // 9
   ```

2. **charAt(int index)**: 返回指定索引处的字符。

   ```java
   char ch = str.charAt(3);  // 'o'
   ```

3. **substring(int beginIndex, int endIndex)**: 返回一个新字符串，它是此字符串的一个子字符串。

   ```java
   String sub = str.substring(1, 4);  // "lgo"
   ```

4. **indexOf(String substring)**: 返回指定子字符串第一次出现的索引。

   ```java
   int index = str.indexOf("go");  // 6
   ```

5. **lastIndexOf(String substring)**: 返回指定子字符串最后一次出现的索引。

   ```java
   int lastIndex = str.lastIndexOf("o");  // 7
   ```

6. **split(String regex)**: 使用给定的正则表达式将此字符串分割为数组。

   ```java
   String[] parts = "a-b-c".split("-");  // ["a", "b", "c"]
   ```

7. **replace(char oldChar, char newChar)**: 返回一个新字符串，结果是通过替换其字符而产生的。

   ```java
   String replaced = str.replace('a', 'z');  // "zlgorithm"
   ```

8. **startsWith(String prefix)** 和 **endsWith(String suffix)**: 测试此字符串是否以指定的前缀或后缀开始或结束。

   ```java
   boolean start = str.startsWith("alg");  // true
   boolean end = str.endsWith("rithm");    // true
   ```

9. **toLowerCase()** 和 **toUpperCase()**: 分别转换为小写或大写。

   ```java
   String lower = str.toLowerCase();  // "algorithm"
   String upper = str.toUpperCase();  // "ALGORITHM"
   ```

10. **trim()**: 返回字符串的副本，忽略前导空白和尾部空白。

```java
String trimmed = "  trim me  ".trim();  // "trim me"
```

1. **equals(Object anObject)**: 将此字符串与指定的对象比较。

```java
boolean isEqual = str.equals("algorithm");  // true
```

1. **compareTo(String anotherString)**: 按字典顺序比较两个字符串。

```java
int comparison = "apple".compareTo("banana");  // negative value since 'apple' is lexicographically before 'banana'
```

1. **isEmpty()**: 返回字符串是否为空。

```java
boolean empty = "".isEmpty();  // true
```

1. **contains(CharSequence sequence)**: 检查是否包含指定的字符序列。

```java
boolean hasSub = str.contains("go");  // true
```



## Stream

`list.stream().mapToInt(i -> i).toArray();` 这行代码的作用是将 `List<Integer>` 类型的集合转换成一个原始类型的 `int[]` 数组。

流操作分为类：中间操作（中间操作）和终端操作（终端操作）。

- **中间操作**：这些操作返回另一个Stream。它们是延迟执行的，例如`filter`，，`map`。`sorted`
  - `filter(Predicate<T>)`：过滤元素。
  - `map(Function<T, R>)`：转换每个元素。
  - `sorted()`：排序。
- **终端操作**：这些操作返回一个非Stream的结果，并且触发实际计算，例如`forEach`, `collect`, `reduce`。
  - `forEach(Consumer<T>)`：迭代每个元素。
  - `collect(Collector<T, A, R>)`：将元素转换成其他形式。
  - `reduce(BinaryOperator<T>)`：将所有元素合并成一个结果。



#### 中间操作

1. **`filter(Predicate<T>)`**：

   ```java
   List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
   List<Integer> evenNumbers = numbers.stream()
                                       .filter(n -> n % 2 == 0)
                                       .collect(Collectors.toList());
   // 结果: [2, 4]
   ```

2. **`map(Function<T, R>)`**：
   ```java
   
   List<String> words = Arrays.asList("Java", "Stream", "API");
   List<Integer> wordLengths = words.stream()
                                    .map(String::length)
                                    .collect(Collectors.toList());
   // 结果: [4, 6, 3]
   ```

3. **`flatMap(Function<T, Stream<R>>)`**：

   ```java

   List<List<Integer>> nestedNumbers = Arrays.asList(
       Arrays.asList(1, 2),
       Arrays.asList(3, 4, 5)
   );
   List<Integer> flatList = nestedNumbers.stream()
                                         .flatMap(List::stream)
                                         .collect(Collectors.toList());
   // 结果: [1, 2, 3, 4, 5]
   ```

4. **`distinct()`**：

   ```java

   List<Integer> numbersWithDuplicates = Arrays.asList(1, 2, 2, 3, 3, 3);
   List<Integer> distinctNumbers = numbersWithDuplicates.stream()
                                                        .distinct()
                                                        .collect(Collectors.toList());
   // 结果: [1, 2, 3]
   ```

5. **`sorted()`**：

   ```java

   List<Integer> numbers = Arrays.asList(4, 1, 3, 5, 2);
   List<Integer> sortedNumbers = numbers.stream()
                                        .sorted()
                                        .collect(Collectors.toList());
   // 结果: [1, 2, 3, 4, 5]
   ```

6. **`limit(long n)`**：

   ```java
   List<Integer> firstThreeNumbers = numbers.stream()
                                            .limit(3)
                                            .collect(Collectors.toList());
   // 结果: [1, 2, 3]
   ```

7. **`skip(long n)`**：

   ```java
   List<Integer> afterSkippingFirstThree = numbers.stream()
                                                  .skip(3)
                                                  .collect(Collectors.toList());
   // 结果: [4, 5]
   ```

#### 终端操作

1. **`forEach(Consumer<T>)`**：

   ```java
   numbers.forEach(System.out::println);
   // 输出: 1 2 3 4 5
   ```

2. **`collect(Collector<T, A, R>)`**：

   ```java
   String combinedString = words.stream()
                                .collect(Collectors.joining(", "));
   // 结果: "Java, Stream, API"
   ```

3. **`reduce(BinaryOperator<T>)`**：

   ```java
   int sum = numbers.stream()
                    .reduce(0, Integer::sum);
   // 结果: 15
   ```

4. **`anyMatch(Predicate<T>)`**：

   ```java
   boolean hasEvenNumber = numbers.stream()
                                  .anyMatch(n -> n % 2 == 0);
   // 结果: true
   ```

5. **`allMatch(Predicate<T>)`**：

   ```java
   boolean allEvenNumbers = numbers.stream()
                                   .allMatch(n -> n % 2 == 0);
   // 结果: false
   ```

6. **`noneMatch(Predicate<T>)`**：

   ```java
   boolean noOddNumbers = numbers.stream()
                                 .noneMatch(n -> n % 2 != 0);
   // 结果: false
   ```

7. **`findFirst()`**：

   ```java
   Optional<Integer> first = numbers.stream()
                                    .findFirst();
   // 结果: Optional[1]
   ```

8. **`count()`**：

   ```java
   long count = numbers.stream()
                       .count();
   // 结果: 5
   ```



#### Integer.valueOf()

`Integer.valueOf(String s, int radix)` 是Java中的一个方法，用于将给定基数（radix）下的字符串表示的数转换为`Integer`对象。这里，`s`是要解析的字符串，而`radix`是解析时使用的基数。例如，对于十进制数字，基数是10；对于二进制，基数是2；对于十六进制，基数是16。

#### getClass()

使用`getClass()`方法来查看一个对象的类型。这个方法是从`java.lang.Object`类继承来的，因此所有的Java对象都继承了这个方法。

#### instanceof

使用`instanceof`关键字来检查对象是否是特定类的实例

```java
if (obj instanceof MyObject) {
    System.out.println("对象是 MyObject 的实例");
}
```

