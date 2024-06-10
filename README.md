# n3-mwe

This is a basic Vue 3 project with Vite using the [n3 parser and store](https://www.npmjs.com/package/n3). ([#386](https://github.com/rdfjs/N3.js/issues/386))

Created with

```sh
yarn create vue@latest
```

added the dependencies according to the `package.json`, i.e.:

- `n3`
- `streamify-string`
- `vite-plugin-node-polyfills`
- `@vue/compiler-dom`
- `@vue/server-renderer`

The code:

```js
const streamParser = new StreamParser()
let dataString = "<http://example.org/some> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/1999/02/22-rdf-syntax-ns#Class> ."
Streamify(dataString).pipe(streamParser)

const n3_store = new Store()
n3_store.import(streamParser).on('end', () => {
  this.dataModel = n3_store
})
```

executes well as a test, but not in the browser (firefox and chromium). I get the following errors:

```
Uncaught TypeError: process.nextTick is not a function
    resume readable.js:903
    resume readable.js:895
    on readable.js:821
    import N3Store.js:306
    tryStore App.vue:27
    mounted App.vue:18
    VueJS 8
    <anonymous> main.js:4
readable.js:903:12
```
```
Uncaught TypeError: process.nextTick is not a function
    onwrite writable.js:411
    _write transform.js:168
    _transform N3StreamParser.js:29
    _write transform.js:153
    writeOrBuffer writable.js:334
    _write writable.js:283
    write writable.js:286
    ondata _stream_readable.js:629
    emit events.js:153
    read _stream_readable.js:451
    flow _stream_readable.js:858
    resume_ _stream_readable.js:842
    run browser.js:153
    drainQueue browser.js:123
    setTimeout handler*runTimeout browser.js:41
    nextTick browser.js:143
    resume _stream_readable.js:832
    resume _stream_readable.js:824
    on _stream_readable.js:753
    pipe _stream_readable.js:626
    tryStore App.vue:24
    mounted App.vue:18
    VueJS 8
    <anonymous> main.js:4
writable.js:411:16
```
