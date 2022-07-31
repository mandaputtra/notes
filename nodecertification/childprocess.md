# Child Process

Child process is another process created by process (parent). This technique used for multitasking on operating system.

There are four different ways to create a child process in Node: `spawn()`, `fork()`, `exec()`, and `execFile()`.

```js
const { spawn } = require('child_process');

const child = spawn('pwd')

child.on('exit', function (code, signal) {
  console.log('child process exited with ' +
              `code ${code} and signal ${signal}`);
});

child.stdout.on('data', (data) => {
  console.log(`child stdout:\n${data}`);
});

child.stderr.on('data', (data) => {
  console.error(`child stderr:\n${data}`);
})
```


Command piping on child process, its like using streams

```
const { spawn } = require('child_process');

const find = spawn('find', ['.', '-type', 'f']);
const wc = spawn('wc', ['-l']);

find.stdout.pipe(wc.stdin);

wc.stdout.on('data', (data) => {
  console.log(`Number of files ${data}`);
});
```

The exec function is a good choice if you need to use the shell syntax and if the size of the data expected from the command is small. (Remember, exec will buffer the whole data in memory before returning it.)

The spawn function is a much better choice when the size of the data expected from the command is large, because that data will be streamed with the standard IO objects.

Execute child process independednly of its parent process

```
const { spawn } = require('child_process');

const child = spawn('node', ['timer.js'], {
  detached: true,
  stdio: 'ignore'
});

child.unref();
```

The `execFile` function. If you need to execute a file without using a shell, the `execFile` function is what you need. It behaves exactly like the exec function, but does not use a shell, which makes it a bit more efficient. On Windows, some files cannot be executed on their own, like `.bat` or `.cmd`` files. Those files cannot be executed with `execFile` and either exec or spawn with shell set to true is required to execute them.

Sync version of child process


```
const { 
  spawnSync, 
  execSync, 
  execFileSync,
} = require('child_process');
```

The `fork()` function. The fork function is a variation of the `spawn` function for spawning node processes. The biggest difference between spawn and fork is that a communication channel is established to the child process when using fork, so we can use the send function on the forked process along with the global process object itself to exchange messages between the parent and forked processes. We do this through the `EventEmitter` module interface.

```
// parent.js
const { fork } = require('child_process');

const forked = fork('child.js');

forked.on('message', (msg) => {
  console.log('Message from child', msg);
});

forked.send({ hello: 'world' });
```


```
// child.js
process.on('message', (msg) => {
  console.log('Message from parent:', msg);
});

let counter = 0;

setInterval(() => {
  process.send({ counter: counter++ });
}, 1000);
```

```compute.js
const longComputation = () => {
  let sum = 0;
  for (let i = 0; i < 1e9; i++) {
    sum += i;
  };
  return sum;
};

process.on('message', (msg) => {
  const sum = longComputation();
  process.send(sum);
});
```

```request
const http = require('http');
const { fork } = require('child_process');

const server = http.createServer();

server.on('request', (req, res) => {
  if (req.url === '/compute') {
    const compute = fork('compute.js');
    compute.send('start');
    compute.on('message', sum => {
      res.end(`Sum is ${sum}`);
    });
  } else {
    res.end('Ok')
  }
});

server.listen(3000);
```
