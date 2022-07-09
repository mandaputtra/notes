# Control Flow

- http://book.mixu.net/node/ch7.html

It's a way to control your Node.js application whether you want to perform code that asynchronous or synchronous.

In Node, you can choose whether to block the main thread with busy task or not at all. The way you will do this is with `Promise` or `Callack`.

```js
for(var i = 1; i &lt;= 1000; i++) {
  fs.readFile('./'+i+'.txt', function() {
     // do something with the file
  });
}
do_next_part();
```

That code will run 1000 asynchronous task, schedule it in the background and then without waiting all to resolve it will do `do_next_part();`.

A control flow function is a lightweight, generic piece of code which runs in between several asynchronous function calls and which take care of the necessary housekeeping to:

- control the order of execution,
- collect data,
- limit concurrency and call the next step in the program.


