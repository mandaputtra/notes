# Process and OS module in Node.js

The process object (which is an instance of the `EventEmitter`) is a global variable that provides information on the currently running Node.js process.

```js
process.on('eventName', () => {
  //do something
})
```

## `uncaughtException`

```js
process.on('uncaughtException', (err) => {
  // here the 1 is a file descriptor for STDERR
  fs.writeSync(1, `Caught exception: ${err}\n`)
})
```

- if `uncaughtException` happens, your application is in an undefined state,
- recovering from `uncaughtException` is strongly discouraged, it is not safe to continue normal operation after it,
- the handler should only be used for synchronous cleanup of allocated resources,
- exceptions thrown in this handler are not caught, and the application will exit immediately,
- you should always monitor your process with an external tool, and restart it when needed (for example, when it crashes).

## `unhandledRejection`

The problem with not handling Promise rejections is the same as in the case of `uncaughtExceptions` – your Node.js process will be in an unknown state. What is even worse, is that it might cause file descriptor failure and memory leaks. Your best course of action in this scenario is to restart the Node.js process.

Unhandled promise

```
const fs = require('fs-extra')

fs.copy('/tmp/myfile', '/tmp/mynewfile')
  .then(() => console.log('success!'))
```

Handled promise

```
fs.copy('/tmp/myfile', '/tmp/mynewfile')
  .then(() => console.log('success!'))
  .catch(err => console.error(err))
```

## Node.js Signal Events

### `SIGTERM`

The `SIGTERM` signal is sent to a Node.js process to request its termination. Unlike the `SIGKILL` signal, it can be listened on or ignored by the process.

This act are required for gracefull shutdown

- The applications get notified to stop (received `SIGTERM`).
- The applications notify the load balancers that they aren’t ready for newer requests.
- The applications finish all the ongoing requests.
- Then, it releases all of the resources (like a database connection) correctly.
- The application exits with a “success” status code `(process.exit())`.

### `SIGUSR1`

By the POSIX standard, SIGUSR1 and SIGUSR2 can be used for user-defined conditions. Node.js chose to use this event to start the built-in debugger.

## Method values exposed by `process` module


### `process.cwd()`

Get current process directory

```js
$ node -e 'console.log(`Current directory: ${process.cwd()}`)'
Current directory: /Users/gergelyke/Development/risingstack/risingsite_v2
```

### `process.env`

Get OS environment variables

### `process.exit([code])`

This method tells the Node.js process to terminate the process synchronously with an exit status code. Important consequences of this call:

- it will force the process to exit as quickly as possible
- even is some `async` operation are in progress
- as writing to STDOUT and STDERR is `async `, some logs can be lost
- in most cases it is node recommended to use `process.exit()` - instead, you can shutdown by depleting the event loop (just close the running program, after everything are finished)

## Exit Code

- 1: Uncaught fatal exception
- 5: Fatal error in V8
- 9: Invalid argument

## OS Module

This module provides many functions that you can use to retrieve information from the underlying operating system and the computer the program runs on, and interact with it.

- https://nodejs.dev/en/learn/the-nodejs-os-module


