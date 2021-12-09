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

# 2. Advanced Streams

A stream is an abstract interface for working with streaming data in Node.js. The stream module provides an API for implementing the stream interface.

There are many stream objects provided by Node.js. For instance, a request to an HTTP server and process.stdout are both stream instances.

Streams can be readable, writable, or both. All streams are instances of EventEmitter.

To access the stream module: `const stream = require('stream');`

The stream module is useful for creating new types of stream instances. It is usually not necessary to use the stream module to consume streams.

[Document about Node.js Stream](https://nodejs.org/docs/latest-v16.x/api/stream.html)

## Why streams

We have Scavenge, and we have Mark-sweep.

If you execute...

`node --trace_gc buffer-vs-stream/stream.js (-40mb in memory)`

`node --trace_gc buffer-vs-stream/buffer.js`

...you're gonna notice that we have actually, a lot of these Mark-sweeps in buffer. So this Mark-sweep is actually a much bigger deal because Mark-sweep is gonna stop your node process to clean up a lot of garbage. The Scavenge doesn't clean up as much garbage, and stream use only this in this example.

[buffer vs stream](https://github.com/laissonsilveira/nodejs-advanced/blob/main/buffer-vs-stream)

## Readable streams

Readable streams are an abstraction for a source from which data is consumed.

Examples of Readable streams include:

* HTTP responses, on the client
* HTTP requests, on the server
* fs read streams
* zlib streams
* crypto streams
* TCP sockets
* child process stdout and stderr
* process.stdin

All Readable streams implement the interface defined by the stream.Readable class.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/readable-stream/index.js)

## Writable streams

Writable streams are an abstraction for a destination to which data is written.

Examples of Writable streams include:

* HTTP requests, on the client
* HTTP responses, on the server
* fs write streams
* zlib streams
* crypto streams
* TCP sockets
* child process stdin
* process.stdout, process.stderr

Some of these examples are actually Duplex streams that implement the Writable interface.

All Writable streams implement the interface defined by the stream.Writable class.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/writable-streams/index.js)

## Backpressure

For ex, can happen's when receive more readstream then can write, so...

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/backpressure/index.js)

## Piping streams

The `readable.pipe()` method attaches a Writable stream to the readable, causing it to switch automatically into flowing mode and push all of its data to the attached Writable. The flow of data will be automatically managed so that the destination Writable stream is not overwhelmed by a faster Readable stream.

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/pipe-streams/index.js)

## Duplex streams

Duplex streams are streams that implement both the Readable and Writable interfaces.

Examples of Duplex streams include:

* TCP sockets
* zlib streams
* crypto streams

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/duplex-streams/index.js)

## Transforms streams

Transform streams are Duplex streams where the output is in some way related to the input. Like all Duplex streams, Transform streams implement both the Readable and Writable interfaces.

Examples of Transform streams include:

* zlib streams
* crypto streams

[node js example](https://github.com/laissonsilveira/nodejs-advanced/blob/main/transform-streams/index.js)

# 3. HTTP Streaming

A web server that handles upload and download streams.

[web server files here](https://github.com/laissonsilveira/nodejs-advanced/blob/main/http-stream/index.js)

Upload: `http://localhost:3000`

Download: `http://localhost:3000/video`