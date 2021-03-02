# 1.今天遇到一个apache重定向的问题

```
    目标路由是：
          domain/orderInfo&id=123
    期望路由是：
          domain/?app=order/orderinfo&id=123
          
 ```
          
# 解决方式1：
    RewriteRule ^orderInfo$ /?app=order/orderinfo [R=permanent,QSA]
    
    [R=permanent,QSA]这个选项能保证，参数会按照query_string的方式追加到路由后面，使用起来很方便
    QSA：query string append
         本来重写url之后，apache会丢弃之前的query_string,使用新生成的query_string,使用QSA参数之后，会把之前的query_string追加到新的query_string
      之后。
  
# 解决方式2：

```
    修改路由规则，可以把参数当成路由来处理
    RewriteRule ^orderInfo/(.+)$ /?app=order/orderInfo&id=$1
    
    目标路由是：
          domain/orderInfo/123
    期望路由是：
          domain/?app=order/orderInfo&id=123
          
    同样可以达到效果!
```
