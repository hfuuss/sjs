```
//得到数组中元素最多的
var getElementUsedMost = function(arr){
    var hash = {};//利用hash 来记录次数
    var m = 0; //现在的最大次数
    var trueEl = null;//最大的元素
    // console.log(arr.length)
    for (var i = 0; i < arr.length; i++) {
    	if(arr[i] == '。' || arr[i] == '，') {continue }
    	// console.log(arr[i])
    	var el = arr[i];
        // console.log(arr[i])
        hash[el] === undefined ? hash[el] = 1 : (hash[el] ++);
        hash[el] >= m && (trueEl = el); 
    }

    return el;
};
```