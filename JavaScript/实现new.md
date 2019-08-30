#### new

> new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象类型之一

1. 用new Object() 的方式新建了一个对象 obj
2. 取出第一个参数，就是我们要传入的构造函数。此外因为 shift 会修改原数组，所以 arguments 会被去除第一个参数
3. 将 obj 的原型指向构造函数，这样 obj 就可以访问到构造函数原型中的属性
4. 使用 apply，改变构造函数 this 的指向到新建的对象，这样 obj 就可以访问到构造函数中的属性
5. 如果函数没有返回对象类型Object(包含Functoin, Array, Date, RegExg, Error)，那么new表达式中的函数调用将返回该对象引用；如果是一个对象，我们就返回这个对象

```javascript
function ObjectFactory(){
    var obj = new Object();
    Constructor = [].shift.call(arguments);
    obj.__proto__ = Constructor.prototype;
    var ret = Constructor.apply(obj, arguments);
    return typeof ret === 'object' ? ret : obj;
};
```

