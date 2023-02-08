# Node/JS

## 1. ES6

- Block scoping
- String literal
- Class
- Promise
	- async-await
	- Promise.resolve
	- Promise.all
	- Promise.race

```javascript

promise
  .then((result) => { ··· })
  .catch((error) => { ··· })
  .finally(() => { // logic independent of success/error })
  
``` 	

- Destructuring  
- Spread
- Arrow
- Generator: able to stop and resume function

```javascript
function* generatorFunc() {
    yield 0
    console.log('something')
    yield 1
}

const generator = generatorFunc()
console.log(generator.next())  // { value: 0, done: false }
console.log(generator.next())  // something 
                                                                        // { value: 1, done: false }
console.log(generator.next())  // { value: undefined, done: true }
```


## 2. Internal work of JS

- V8 engine comprise of two component:
	- Host env
	- V8 Engine

- Host env:
	- Host env comprise of multiple component:
		1. Call Stack
		2. Event Loop
		3. Heap
		4. Web API
		5. Call Back queue 

![](img/js_1.png)


- How it works:
	- When new event start, for example **fetch data from backend**, it push event to call stack first.
	- **Event Loop** pick up this event and start process it.
	- The fetch data event will process end send another request to **Web API**, and it will be pop out from the call stack. This make process do not stuck at point.
	- Web API make call to BE server and wait for return.
	- BE return data, Web API push it to **Callback Queue**.
	- Event Loop pick up that data from call back queue and process it.

- V8 Engine have these component:
	- Javascript Core
	- GC
	- Coroutine

 
## 3. JS concept

### Closures and Higher-order Functions

- **Closure**: When we create a function inside another function in JavaScript, the inner function has access to the scope of the outer function as well as its own.

- **Higher-order Functions**: function that return other function is higher-order function.

```javascript

function throttle(fn, milliseconds) {
  let lastCallTime;

  return function() {
    let nowTime = Date.now();

    if(!lastCallTime || lastCallTime < nowTime - milliseconds) {
      lastCallTime = nowTime;
      fn();
    }
  };
}

let helloToptalThrottled = throttle(helloToptal, 1000);
setInterval(helloToptalThrottled, 10);

```

- **The Rest and Spread Operators**

```javascript

// Spread operator

function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a);
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");

// a, "one"
// b, "two"
// manyMoreArgs, ["three", "four", "five", "six"] <-- an array

Math.max(...[1,3,5]) // output: 5

```

## 4. Node JS Internal

- Node JS Platform uses “Single Threaded Event Loop” architecture to handle multiple concurrent clients constrast to other framework who use multi-thread model.
- Drawbacks of multi-thread model:
	- Handling more and more concurrent client’s request is bit tough.
	- Waste time blocking IO
	- Threads increase will increase size of memory

## 5. Express 
### 5.1 Core feature of express:

- Middleware:
	- Logging
	- Authentication
	- Authorization
	- JSON parser 
- Routing
- Subapplication: using router
- Conveniences

### 5.3 Middleware

- Express middleware:
	- Rate limit
	- Helmet
	- Cookie-parser
	- Response-time

### 5.4 Routing

- URL param **/test/:who request.params**
- URL query **https://stackabuse.com/?page=2&limit=3 req.query**
- Router can be use to split up application

```typescript
// Main route
app.use('/api', MainRouter);

```

### 5.5 HTTPs

```sh
openssl genrsa -out privatekey.pem 1024
openssl req -new -key privatekey.pem -out request.pem
```

```javascript

var express = require("express");
var https = require("https");
var fs = require("fs");
var app = express();

// ... define your app ...

var httpsOptions = {
	key: fs.readFileSync("path/to/private/key.pem"),
	cert: fs.readFileSync("path/to/certificate.pem")
};

http.createServer(app)
	.listen(80);

https.createServer(httpsOptions, app)
	.listen(443);

```

### 5.6 API version

```javascript

var express = require("express");
var apiVersion1 = require("./api1.js");
var app = express();

app.use("/v1", apiVersion1);

app.listen(3000, function() {
    console.log("App started on port 3000");
});

```


## 6. Webpack build tool

## 7. Node JS Unit Test





