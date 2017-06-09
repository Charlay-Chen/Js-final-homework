# Reflect API

## reflect的意义
Reflect不是构造函数， 要使用的时候直接通过Reflect.method()调用而Reflect的作用主要是
配合Proxy来使用。
Reflect和Math对象一样，里面都是静态方法。

## 使用Reflect的几点好处

* 拥有更加有用的返回值。

例如Object.defineProperty和Reflect.defineProperty
```javascript
try {
Object.defineProperty(obj, name, desc);
// property defined successfully
} catch (e) {
// possible failure 
}
```
和
```javascript
if (Reflect.defineProperty(obj, name, desc)) {
// success
} else {
// failure
}
```
可以看出用reflect比较方便。
* 像函数一样操作

reflect它帮你直接封装好了，
例如Reflect.has,Reflect.set,Reflect.get,Reflect.deleteProperty

* 更加可靠的函数式执行方式

如果要执行一个函数f，并穿一组参数需要表示成

    f.apply(obj,args)
但是apply可能被用户定义成另一个apply，所以要写成

    Function.prototype.apply.call(f,obj,args)
但是这样的代码看着有感觉很复杂，有了reflect之后就可以写成

    Reflect.apply(f,obj,args)

## Reflect的一些方法

### Reflect.get & Reflect.set
```javascript
var x = { a: 5 };
var obj = new Proxy(x, {
    get(t, k, r) { return t.a + 'bar'; }
});

Reflect.set(x,'a',6)
Reflect.get(obj, 'foo'); // "6bar"
```
这里面的t代表的就是x这个对象，而k代表的是传进来的值也就是“foo”，而r在这段函数中还没有什么含义。
如果return的是k，那么结果就是foobar。
这里的set函数将x中的a的值更改成为了6，所以输出就成了6bar

### Reflect.has
Reflect.has方法允许您检查属性是否在对象中。 它的作用就像在运算符中一样。
```javascript
obj = new Proxy({}, {
  has(t, k) { return k.startsWith('door'); }
});
Reflect.has(obj, 'doorbell'); // true
Reflect.has(obj, 'dormitory'); // false
```
.has方法就是判断你传入的参数中有没有某一特定的元素。

### Reflect.defineProperty
Reflect.defineProperty方法能够更加精确的修改或者添加对象的属性，并且返回一个布尔值，指示属性
是否已经成功定义。因此，我们这里可以使用if...else块。
```javascript
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```



