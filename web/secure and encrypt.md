## 安全和加密

```
学习网站: https://github.com/astaxie/build-web-application-with-golang/blob/master/zh/preface.md

对于用户的输入数据，在对其进行验证之前都应该将其视为不安全的数据。如果直接把这些不安全的数据输出到客户端，

就可能造成跨站脚本攻击(XSS)的问题；如果把不安全的数据用于数据库查询，那么就可能造成SQL注入问题。
```