#### 解析 URL Params 为对象

```javascript
function parseParam(){
    //通过window.search获取URL参数
    const str = window.location.search;
    //去除首字符'?'
    str = str.substring(1, str.length);
    //以'&'分割字符串，返回数组
    const arr = str.split(&);
	var obj = {};
    //sasd
	arr.forEach( param => {
        if(/=/.test(param)){//处理有value的参数
            let [key, val] = param.split("=");//分割key和value
            val = decodeURIComponent(val);//解码
            val = /^\d+$/.test(val) ? parseFloat(val) : val;//判断是否转为数字
            if(obj.hasOwnProperty(key)){//如果对象已有该key，则转化为数组并添加一个值
                obj[key] = [].concat(obj[key], val);
            }else{//如果对象没有该key，则创建key并设置值为true
                obj[key] = val;
            }
        }else{//处理没有value的参数
            obj[param] = true;
        }
    })
}
```

