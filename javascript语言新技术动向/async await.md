# async await

Async是一个实用模块，它为使用异步JavaScript提供了直接、强大的功能。
虽然最初是为使用节点而设计的。
而await操作符用于等待一个异步函数返回的承诺。
所以在ES7中为了解决javascript的异步问题中，提出了async和await。

在提出async和await之前，在javascript中处理异步问题的主要途径就是通过Promise
，可以将嵌套的回调函数展平，但是写代码和阅读依然有额外的负担。

下面是一个通过async和await来实现sleep3秒的代码
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
