# stream-text-file

This is `index.js` file:
```
var http = require("http");
var filename = process.argv[2];

if (!filename)
    return console.log("Usage: node tailServer filename");

var spawn = require('child_process').spawn;
var tail = spawn('tail', ['-f', filename]);

http.createServer(function (request, response) {
    console.log('request starting...');

    response.writeHead(200, {'Content-Type': 'text/plain' });

    tail.stdout.on('data', function (data) {
      response.write('' + data);                
    });
}).listen(8088);

console.log('Server running at http://127.0.0.1:8088/');
```

Usage:

```
node index.js path_to_your_log_file 
```

Resource:

https://stackoverflow.com/questions/11225001/reading-a-file-in-real-time-using-node-js
