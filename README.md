# bitcoind-rpc

A JavaScript client for connecting Node.js applications to Bitcoin Core RPC. Use it to call RPC methods and batch requests against a running Bitcoin Core node.

## Features

- Connect to Bitcoin Core using a configuration object or a connection URL.
- Retrieve transaction IDs from the mempool with `getRawMemPool`.
- Fetch raw transactions with `getRawTransaction`.
- Group RPC requests with `batch`.
- Handle RPC responses and errors through callbacks.

## Installation

Install with npm in your Node.js project:

```bash
npm install bitcoind-rpc
```

You also need a running Bitcoin Core node with RPC enabled and credentials configured. Keep the RPC endpoint restricted to trusted clients.

## Usage

Save this example as `example.js`. Replace the credentials with those configured for your node. Port `18332` is the default Bitcoin Core testnet RPC port; use the port your node listens on.

```javascript
var RpcClient = require('bitcoind-rpc');

var config = {
  protocol: 'http',
  user: 'user',
  pass: 'pass',
  host: '127.0.0.1',
  port: '18332'
};

// Alternatively:
// var config = 'http://user:pass@127.0.0.1:18332';

var rpc = new RpcClient(config);

rpc.getRawMemPool(function (err, ret) {
  if (err) {
    console.error(err);
    process.exitCode = 1;
    return;
  }

  console.log('Mempool transaction IDs:', ret.result);
});
```

Run the example:

```bash
node example.js
```

RPC callbacks receive an error as the first argument and a response as the second. In this example, `ret.result` contains the mempool transaction IDs.

## License

MIT. This project is based on [bitpay/bitcoind-rpc](https://github.com/bitpay/bitcoind-rpc), released under the MIT license.

Original code copyright 2013–2018 BitPay, Inc. Retain the original copyright and MIT permission notice when distributing copies or substantial portions of the code.
