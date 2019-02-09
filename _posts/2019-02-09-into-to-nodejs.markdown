# Intro To NodeJs

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

**You can use the path module parse function to parse a __filename**








