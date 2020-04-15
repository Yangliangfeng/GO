### GO面试知识点准备

* Go语言中byte、rune与字符串区别
```
1. byte，占用1个节字,所以它和 uint8 类型本质上没有区别，它表示的是 ACSII 表中的一个字符

2. rune，占用4个字节，所以它和 uint32 本质上也没有区别，它表示的是一个 Unicode字符

3. byte 和 rune 都是字符类型，若多个字符放在一起，就组成了字符串，也就是这里要说的 string 类型
```
* Go语言中默认是指针的类型
```
map，channel，interface，slice，func
```
