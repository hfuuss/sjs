  
 //字符数组互转
String.prototype.toArr = function() {
	  return this.split(',')//可以替换
};

var arr = ['1','24','3','5','1','2','3','4']
var str = arr.toString()//1,24,3,5,1,2,3,4
console.log(str)
console.log(str.toArr())//[ '1', '24', '3', '5', '1', '2', '3', '4' ]
```