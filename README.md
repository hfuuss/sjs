# 说明
看到一篇文章，打造的很不错。拿来主义，然后把自己博客里面的那几段代码加进来，做一个简单的js库。时时刻刻丰富。
打造一个自己日常生活中遇到的js一些坑，以及可以复用的一些代码。

## 封装成形
```
//这样的话，封装了几个操作，就增加了几个全局函数，污染了全局变量，在开发中应该尽量避免全局变量。不说别的，如果一个项目，几个人开发，很有可能会造成命名的冲突。
function setUrlPrmt(obj){..}
function getUrlPrmt(url){..}
function upsetArr(obj){..}
//所以，建议的封装姿势是
var myJS={
    setUrlPrmt:function(obj){..},
    getUrlPrmt:function(url){..},
    upsetArr:function(arr){..},
}
```
第二种方式(公司可能不让)
```
String.prototype.trim=function(type){
    switch (type){
        case 1:return this.replace(/\s+/g,"");
        case 2:return this.replace(/(^\s*)|(\s*$)/g, "");
        case 3:return this.replace(/(^\s*)/g, "");
        case 4:return this.replace(/(\s*$)/g, "");
        default:return this;
    }
}
//'  12345 6 8 96  '.trim(1)
//"123456896"
//比这样trim('  12345 6 8 96  ',1)调用方便。
//但是，这样是不推荐的做法，这样就污染了原生对象String,别人创建的String也会被污染，造成不必要的开销。
//更可怕的是，万一自己命名的跟原生的方法重名了，就被覆盖原来的方法了
//String.prototype.substr=function(){console.log('asdasd')}  
//'asdasdwe46546'.substr()
//asdasd 
//substr方法有什么作用，大家应该知道，不知道的可以去w3c看下
```