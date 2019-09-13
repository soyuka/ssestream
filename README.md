# SseStream

A node stream for writing Server-Sent Events

Note I merged together:
- https://github.com/EventSource/node-ssestream/blob/master/README.md
- https://gist.github.com/gitawego/8ef33ec7d895498f2eedd95eafa835bb
- https://github.com/EventSource/node-ssestream/pull/2

## Installation

```
npm install sse-stream
```

Or:

```
yarn add sse-stream
```

## Usage

In a `(req, res)` handler for a [`request`](https://nodejs.org/api/http.html#http_event_request) event, Express [#get](https://expressjs.com/en/4x/api.html#app.get.method) route or similar:

```javascript
const SseStream = require('sse-stream')

function (req, res) {
  const headers = {'CUSTOM-HEADER': 'FOO'}
  const sse = new SseStream(req, headers)
  sse.pipe(res)

  const message = {
    data: 'hello\nworld',
  }
  sse.write(message)
}
```

Properties on `message`:

* `data` (String or object, which gets turned into JSON)
* `event`
* `id`
* `retry`
* `comment`
