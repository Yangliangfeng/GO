### GO面试知识点准备

* http状态码
```
1. 400 bad request，请求报文存在语法错误

2. 401 unauthorized，表示发送的请求需要有通过 HTTP 认证的认证信息(未授权)

3. 403 forbidden，表示对请求资源的访问被服务器拒绝

4. 404 not found，表示在服务器上没有找到请求的资源

5. 301 redirect，永久重定向，适用于域名的跳转

6. 302 redirect，临时性的重定向，适用于未登录跳转

7. 504，网关超时，比如nginx在设置了超时时间内没有收到请求时，就会返回504

8. 502，网关超时，比如可能php-fpm挂了，无法与nginx进行连接；可能是backlog队列
```
* new和make之间的区别
```
1. 指针：带类型的

2. new： 用来初始化值类型指针的（var a *int）

3. make：用来初始化slice,map,channel等引用类型的
```
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
* Go的切片浅拷贝和深拷贝的写法和区别
```
切片的数据结构是：指针，len —切片的长度，cap —切片的容量

1)	浅拷贝和深拷贝的区别是：浅拷贝是共享同一个底层数组空间，深拷贝不是共用一个底层数组空间

2) 写法：
    
    浅拷贝：
	      a := []int{1, 2, 3}
		    b := a
        
    深拷贝：
        a := []int{1, 2, 3}
        b := make([]int,len(a), cap(a)) //必须这种写法
        copy(b,a)
```
* Go的struct能不能比较
```
1) 分析
   
   type User struct {
      Id int
   }
   u1 := User{101}
   u2 := User{101}
   这个user结构体的成员变量中只含有int类型，实例化后是可以比较的，如果user结构体中含有func，map，slice的成员变量
   
   （引用类型），那么则是不可以比较 的；如果&User{101}，取的是指针地址，则也是不能比较的

    type User1 struct {
        Id int
    }
    type User2 struct {
        Id int
    }
    
    u1 := User1{101}
    u2 := User2{101}
    fmt.Println(u1 == User1(u2)) //能够把u2转化为u1
    
    答案：
    
    相同结构，只要成员变量能比较，就能比较
    
    不相同的结构，如果能相互转化，也能比较。前提是成员能够比较
    
    比如：不能比较的类型有：func, map, slice
```
* 说一说Go的内存逃逸分析
```
1. 基础补缺：

   1）逃逸分析是：
        Go在编译阶段确定内存是分配到栈上还是在堆上的一种行为
   
   2）几个底层知识点：
        1. 栈内存的分配和释放非常的快
        
        2. 堆内存需要依靠Go垃圾回收（占CPU）
        
        3. 通过逃逸分析，可以尽量把那些不需要分配在堆上的变量直接分配到栈上
        
    3）分析逃逸分析的命令
       go build -gcflags=-m /src/main.go

2. 答案分析：
  
  1）局部变量原本应该在栈中分配，在栈中回收，由于外部的引用，所以，有返回值（这个时候分配在堆上）
    
     这个时候就发生了逃逸。如果函数的返回值外部没有引用到，那么可以进行代码优化，不需要返回值
    
     func test1() []int{ //有返回值，所以，发生了逃逸
	      a := []int{1, 2 ,3, 4}
	      a[1] = 100
	      return a
      }
  
  2）参数为inteface{}类型，比如fmt.println(a ...interface{})，编译期间很难确定其参数的具体类型，也能产生逃逸
    
     因此，开发过程中，如果能确定参数的类型，就用确定类型
     
     func test1(){
	      a := []int{1, 2 ,3, 4}
	      a[1] = 100
	      fmt.Println(a)//发生了逃逸，因为println()里面的参数类型是interface{}
     }
     
 3）在自定义的结构体中，如果实例化结构体返回指针类型的结构体，此时就会发生逃逸，所以，如果能不返回结构体指针就不返回
    
    type Student struct {
	      Id int
    }
    func NewStudent() *Student {
	      return &Student{101}
    }
```
* GO实现一个简单的set
```
代码如下：
  
  type Empty struct {}
  type Set map[interface{}]Empty
  func(this Set) Add(vs ...interface{}) {
	    for _, v := range vs {
		    this[v] = Empty{}
	    }
   }
  func NewSet() Set {
	  return make(map[interface{}]Empty)
  }
```
