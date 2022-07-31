# Node.js CLI Options

- https://blog.risingstack.com/mastering-the-node-js-cli-command-line-options/

To access man CLI page `man node`.


`-v` : version

`-e` : eval `node -e 'console.log(3 + 2)'`

`-c` : check syntax without actually running it

`--inspect-brk[=host:port]` : The --inspect-brk has the same functionality as the --inspect option, however it pauses the execution at the first line of the user script.

`--prof-process` : Using the --prof-process, the Node.js process will output the v8 profiler output.

## V8

`--max_old_space_size` : With this option, you can set the maximum size of the old space on the heap, which directly affects how much memory your process can allocate.

`--optimize_for_size` : With this option, you can instruct V8 to optimize the memory space for size – even if the application gets slower.


