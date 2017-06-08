# async await

Async是一个实用模块，它为使用异步JavaScript提供了直接、强大的功能。
虽然最初是为使用节点而设计的。
而await操作符用于等待一个异步函数返回的承诺。
所以在ES7中为了解决javascript的异步问题中，提出了async和await。

在提出async和await之前，在javascript中处理异步问题的主要途径就是通过Promise
，可以将嵌套的回调函数展平，但是写代码和阅读依然有额外的负担。

下面是一个通过async和await来实现sleep3秒的代码
## 例子

```javascript
    async function sleep(timeout) {
    return new Promise((resolve, reject) => {
        setTimeout(function() {
        resolve();
        }, timeout);
    });
    }

    (async function() {
    console.log('Do some thing, ' + new Date());
    await sleep(3000);
    console.log('Do other things, ' + new Date());
    })();
```


这段代码中，当它执行了第一个console的时候执行了await，（因为await要等待
sleep中返回的值之后才能够接下去执行代码。）这时候就进入了
sleep中，因为在等带settimeout运行3秒之后才从promise中跳出来，然后再
执行后一句console。所以这样就能够通过async和await实现3秒的停顿。

## 对比

因为当我们再使用promise 的时候会有很多的回调和使用then方法，所以我们通过一段代码
来看看promise是怎么样的情况，这样就能够体现async和await的优势。
```javascript
const f = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(123);
    }, 2000);
  });
};

const testAsync = () => {
  f().then((t) => {
    console.log(t);
  });
};

testAsync();
```
从这一段代码中可以看出promise用了很多的then方法，而使用then方法的问题在于，then方法内部是一个独立的
作用于，要是想共享数据，就要将部分数据暴露在最外层，在then内部赋值一次。，但是await是基于Promise
的，所以promise还是很有用的。

## 异常处理

通过try/catch，我们就可以捕获async/await中的错误，还有await中要
使用到的promise中reject的数据内容。
```javascript
const f = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(234);
    }, 2000);
  });
};

const testAsync = () => {
  try {
    const t = await f();
    console.log(t);
  } catch (err) {
    console.log(err);
  }
};

testAsync();
```
这就是通过将f方法中的resolve改成reject来让try/catch将数据抓住，
抓出来的数据就是promise中的234。

要是try/catch中有多个await的话，那么catch就只会返回第一个reject的值。
下面就是一个try/catch中有多个await的例子：
```javascript
const f1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(111);
    }, 2000);
  });
};

const f2 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(222);
    }, 3000);
  });
};

const testAsync = () => {
  try {
    const t1 = await f1();
    console.log(t1);
    const t2 = await f2();
    console.log(t2);
  } catch (err) {
    console.log(err);
  }
};

testAsync();
```
## 小结
总之async/await的作用就是解决了promise
中有比较多麻烦的then方法，然后基于promise解决了异步调用的的问题。