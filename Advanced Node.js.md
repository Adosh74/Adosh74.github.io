# The internals of `Node`

## Is `Node` a single thread?

not truly, but it is a single thread in the sense that it has only one thread per process.

### Example

```js
const crypto = require('crypto')

const start = Date.now()

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('1:', Date.now() - start);
})
```

This is a simple example of `Node` code that makes use of the `crypto` module to hash a string.

when we run this code, it will take some time to execute, and then it will print out the time it took to execute the function.

till this moment doesn't seem to be anything special, but if we run the same function again, we will see that it will take the same amount of time to execute the function.

```js
const crypto = require('crypto')

const start = Date.now()

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('1:', Date.now() - start);
})

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('2:', Date.now() - start);
})
```

now we will see the two functions will take the same amount of time to execute, and this is because the **thread pool**.

### Thread pool

thread pool is a set of threads that are available to execute tasks.

### Another example

```js
const crypto = require('crypto')


const start = Date.now()

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('1:', Date.now() - start);
})

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('2:', Date.now() - start);
})

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('3:', Date.now() - start);
})

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('4:', Date.now() - start);
})

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('5:', Date.now() - start);
})
```

when we run this code, we will see that the first four functions will take the same amount of time to execute, and the fifth function will take a little bit longer to execute.

this is because the thread pool has only four threads by default, and the fifth function will wait for one of the threads to be available to execute it.

### Conclusion

when we run the code, `Node` will start up a thread pool with four threads by default, and these threads are available to execute code inside of our `Node` application.

when we call `crypto.pbkdf2` function, it will take the function and pass it off to one of the threads in the thread pool, and that thread will then execute the function.

when the function is done executing, it will then pass the result back to the `Node` event loop, and then `Node` will call the callback function that we passed to `crypto.pbkdf2` function.

### Changing the thread pool size

we can change the size of the thread pool by using `process.env.UV_THREADPOOL_SIZE` environment variable.

```js
process.env.UV_THREADPOOL_SIZE = 2
```

if use windows, we can use `set` command to set the environment variable when we run the code.

```bash
set UV_THREADPOOL_SIZE=2 && node <filename>.js
```

now we will see that the first two functions will take the same amount of time to execute, and the third function will wait for one of the threads to be available to execute it.

### Libuv OS Delegation

`Node` uses `libuv` to handle the thread pool, and `libuv` uses `OS` delegation to handle the thread pool.

`OS` delegation means that `libuv` will delegate the task of creating threads to the `OS`.

### Example

```js
const https = require('https');

const start = Date.now();

const doRequest = () => {
    https.request('https://www.google.com', res => {
        res.on('data', () => {})
    
        res.on('end', () => {
            console.log('time', Date.now() - start);
        })
    }).end()
}

doRequest()
doRequest()
doRequest()
doRequest()
doRequest()
doRequest()
```

when we run this code, we will see all the requests will take the same amount of time to execute.

#### Conclusion

`Libuv` Delegates the task of creating threads to the `OS`, and the `OS` will create threads to handle the requests.

# nodejs #tools
