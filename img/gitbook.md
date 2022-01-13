

最近手头有些东西打算移植到gitbook方便自己查看，so，记录一下

#### 1、gitbook 脚手架安装

我这里有cnpm就用cnpm了，没有的还是用npm

```
cnpm install -g gitbook-cli
```

![image-20220113103138338](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113103138338.png)

#### 2、初始化 gitbook 

新建一个目录

```
gitbook init
```

在初始化的时候遇到以下问题

```
TypeError: cb.apply is not a function
    at /usr/local/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js:287:18
    at FSReqCallback.oncomplete (fs.js:184:5)
```

查找得知需要修改polyfills.js文件注释掉以下代码

```
fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)
```

![image-20220113104031250](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113104031250.png)

注释掉再执行gitbook的初始化后又出现了其它问题

```
TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be of type string or an instance of Buffer, TypedArray, or DataView. Received an instance of Promise
```



![image-20220113104305130](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113104305130.png)

查了一下，需要降级node.js的版本，我这里是14的版本，这里我们降回12.22.9版本，

地址：

https://nodejs.org/download/release/v12.22.9/node-v12.22.9-x64.msi

再次初始化gitbook，没问题了

![image-20220113104641835](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113104641835.png)



#### 3、启动gitbook

```
gitbook serve
```

![image-20220113105124400](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113105124400.png)

![image-20220113105202913](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113105202913.png)

#### 4、生成静态页面部署

```
gitbook build
```

![image-20220113105244304](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113105244304.png)

在目录下会生成_book目录，接下来部署就好
![image-20220113105318734](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220113105318734.png)