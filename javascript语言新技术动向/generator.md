# Generator

## 定义
Generator是ES6标准引入的新的数据类型。它虽然看上去像是一个函数，但是
它和普通函数的区别在于普通函数只能返回一次，而它能够返回多次。

下面我们可以通过两段**定义**来简单的看看函数和generator的区别

这是函数的定义过程。
```javascript
    function gen(x){
        return x;
    }
    var y = gen(x);
```
这是generator的定义过程，不同的是在function后面加了一个*，并且在原有的
return的基础上又加上了一个yield的返回方式，并且yield可以yield可以返回
多次。
```javascript
    function* gen(x){
        yield x;
        yield x + 1;
        retuen x + 2;
    }
```

## 例子

很多时候我们需要返回一组数据的时候，用函数来写的话就要定义一个数组，然后
再一次性的返回过来，用generator的话就可以可以一次返回一个数，不断返回多
次。
以斐波那契数列为例：

我们利用generator写了一个用于输出斐波那契数列。
```javascript
    function* gen(max){
        var
            t,
            a=0;
            b=1;
            n=1;
            while (n<max){
                yield a;
                t=a+b;
                a=b;
                b=t;
                n ++;
            }
            return a;
            
    }
```
因为generator和调用函数是不一样的，不能够直接的调用，有以下两种方法：

* next()方法
* for...of方法

通过next()方法，我们可以队输出进行控制，在调用函数的方法中我们只能够
建立一个数组然后一次性的蒋我们想要的东西全部输出，但是用了generator
之后我们就可以通过next()方法来一个个将数列中的数字输出，并且我们还能
够在返回一个结果之后在做一些其他的事情。因为，**next()方法在执行generator
代码的时候，每次执行完yield之后都会返回对象`{value: x, done: true/false}`
然后暂停下来，给你空间去控制是做其他事还是继续返回数字**，这就是generator
与调用函数不同的地方。

```javascript
    var g = gen(5);
    console.log("hello");//hello
    console.log(g.next());//{ value: 0, done: false }
    console.log(g.next());//{ value: 1, done: false }
    console.log(g.next());//{ value: 1, done: false }
    console.log(g.next());//2
    console.log(g.next().value);{ value: 3, done: true }
```

for...of方法，和调用函数也没什么特别不一样的地方，也是通过循环来输出。

```javascript
    for (var x of gen(5)) {
            console.log(x); // 依次输出0, 1, 1, 2, 3
        }
```
## 一些generator的方法

* generator.return

在generator中，利用next()方法可以返回，但是使用return返回之后就不能
够在使用next()返回了。

代码如下:

```javascript
function* gen() { 
  yield 1;
  yield 2;
  yield 3;
}

var g = gen();

g.next();        // { value: 1, done: false }
g.return('foo'); // { value: "foo", done: true }
g.next();        // { value: undefined, done: true }
```
* generator.throw

throw()这个方法主要就是用来捕获错误的，就和以前的try...catch一样。

代码如下：

```javascript
function* gen() {
  while(true) {
    try {
       yield 42;
    } catch(e) {
      console.log('Error caught!');
    }
  }
}

var g = gen();
g.next();
// { value: 42, done: false }
g.throw(new Error('Something went wrong'));
// "Error caught!"
// { value: 42, done: false }
```