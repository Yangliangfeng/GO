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

19. 判断字符串是否以指定字符结束

strings.HasSufffix("abc.jpg", ".jpg") //true

20. 判断字符串是否以指定的字符开头

strings.HasPrefix("ftp://www.baidu.com", "ftp:")

```
### 格式化时间
 ```
 1. 格式化显示当前时间(第一种方式)
 
 now := time.Now()
 
 fmt.Sprintf("%04d-%02d-%02d %02d:%02d:%02d", now.Year(), now.Month(), now.Day(), now.Hour(), 
 
 now.Minute(), now.Second())
 
 2. 格式化显示当前时间(第二种方式)
 
 now.Format("2006-01-02 15:04:05")  //里面的时间是固定的，据说是Go语言创建的原始时间
 
 now.Format("01") //显示当前的月份
 
 now.Format("02") //显示当前的天
 ```
 3. 时间的常量
 ```
 const (
     Nanosecond    //纳秒
     Microsecond   //微秒
     Millisecond   //毫秒
     Second   //秒
     Minute   //分钟
     Hour     //小时
 )
 ```
 4. 休眠
 ```
 time.Sleep(100 * time.Millisecond)  //休眠100毫秒
 ```
 5. 获取当前时间戳
 ```
 time.Now().Unix() //当前时间戳
 
 time.Now().UnixNano() 
 ```
 ### 内置函数
 ```
 1. new: 用来分配内存的，主要用来分配值类型，比如int，float，struct，返回零值的指针
  
 num1 := new(int)
 这里new干了3件事：
 1）开辟了一块内存空间，地址为addr1,里面存储数字0
 2）然后，再开辟另外一块内存空间，地址addr2,把上一块内存的地址addr1存储到addr2的空间内。
 3) 让num1指向地址addr2
 fmt.Prinf("num1的类型 num1 = %T, num1的值 num1 = %v，num1的地址 num1 = %v, num1这个指针指向的值 num1 = %v", num1, num1, &num1, *num1)
 ```
