# Error handling in Node.js

Links :

- https://nodejs.dev/learn/error-handling-in-nodejs
- http://thecodebarbarian.com/unhandled-promise-rejections-in-node.js.html
- https://medium.com/dailyjs/how-to-prevent-your-node-js-process-from-crashing-5d40247b8ab2

How to caught global event uncaught exception

```
process.on('uncaughtException', err => {
  console.error('There was an uncaught error', err);
  process.exit(1); // mandatory (as per the Node.js docs)
});

process.on('unhandledRejection', error => {
  console.log('unhandledRejection', error);
});
```

It's always better to handle promise rejection. You can wrap it inside  `try/catch`.

Await handles promise rejections for you, so unhandled promise rejections go away.

## Building error constructor in server

- https://levelup.gitconnected.com/the-definite-guide-to-handling-errors-gracefully-in-javascript-58424d9c60e6
