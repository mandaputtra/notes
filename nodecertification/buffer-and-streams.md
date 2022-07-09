# Nodejs Streams

Stream are an interface for working with streaming data, image, text, objects, array, etc. It's like unix pipe

Stream data is a Buffer by default, unless the stream has been specifically configured to work with Objects.

Stream is a must when used to process large data. We will only deal with data a chunk at a time, and not fit all the data into memory.

Streams are composable, meaning they can be connected to and combined with other streams. The output of one stream can be used as the input for another stream, allowing us to combine streams into a pipeline through which data can flow between the various streams.

```js
stream.pipe(a).pipe(b) // Composable
```

## 4 Type of streams

- Readable: A source of input. Read data from `Readable` stream
- Writeable: Destination. Stream data into `Writable` stream. End destination of a stream.
- Duplex: Implements both `Readable` and `Writeable`. Can recieve and produce data. Example: TCP Socket
- Transform: Type of `Duplex` stream. Data passing through stream are altered
- PassThrough: Special types of `Transform` stream. Do not alter the data passing through.

## Stream Events

All stream is instance of `EventEmmiter`. Listening to events is not the recommended way to consume streams.

Node.js recommend using `pipe` and `pipeline` method.

## Connect Stream with `pipe`

The pipe method is available on streams that implement a Readable interface (Readable, Duplex, Transform, and Passthrough streams). The pipe method accepts a destination to pipe data to. The destination stream must implement a Writable interface (Writable, Duplex, Transform, and Passthrough streams).

## `fs` Module to Create and Write Stream

```js
const fs = require("fs");

// Create Readable stream
const inputFileStream = fs.createReadStream("file.txt");

// Outputing on the terminal Writeable
inputFileStream.pipe(process.stdout);
```

## Handling errors

One of the most important events fired by streams is the error event.

## `pipeline` streams

The pipeline method takes any number of streams as arguments, and a callback function as its last argument.

```js
const { PassThrough, pipeline } = require("stream");
const fs = require("fs");

// make sure you have a file.txt file with some text in it!
const input = fs.createReadStream("file.txt");
const out = fs.createWriteStream("out.txt");

const passThrough = new PassThrough();

console.log("Starting pipeline...");
pipeline(input, passThrough, out, err => {
  if (err) {
    console.log("Pipeline failed with an error:", err);
  } else {
    console.log("Pipeline ended successfully");
  }
});

// passThrough.emit("error", new Error("Uh oh!"));
```

Using pipeline simplifies error handling and stream cleanup, and makes combining streams in complex ways more straightforward. When an error occurs while using pipeline, the streams will be destroyed. Destroying the streams releases their internal resources, freeing up any memory the stream was using.

## Transform streams

```js
const { Transform, pipeline } = require("stream");

const upperCaseTransform = new Transform({
  transform: function(chunk, encoding, callback) {
    callback(null, chunk.toString().toUpperCase());
  }
});
```
