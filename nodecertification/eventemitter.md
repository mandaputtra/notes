# Events

## Understanding event emitter by building it yourself

- https://www.freecodecamp.org/news/how-to-code-your-own-event-emitter-in-node-js-a-step-by-step-guide-e13b7e7908e1/

## Event emitter

Events module are for passing events

```
const e = new EventEmitter()


e.on('news', (data) => {
  console.log(data)
}) // send data


e.emit('news', 'news data')

e.once('hotnews', () => {

}) // Can only be triggered for once
```
