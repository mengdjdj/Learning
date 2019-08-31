#### bind

> bind() 方法会创建一个新函数。当这个新函数被调用时，bind() 的第一个参数将作为它运行时的 this，之后的一序列参数将会在传递的实参前传入作为它的参数。

1. 返回一个函数
2. 可以传入参数

```javascript
Function.prototype.mybind = function(context){
    
    if(typeof this !== 'function'){
        throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }
    
    var self = this;
    //获取mybind函数第二个参数到最后一个参数
    var args = Array.prototype.slice.call(arguments, 1);
    
    var fNOP = function(){};
    
    var fBound = function(){
        //此处arguments为传入fBound的参数
        var bindArgs = Array.prototype.slice.call(arguments);
        //当作为构造函数，this指向实例，将绑定函数的this指向该实例
        //但作为普通函数，this指向window，将绑定函数的this指向context
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }
    //直接修改fBound.prototype的时候，也会直接修改绑定函数的prototype
    //可通过一个空函数fNOP来进行中转
    fNOP.prototype = this.prototype;
    //修改返回函数的prototype为绑定函数的prototype，实例就可以继承绑定函数的原型中的值
    fBound.prototype = new fNOP();
    return fBound;
}
```

