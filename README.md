# nodejs-advanced

Advanced techniques for asynchronous programming and data streaming in Node.js

## skills

* Asynchronous patterns
* Resolving and rejecting promises
* Sequential, parallel, and concurrent execution
* Working with readable and writeable streams
* Transforming streams
* HTTP streaming

# 1. Asynchronous Patterns

## Callback pattern

A callback is a block of instructions wrapped in a function so that it can be invoked when an asynchronous operation has completed.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/callback-pattern/index.js)

## Resolving and Rejecting promises

A promise is an object that can be used to represent the eventual completion of an a asynchronous operation.

The idea behind a promise is that we can wait for an asynchronous operation to complete, and then we can resolve the promise, or we can say that that operation has completed successfully with success or error.

[node js example - resolving](https://github.com/laissonsilveira/nodejs-advanced/blob/main/resolving-promises/index.js)

[node js example - resolving](https://github.com/laissonsilveira/nodejs-advanced/blob/main/rejecting-promises/index.js)

## The promisify function

If our callback functions are all structured like this, where they pass the error as the first argument to the callback, and they pass any additional values as second, or third, or fourth arguments to the callback, then we can quickly convert these functions into promises using a utility that ships with Node JS.

So promisify is a function that we can use to convert callback functions into promises. You can find it in the util package that ships with the Node JS core

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/promisify-function/index.js)

## Sequential execution

We introduced sequential execution with callbacks and we saw how nesting too many callbacks can create an anti-pattern called callback hell or the pyramid of doom.  So there is another way to handle things sequentially. And this time using Promises, we can see that our code is much cleaner, much easier to organize. Everything's happening in order. Let's go out to our terminal and give this a shot, node dot. So we can see that we're starting, waiting, things are happening sequentially, just like they were in the pyramid of doom, although it is much easier to manage this.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/sequential-execution/index.js)

## Sequential execution with async/await

JavaScript provides us a way to work with promises using code that appears synchronous, but is in fact asynchronous. The solution is async functions. Inside of an async function, you can await for a promise to complete.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/sequential-exec-async-await/index.js)

## Parallel execution

Promise.all vs Promise.race.

Both of the Promise methods receive an array of promises, however, you’ll want to choose one over the other depending on what you need to accomplish.

Promise.all accepts an array of promises, and will attempt to fulfill all of them. Exits early if just 1 promise gets rejected.
Promise.race also accepts an array of promises, but returns the first promise that is settled. A settled promise can either be resolved or rejected.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/parallel-execution/index.js)

## Concurrent tasks

Sometimes your promises may contain large tasks that eat a lot of resources or take a lot of time to process. Running everything at once can be too costly, but running one task at a time may take too long. A possible solution for this is to create a task queue that can run a specified number of tasks concurrently at the same time. Let's implement a promise queue that can run a specified number of promises at the same time.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/concurrent-tasks/index.js)