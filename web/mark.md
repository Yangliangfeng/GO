* Go管理工具gopm的安装
```
go get -v github.com/gpmgo/gopm
```
* Go输出的内容转utf8的编码
```
gopm get -g -v golang.org/x/text       //转化html编码为utf8
gopm get -g -v golang.org/x/net/html   //自动检测输出html的编码
```
* Go的Websocket包
```
gopm get -g -v github.com/gorilla/websocket
```
* Go的scrypt密码加密包
```
gopm get -v -g golang.org/x/crypto/scrypt
```
* Go的面向对象
```
1.封装:
    1)包的范围内：通过标识符首字母小写，对象只在它所在的包内可见
    2)可导出的：通过标识符首字母大写，对象对所在包以外也能可见
2.继承：
    用组合实现：内嵌一个（或者多个）包含想要的行为（字段和方法）的类型
3.多态：
    用接口实现：某个类型的实例可以赋给它所实现的任意接口类型的变量，类型和接口是松耦合的，并且多重继承可以通过多个接口实现。
    
```
* make与new的区别
```
new(T)：
用户各种类型的内存分配，它返回了一个指针，指向新分配的类型T的零值
make(T):
make只能创建slice，map，channel类型，并且返回一个有初始值(非零值)的T类型
```
