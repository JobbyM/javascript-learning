## 捕获js 文件报错位置方法

```javascript
(function(){
    var fn=function(o,url,line){
        var str='cntverror,';
        if(typeof o ==='object'){
            str+='url:'+o.filename+',line:'+o.lineno+',message:'+o.message;
        }else{
            str+='url:'+url+',line:'+line+',message:'+o;
        }
        console.log(str);
    }
    if(window.addEventListener){
        /*
        需要特别注意addEventListener的第三个参数，是否在捕获阶段处理
        这个参数，大多数时候用的都是false
        在这里，chrome、firefox也都可以用false
        但是opera用false时就无法处理error
        必须设置为true，在捕获阶段处理error，脚本才能正常运行
        */
        window.addEventListener("error",fn,true);
    }else if(window.attachEvent){
        //ie在这里表示无压力
        window.attachEvent("onerror",fn);
    }
})();
```
