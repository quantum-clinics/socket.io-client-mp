重新打包微信小程序socket.io客户端, https://github.com/mdluo/socket.io-client-mp
原repo上的socket.io.slim.js打包有点小问题

直接下载并在小程序中调用 socket.io.slim.js 即可

```
const io = require('./socket.io.slim')

const socket = io('ws://192.168.1.100:7001', {
  transports: ['websocket'], // 此项必须设置
  transportOptions: {
    websocket: {
      extraHeaders: { // 可选，小程序 WebSocket API 允许设置的 header
        'x-client-id': 'abc',
      },
      protocols: ['custom-protocol'] // 可选，子协议数组
    },
  },
})
```


原repo中打包错误的具体解决办法是将webpack-stream 升级至 4.0.3
```
// socket.io-client-mp/package.json
"webpack-stream": "4.0.3",

// socket.io-client-mp/
npm install
```

再将node-modules中webpack-stream里package.json中的 webpack 降为2.1.0-beta.25
```
// socket.io-client-mp/node_modules/webpack-stream/package.json
"webpack": "2.1.0-beta.25"

// socket.io-client-mp/node_modules/webpack-stream/
npm install
```

然后打包
```
// socket.io-client-mp/
gulp
```