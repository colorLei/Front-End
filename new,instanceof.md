> new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象类型之一

```
function create() {
    // 创建一个空的对象
    let obj = new Object()
    // 获得构造函数
    let Con = [].shift.call(arguments)
    // 链接到原型
    obj.__proto__ = Con.prototype
    // 绑定 this，执行构造函数
    let result = Con.apply(obj, arguments)
    // 确保 new 出来的是个对象
    return typeof result === 'object' ? result : obj
}

```
> instanceof 可以正确的判断对象的类型，因为内部机制是通过判断对象的原型链中是不是能找到类型的 prototype。

```
function instanceof(left,right){
    // 获得类型的原型
    let prototype = right.prototype
    // 获得对象的原型
    left = left.__proto__
    while(true){
        //Object.prototype.__proto__ === null
        if(left === null)
            return false;
        if(left === right)
            return true;
        left = left.__proto__;
    }
}
```
