# beego 框架
* 安装 Beego 和 Bee 的开发工具

```
gopm get -g -v github.com/astaxie/beego
gopm get -g -v github.com/beego/bee
```
beege和bee是两个概念。beego是框架，bee是工具，是命令
```
go build github.com\beego\bee
```
会在当前dir下面生成 bee.exe 文件，把这个文件 剪切到 GOROOT/bin 下面去

* bee 工具的使用

在命令行输入bee

![](https://github.com/Yangliangfeng/GO/raw/master/images/12.jpg)

如果出现这种提示就说明你的 bee 安装成功过

在GOPATH/src下面运行 bee new 项目名称。比如我的项目名称就叫 b_project

![](https://github.com/Yangliangfeng/GO/raw/master/images/13.jpg)

可以运行bee run 运行一下这个项目

![](https://github.com/Yangliangfeng/GO/raw/master/images/14.jpg)

在浏览器中输入 http://127.0.0.1:8080/

![](https://github.com/Yangliangfeng/GO/raw/master/images/15.jpg)

ok。如果出现这种提示就说明 beego 已经 install 成功了
