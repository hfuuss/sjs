### 深拷贝
```
var obj = {
  name: 'zhangsan',
  age: 12,
}
console.log(obj.name);
boj.name = obj = 'lisi';
//想要结果为 张三;结果输出 lisi

//用以下语句进行深拷贝既可以解决 -----来自<你不懂的JavaScript(上卷)>
console.log(JSON.parse(JSON.stringfy(obj)))
``` 
### 函数和函数变量
```
b();
a();
function b(){
document.write("aa");
}
var a=function(){
document.write("123");
}
```
这样再运行一下就有区别了
function b(){} 为函数声明，程序运行前就已存在；var a = function(){} 为函数表达式，属于按顺序执行，所以a为undefined

### 函数到底是否执行？
```
//1
function f() {
  console.log('执行了！')
}

var generator = f();//'执行了！'


//2
function f2() {
  console.log('执行了！')
}

var generator2 = f2;//不执行

generator2();//执行
```

###  星号函数的异同


```
function* f() {
  console.log('执行了！')
}

var generator = f();

setTimeout(function () {
  generator.next()
}, 2000);
```
上面代码中，函数f如果是普通函数，在为变量generator赋值时就会执行。但是，函数f是一个 Generator 函数，就变成只有调用next方法时，函数f才会执行。