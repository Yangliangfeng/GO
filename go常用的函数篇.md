### 字符串函数
```
1. 统计字符串的长度，按照字节

len(str)

2. 字符串遍历，同时处理有中文的情况

[]rune(str)

3. 字符串转整数

strconv.Atoi("123")

4. 整数转字符串

strconv.Itoa(1234)

5. 字符串转byte

[]byte("hello")

6. []byte 转字符串

string([]byte{2, 9})

7. 十进制转2，8， 16

strconv.FormatInt(123, 2) //转2进制

strconv.FormatInt(123, 8) //转8进制

8. 查找字串是否在字符串中

strings.Contains("wwwwww", "w") //查找"m"是否在"wwwww"中

9.统计字符串出现的次数

strings.Count("heeeeeesss", "e")

10. 不区分大小写的比较字符串（== 是区分大小写的）

strings.EqualFold("abc" , "Abc")

11. 查找字串第一次在字符串中出现的位置，如果没有，则返回 -1

strings.Index("NJL_abc", "abc")

```
