# File system

Some of the most commonly used methods fs exposes are:

  - `fs.readFile` -- Read data from a file
  - `fs.writeFile` -- Write data to a file, replaces the file if it already exists
  - `fs.watchFile` -- Get notified of changes to a file
  - `fs.appendFile` -- Append data to a file

`__dirname` directory of where my code is running

Using `path` to concat path are recommended it will take care all of file path type in every OS, so something doesn't have to be breaking when you're using Windows.

## Asynchronous v.s. Synchronous `fs` methods

By default, the functions provided by fs are asynchronous and callback-based. But many of these functions have synchronous versions as well, such as `readFileSync` and `writeFileSync`. Typically, all I/O operations in Node.js are done asynchronously to avoid blocking the event loop and making your program unresponsive while I/O heavy tasks run.

## When can't we rely on the filesystem?

Depending on where our code is running, we don't always have access to a persistent filesystem. When developing locally on your own machine, you can easily persist files and access them again later. But in certain environments in the cloud, we don't have access to a persistent filesystem.

## Reading

- https://nodejs.org/dist/latest-v12.x/docs/api/fs.html
- https://heynode.com/tutorial/readwrite-json-files-nodejs/
