#### 实现instanceOf

```javascript
function instance_of(L, R){// L 为要判断的对象，R 为目标类型
    //取 R 的显示原型
    var O = R.prototype;
    //取 L 的隐式原型
    L = L.__proto__;
    while(true){
        if(L === null) return false;
        if(L === O) return true;
        //按原型链查找
        L = L.__proto__;
    }
}
```

