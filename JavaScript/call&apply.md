#### call

call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法。

- 将函数设为对象的属性
- 执行&删除这个函数
- 指定this到函数并传入给定参数执行函数
- 如果不传入参数，默认指向为 window

```javascript
Function.prototype.mycall = function(context){
    var context = context || window;//当传入参数为null，环境指向window
    context.fn = this;//将当前函数作为传入对象的属性
    let args = [];
    for(let i = 1, len = arguments.length; i < len; i++){
        args.push(arguments[i]);
    }
    let result = context.fn(...args);//context环境下执行当前函数
    delete context.fn;//执行完后删除
    return result;
}
```



#### apply

apply接收的参数为数组，call则为参数列表，即：

```javascript
function.apply(thisObj[, argArray])

function.call(thisObj[, arg1[, arg2[, [,...argN]]]])
```

```javascript
Function.prototype.myapply = function(context, arr){
    var context = context || window;
    context.fn = this;
    var result = null;
    if(!arr){
        result = context.fn();
    }else{
        var args = [];
        for(let i = 1, len = arr.length; i < len; i++){
        	args.push("arr[" + i + "]");
    	}
        result = eval("context.fn(" + args + ")");
    }
    delete context.fn;
    return result;
}
```

