#### Rust 入门到放弃

* 安装MSYS2
```
1.介绍
  集成了pacman和Mingw-w64的Cygwin升级版, 提供了bash shell等linux环境、版本控制软件（git/hg）
  
  和MinGW-w64 工具链

2. 下载地址
    https://mirrors.tuna.tsinghua.edu.cn/msys2/distrib/x86_64/
    
3. 修改配置信息
   用编辑器打开msys2_shell.cmd
   
   把set MSYS2_PATH_TYPE=inherit前面的rem去掉
   
4. 启动 msys2_shell.cmd
```
* window 安装
```
1. 新建目录rust
    1）在rust目录下，新建cargo目录，rustup目录
    
    2）添加环境变量
      CARGO_HOME d:\rust\cargo
      RUSTUP_HOME  d:\rust\rustup
    
    3）在path环境变量中加入：%CARGO_HOME%\bin
    
    4）设置源环境变量
      RUSTUP_DIST_SERVER : https://mirrors.ustc.edu.cn/rust-static
      RUSTUP_UPDATE_ROOT : https://mirrors.ustc.edu.cn/rust-static/rustup
      
    5）把MSYS2切换到rust目录下，执行./rustup-init.exe
    
    6) 选择：自定义安装2
    
    7）host输入：
      x86_64-pc-windows-gnu
  
    8）其他默认，在是否修改path环境变量时，选择：no
    
    9）卸载已经安装的rust
      rustup self uninstall
```
* 基本命令的使用
```
1. 查看版本
  rustc -V
  cargo -V
  rustup -V
  
2. 安装rust的源码库
   rustup component  add rust-src

3. 新建项目
   cargo new mypros
4. 编译并运行文件
   cargo build && cargo run
```
* 变量
```
1. 变量的默认类型是不可变的，如果要变成可变，加mut关键字

2. 变量的隐藏特性，如果定义了两个重名的变量，后面定义的变量才会有效，而前面的会失效，就像隐藏起来了一样
```
* String的入门
```
1. str ，存在于栈中，性能高。通常以&str的方式引用。

2. String,分配在堆中,可增长、可变、有所有权、UTF-8 编码的字符串类型
   String::new()
   String::from
   
3. String类型在离开作用域的时候会调用drop方法进行回收
```
3. RUST常见符号
```
unspecified -> Display

? -> Debug

o -> Octal //8进制

x -> LowerHex  //16进制

X -> UpperHex

p -> Pointer

b -> Binary //二进制

```
* String类型在堆栈中的存储

![](https://github.com/Yangliangfeng/GO/raw/master/images/String_struct.png)

```
String 类型在栈中存放的是：ptr指针地址，len长度，capacity容量

在堆中存放的是内容

rust查看指针的地址：println!("{:p}", name.as_ptr())

```
* 引用
```
在同一时间内，不可变引用与可变引用不能共存。。。。
```
* rust的内存回收机制
```
1. rust是通过所有权机制来管理内存，编译器在编译会根据所有权规则来对内存的使用进行检查

2. 堆和栈
   1）编译的时候数据类型大小固定的，就是分配在栈上
   
   2） 编译的时候数据类型大小不固定的，就是分配在堆上
```
