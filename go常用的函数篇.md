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

12. 查找字串最后一次在字符串中出现的位置，如果没有，则返回 -1

strings.LastIndex("NJL_abc", "abc")

13. 将目标字符串替换成指定字符串

strings.Replace("go go Hello", "go", "Go语言" , n)//将"go"替换成"Go语言",n 指定替换多少个，n = -1 表示全部替换

14.字符串的分割成数组

strings.Split("he,woo,wdddd", ",")

15. 字符串的大小写转换

strings.ToUpper("go") //大写   strings.ToLower("Go") //小写

16. 去掉字符串首尾的空格

strings.TrimSpace(str)

17. 去掉字符串首位指定的字符

strings.Trim("! hello  !", " !") // 去掉首位的空白和！字符

18.去掉字符串左或者右的指定字符

strings.TrimLeft()     strings.TrimRight()

```
