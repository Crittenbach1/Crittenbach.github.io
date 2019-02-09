
**Everything in Nodejs is inside a Module Wrapper Function** 

```

(function (exports, require, module, __filename, __dirname) {

var url = "http://mylogger.io/log";

function log(message) {
  // send http request
  console.log(message);
}

module.exports.log = log;

})

```

**View the __filename and __dirname with the module wrapper args**

```
    console.log(__filename); 
    console.log(__dirname);
```

terminal:

```
    Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
    /Users/cynthia/.atom/myProjects/nodejs/app.js
    /Users/cynthia/.atom/myProjects/nodejs
```
**Use the path module parse function to parse a __filename**

``` 
    const path = require('path');

    var pathObj = path.parse(__filename);

    console.log(pathObj);
```

terminal:

```
    Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
    { root: '/',
      dir: '/Users/cynthia/.atom/myProjects/nodejs',
      base: 'app.js',
      ext: '.js',
      name: 'app' }
```

**Node os module functions allow you to get info about the OS**


``` 
    const os = require('os');

    var totalMemory = os.totalmem();
    var freeMemory = os.freemem();

    //console.log('Total memory: ' + totalMemory);

    //Template string
    //ES6 / ES2015 : ECMAScript 6

    console.log(`Total Memory: ${totalMemory}`);
    console.log(`Free Memory: ${freeMemory}`);
```

terminal:

```
    Total Memory: 8589934592
    Free Memory: 43216896
```

**Use node fs module to a show string array of directory files**


``` 
    const fs = require('fs');

    const files = fs.readdirSync('./');
    console.log(files);

    fs.readdir('./', function(err, files) {
      if (err) console.log('Error', err);
    });
```

terminal:

```
     Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
     [ '.git', 'app.js', 'logger.js' ]
```

**Or throw an error:**

``` 
    const fs = require('fs');

    const files = fs.readdirSync('./');
    console.log(files);

    fs.readdir('$', './', function(err, files) {
      if (err) console.log('Error', err);
      else console.log('Result', files);
    });
```

terminal:

```
     Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
    [ '.git', 'app.js', 'logger.js' ]
    internal/fs/utils.js:60
        throw new ERR_INVALID_OPT_VALUE_ENCODING(encoding);
        ^

    TypeError [ERR_INVALID_OPT_VALUE_ENCODING]: The value "./" is invalid for option "encoding"
        at assertEncoding (internal/fs/utils.js:60:11)
        at getOptions (internal/fs/utils.js:182:5)
        at Object.readdir (fs.js:758:13)
        at Object.<anonymous> (/Users/cynthia/.atom/myProjects/nodejs/app.js:31:4)
        at Module._compile (internal/modules/cjs/loader.js:689:30)
        at Object.Module._extensions..js (internal/modules/cjs/loader.js:700:10)
        at Module.load (internal/modules/cjs/loader.js:599:32)
        at tryModuleLoad (internal/modules/cjs/loader.js:538:12)
        at Function.Module._load (internal/modules/cjs/loader.js:530:3)
        at Function.Module.runMain (internal/modules/cjs/loader.js:742:12)
```

**Raise event and register a listener with the EventEmitter Class**
``` 
   
    const EventEmitter = require('events'); // CLASS
    const emitter = new EventEmitter(); // OBJECT

    //Register a listener
    emitter.on('messageLogged', function(){
      console.log('Listener called');
    })

    // Raise an Event
    emitter.emit('messageLogged');

```

terminal:

```
    Listener called

```

**You can pass an object argument to event listeners**


``` 
   
    const EventEmitter = require('events'); // CLASS
    const emitter = new EventEmitter(); // OBJECT

    //Register a listener
    emitter.on('messageLogged', (arg) => {
      console.log('Listener called', arg);
    })

    // Raise an Event
    emitter.emit('messageLogged', { id: 1, url: 'http://' });

```

terminal:

```
    Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
    Listener called { id: 1, url: 'http://' }

```


**Emit a message inside Logger class log method on the messageLogged event**

/logger.js
``` 
     const EventEmitter = require('events'); // CLASS

    var url = "http://mylogger.io/log";

    class Logger extends EventEmitter {
        log(message) {
          // send http request
          console.log(message);

          // Raise an Event
          this.emit('messageLogged', { id: 1, url: 'http://' });
        }
    }


    module.exports = Logger;
```

/app.js

``` 
    const Logger = require('./logger');
    const logger = new Logger();

    // Register a listener
    logger.on('messageLogged', (arg) => {
      console.log('Listener called', arg);
    })

    logger.log('message');

```


terminal:

```
    Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
    message
    Listener called { id: 1, url: 'http://' }

```

**Connect to server 3000 with the http module**

/app.js

``` 
    const http = require('http');

    const server = http.createServer();

    server.on('connection', (socket) => {
      console.log('New connection...');
    })

    server.listen(3000);

    console.log('Listening on port 3000...')

```


terminal when you go to localhost3000 in browser:


```
    Cynthias-MacBook-Pro:nodejs cynthia$ node app.js
      Listening on port 3000...
      New connection...
      New connection...

```

**Write hello string on / url in browser**

/app.js

``` 
   const http = require('http');

    const server = http.createServer((req, res) => {
      if (req.url == '/') {
        res.write("hello ");
        res.write("hello ");
        res.write("hello ");
        res.write("hello ");
        res.end();
      }
    });

    server.listen(3000);

    console.log('Listening on port 3000...')

```


in browser:


```
   hello hello hello hello
```

**Write hello string on / url in browser**

/app.js

``` 
   const http = require('http');

    const server = http.createServer((req, res) => {
      if (req.url == '/') {
        res.write("hello ");
        res.write("hello ");
        res.write("hello ");
        res.write("hello ");
        res.end();
      }
    });

    server.listen(3000);

    console.log('Listening on port 3000...')

```


in browser:


```
   hello hello hello hello
```

**Show api JSON on api/courses url**

/app.js

``` 
  const http = require('http');

    const server = http.createServer((req, res) => {
      if (req.url == '/') {
        res.write("hello");
        res.end();
      }

      if (req.url == '/api/courses') {
        res.write(JSON.stringify([{ name: "cynthia", age: 23 }]));
        res.end();
      }

    });

    server.listen(3000);

    console.log('Listening on port 3000...')

```


in browser:


```
[{"name":"cynthia","age":23}]
```









