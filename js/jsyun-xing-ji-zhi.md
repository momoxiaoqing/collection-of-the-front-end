### js运行机制

settimeout，setImme产生的是宏任务，promise的then产生的是微任务，  
process.nexttick是在宏任务结束后微任务开始执行前的回调，  
js执行每次都是先执行一遍当前队列中的所有宏任务，再执行回调，再执行所有微任务，然后再执行下一轮。

每次找当前宏任务队列的时候，吧settimeout先遮住不看，剩下的，包括new Promise里的都是当前宏任务。![](/assets/js)

例子：  
`console.log('1');`

`setTimeout(function() {      
    console.log('2');      
    process.nextTick(function() {      
        console.log('3');      
    })      
    new Promise(function(resolve) {      
        console.log('4');      
        resolve();      
    }).then(function() {      
        console.log('5')      
    })      
})      
process.nextTick(function() {      
    console.log('6');      
})      
new Promise(function(resolve) {      
    console.log('7');      
    resolve();      
}).then(function() {      
    console.log('8')      
})`

`setTimeout(function() {      
    console.log('9');      
    process.nextTick(function() {      
        console.log('10');      
    })      
    new Promise(function(resolve) {      
        console.log('11');      
        resolve();      
    }).then(function() {      
        console.log('12')      
    })      
})`

