
>call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法。 
```
const obj = {
    value:1
}
function getValue(name,age){
    console.log(name)
    console.log(age)
    console.log(this.value)
}

getValue.call(obj,'lei',18)
getValue.apply(obj,['lei',18])
const fn = getValue.bind(obj,'lei',18)

//call
Function.prototype.myCall = (context=window) => {
    // 给 context 添加一个属性
    // getValue.call(obj, 'yck', '24') => obj.fn = getValue
    context.fn = this;
    const args = [...arguments].slice(1)
    const result = context.fn(...args)
    delete context.fn
    return result;
}

//apply
Function.prototype.myApply = (context=window) => {
    context.fn = this;
    const result;
    // 需要判断是否存储第二个参数
    // 如果存在，就将第二个参数展开
    if(arguments[1]){
        result = context.fn(...arguments[1])
    }else{
        result = context.fn()
    }
    delete context.fn
    return result;
}
```

> bind() 方法会创建一个新函数。当这个新函数被调用时，bind() 的第一个参数将作为它运行时的 this，之后的一序列参数将会在传递的实参前传入作为它的参数。

```
// bind 和其他两个方法作用也是一致的，只是该方法会返回一个函数。并且我们可以通过 bind 实现柯里化。
Function.prototype.myBind = (context=window) => {
    if(typeof this !== 'function'){
        throw new TypeError('Error')
    }
    const _self = this;
    const args = [...arguments].slice(1);
    // 返回一个函数
    return function F() {
        // 因为返回了一个函数，我们可以 new F()，所以需要判断
        if(this instanceof F){
            return new _self(...args, ...arguments)
        }
        return _self.apply(context,args.concat(...arguments))
    }
}
```
