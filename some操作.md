```
//cookie
//设置cookie
function setCookie(name,value,iDay){
    var oDate=new Date();
    oDate.setDate(oDate.getDate()+iDay);
    document.cookie=name+'='+value+';expires='+oDate;
}
//获取cookie
function getCookie(name){
    var arr=document.cookie.split('; ');
    for(var i=0;i<arr.length;i++){
        var arr2=arr[i].split('=');
        if(arr2[0]==name)
        {
            return arr2[1];
        }
    }
    return '';
}
//删除cookie
function removeCookie(name){
    setCookie(name,1,-1);
}
```

### 清除对象中值为空的属性
```
//filterParams({a:"",b:null,c:"010",d:123})
//Object {c: "010", d: 123}
function filterParams(obj){
    let _newPar = {};
    for (let key in obj) {
        if ((obj[key] === 0 || obj[key]) && obj[key].toString().replace(/(^\s*)|(\s*$)/g, '') !== '') {
            _newPar[key] = obj[key];
        }
    }
    return _newPar;
}

```

### 现金额大写转换函数
```
//upDigit(168752632)
//"人民币壹亿陆仟捌佰柒拾伍万贰仟陆佰叁拾贰元整"
//upDigit(1682)
//"人民币壹仟陆佰捌拾贰元整"
//upDigit(-1693)
//"欠人民币壹仟陆佰玖拾叁元整"
function upDigit(n)   
{  
    var fraction = ['角', '分','厘'];  
    var digit = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'];  
    var unit = [ ['元', '万', '亿'], ['', '拾', '佰', '仟']  ];  
    var head = n < 0? '欠人民币': '人民币';  
    n = Math.abs(n);  
    var s = '';  
    for (var i = 0; i < fraction.length; i++)   
    {
        s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, ''); 
    } 
    s = s || '整';  
    n = Math.floor(n);  
    for (var i = 0; i < unit[0].length && n > 0; i++)   
    {  
        var p = '';  
        for (var j = 0; j < unit[1].length && n > 0; j++)   
        {  
            p = digit[n % 10] + unit[1][j] + p; 
            n = Math.floor(n / 10);
        }
        //s = p.replace(/(零.)*零$/, '').replace(/^$/, '零')+ unit[0][i] + s; 
        s = p+ unit[0][i] + s;
    }
    return head + s.replace(/(零.)*零元/, '元').replace(/(零.)+/g, '零').replace(/^整$/, '零元整');
} 
```

### 获取，设置url参数
```
//获取url参数
//getUrlPrmt('segmentfault.com/write?draftId=122000011938')
//Object{draftId: "122000011938"}
function getUrlPrmt(url) {
    url = url ? url : window.location.href;
    let _pa = url.substring(url.indexOf('?') + 1), _arrS = _pa.split('&'), _rs = {};
    for (let i = 0, _len = _arrS.length; i < _len; i++) {
        let pos = _arrS[i].indexOf('=');
        if (pos == -1) {
            continue;
        }
        let name = _arrS[i].substring(0, pos), value = window.decodeURIComponent(_arrS[i].substring(pos + 1));
        _rs[name] = value;
    }
    return _rs;
}
//设置url参数
//setUrlPrmt({'a':1,'b':2})
//a=1&b=2
function setUrlPrmt(obj) {
    let _rs = [];
    for (let p in obj) {
        if (obj[p] != null && obj[p] != '') {
            _rs.push(p + '=' + obj[p])
        }
    }
    return _rs.join('&');
}
```

### 随机返回一个范围的数字
```
function randomNumber(n1,n2){
    //randomNumber(5,10)
    //返回5-10的随机整数，包括5，10
    if(arguments.length===2){
        return Math.round(n1+Math.random()*(n2-n1));
    }
    //randomNumber(10)
    //返回0-10的随机整数，包括0，10
    else if(arguments.length===1){
        return Math.round(Math.random()*n1)
    }
    //randomNumber()
    //返回0-255的随机整数，包括0，255
    else{
        return Math.round(Math.random()*255)
    }  
}
```
### 随进产生颜色
```
function randomColor(){
    //randomNumber是上面定义的函数
    //写法1
    return 'rgb(' + randomNumber(255) + ',' + randomNumber(255) + ',' + randomNumber(255) + ')';
    //写法2
    return '#'+Math.random().toString(16).substring(2).substr(0,6);
    //写法3
    var color='#';
    for(var i=0;i<6;i++){
        color+='0123456789abcdef'[randomNumber(15)];
    }
    return color;
}
//这种写法，偶尔会有问题。大家得注意哦
//Math.floor(Math.random()*0xffffff).toString(16);
```

### Date日期时间部分
```
//到某一个时间的倒计时
//getEndTime('2017/7/22 16:0:0')
//"剩余时间6天 2小时 28 分钟20 秒"
function getEndTime(endTime){
    var startDate=new Date();  //开始时间，当前时间
    var endDate=new Date(endTime); //结束时间，需传入时间参数
    var t=endDate.getTime()-startDate.getTime();  //时间差的毫秒数
    var d=0,h=0,m=0,s=0;
    if(t>=0){
      d=Math.floor(t/1000/3600/24);
      h=Math.floor(t/1000/60/60%24);
      m=Math.floor(t/1000/60%60);
      s=Math.floor(t/1000%60);
    } 
    return "剩余时间"+d+"天 "+h+"小时 "+m+" 分钟"+s+" 秒";
}
```
### 适配rem
```
function getFontSize(){
    var doc=document,win=window;
    var docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
    recalc = function () {
        var clientWidth = docEl.clientWidth;
        if (!clientWidth) return;
        //如果屏幕大于750（750是根据我效果图设置的，具体数值参考效果图），就设置clientWidth=750，防止font-size会超过100px
        if(clientWidth>750){clientWidth=750}
        //设置根元素font-size大小
        docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
    };
    //屏幕大小改变，或者横竖屏切换时，触发函数
    win.addEventListener(resizeEvt, recalc, false);
    //文档加载完成时，触发函数
    doc.addEventListener('DOMContentLoaded', recalc, false);
}
//使用方式很简单，比如效果图上，有张图片。宽高都是100px;
//样式写法就是
img{
    width:1rem;
    height:1rem;
}
//这样的设置，比如在屏幕宽度大于等于750px设备上，1rem=100px；图片显示就是宽高都是100px
//比如在iphone6(屏幕宽度：375)上，375/750*100=50px;就是1rem=50px;图片显示就是宽高都是50px;
```







