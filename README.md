# Node-Tutorial

Learn NodeJS by Ifeanyi Omeata

## Tutorial

---

### [1-NODE CRASH COURSE - NET NINJA](#)

+INTRODUCTION

<details>
  <summary>1. Check for Node Version</summary>

```Javascript
node -v
```

</details>

<details>
  <summary>2. Run Node File</summary>

```Javascript
node index.js
```

</details>

<details>
  <summary>3. The Global Object</summary>

Test.js:

```Javascript
let count = 0

const program = global.setInterval(()=>{
    count++
    console.log(count)
}, 1000)

global.setTimeout(()=>{
    console.log("Setting timeout")
    clearInterval(program)
}, 3000)
```

Absolute Path

```Javascript
console.log(__dirname)
```

```Javascript
// ~/Desktop/SERVER/Cloud/node
```

Absolute Path + Filename

```Javascript
console.log(__filename)
```

```Javascript
// ~/Desktop/SERVER/Cloud/node/test.js
```

</details>

<details>
  <summary>4. Modules and Require</summary>

require.js:

```Javascript
const people = ['yoshi' , 'ryu', ' chun-li' , ' mario'];
const ages = [20, 25, 30, 35];

module.exports = {
    people,
    ages
};

```

modules.js:

```Javascript
const {people, ages} = require('./require.js');

console.log(people, ages);
```

```Javascript
// [ 'yoshi', 'ryu', ' chun-li', ' mario' ] [ 20, 25, 30, 35 ]
```

</details>

<details>
  <summary>5. OS module</summary>

```Javascript
const os = require('os');

console.log(os.platform(), os.homedir());

```

```Javascript
// darwin /Users/ifeanyiomeata
```

</details>

<details>
  <summary>6. Reading Files</summary>

```Javascript
const fs = require("fs");

// reading files
fs.readFile('./docs/blog1.txt', (err, data) => {
    if(err){
    console.log(err);
    }
    console.log(data.toString());
});

console.log('last line');
```

```Javascript
// last line
// Hello World!
// Hello World 2!
```

</details>

<details>
  <summary>7. Writing Files</summary>

```Javascript
const fs = require("fs");

// writing files
fs.writeFile('./docs/blog1.txt', 'hello, world', () => {
    console.log('file was written');
});
fs.writeFile('./docs/blog2.txt', 'hello, again' , () => {
    console.log('file was written');
});
```

```Javascript
// file was written
// file was written
```

</details>

<details>
  <summary>8. Create and Delete Folder/Directory</summary>

```Javascript
const fs = require("fs");

// Create and Delete directories/Folders
if(!fs.existsSync('./assets')) {
    fs.mkdir('./assets', (err) => {
        if (err) {
            console.error(err);
        }
        console.log('folder created');
    });
} else {
    fs.rmdir('./assets', (err) => {
        if(err) {
            console.log(err)
        }
        console.log('folder deleted');
    })
}
```

```Javascript
// folder created
// folder deleted
```

</details>

<details>
  <summary>9. Delete Files</summary>

```Javascript
const fs = require("fs");

// deleting files
if (fs.existsSync('./docs/blog1.txt')) {
    fs.unlink('./docs/blog1.txt', (err) => {
        if(err) {
            console.log(err)
        }
        console.log('file deleted');
    })
}
```

```Javascript
// file deleted
```

</details>

<details>
  <summary>10. Read Stream</summary>

```Javascript
const fs = require("fs");

const readStream = fs.createReadStream('./docs/blog2.txt', { encoding: 'utf8' });

readStream.on('data', (chunk) => {
    console.log('-------- NEW CHUNK -----');
    console.log(chunk);
});

```

```Javascript
// -------- NEW CHUNK -----
// <Buffer 4c 6f 72 65 6d 20 69 70 73 75 6d 20 64 6f 6c 6f 72 20 73 69 74 20 61 6d 65 74 2c 20 63 6f 6e 73 65 63 74 65 74 75 65 72 20 61 64 69 70 69 73 63 69 6e ... 65486 more bytes>
// -------- NEW CHUNK -----
// <Buffer 20 56 69 76 61 6d 75 73 20 69 6e 20 65 72 61 74 20 75 74 20 75 72 6e 61 20 63 75 72 73 75 73 20 76 65 73 74 69 62 75 6c 75 6d 2e 20 46 75 73 63 65 20 ... 65486 more bytes>
// -------- NEW CHUNK -----
// <Buffer 53 75 73 70 65 6e 64 69 73 73 65 20 66 65 75 67 69 61 74 2e 20 53 75 73 70 65 6e 64 69 73 73 65 20 65 6e 69 6d 20 74 75 72 70 69 73 2c 20 64 69 63 74 ... 65486 more bytes>
// -------- NEW CHUNK -----
// <Buffer 69 62 75 6c 75 6d 20 65 74 2c 20 74 65 6d 70 6f 72 20 61 75 63 74 6f 72 2c 20 6a 75 73 74 6f 2e 20 49 6e 20 61 63 20 66 65 6c 69 73 20 71 75 69 73 20 ... 65486 more bytes>
// -------- NEW CHUNK -----
// <Buffer 6c 61 6d 63 6f 72 70 65 72 20 75 6c 74 72 69 63 69 65 73 20 6e 69 73 69 2e 20 4e 61 6d 20 65 67 65 74 20 64 75 69 2e 20 45 74 69 61 6d 20 72 68 6f 6e ... 11132 more bytes>
```

</details>

<details>
  <summary>11. Write Stream</summary>

```Javascript
const fs = require("fs");

const readStream = fs.createReadStream('./docs/blog2.txt',{ encoding: 'utf8' });
const writeStream = fs.createWriteStream('./docs/blog3.txt');

readStream.on('data' , (chunk) => {
    console.log('------ NEW CHUNK -----');
    console.log(chunk);
    writeStream.write('\nNEW CHUNK\n');
    writeStream.write(chunk);
});
```

</details>

<details>
  <summary>12. Piping</summary>

```Javascript
const fs = require("fs");

const readStream = fs.createReadStream('./docs/blog2.txt',{ encoding: 'utf8' });
const writeStream = fs.createWriteStream('./docs/blog3.txt');

// readStream.on('data' , (chunk) => {
//     console.log('------ NEW CHUNK -----');
//     console.log(chunk);
//     writeStream.write('\nNEW CHUNK\n');
//     writeStream.write(chunk);
// });

// piping
readStream.pipe(writeStream);
```

</details>

+REQUESTS & RESPONSES

<details>
  <summary>13. Create a Server</summary>

```Javascript
const http = require('http');

const server = http.createServer((req, res) =>{
    console.log('request made');
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

```Javascript
// listening for requests on port 3000
// request made
```

</details>

<details>
  <summary>14. Get Request URL and Method</summary>

```Javascript

const http = require('http');

const server = http.createServer((req, res) =>{
    console.log('request made');
    console.log("Url: ", req.url);
    console.log("Method: ", req.method);
    console.log("Headers: ", req.headers);
    console.log("Body: ", req.body);
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

```Javascript
// listening for requests on port 3000
// request made
// Url:  /
// Method:  GET
// Headers:  {
//   host: 'localhost:3000',
//   connection: 'keep-alive',
//   'sec-ch-ua': '"Chromium";v="106", "Google Chrome";v="106", "Not;A=Brand";v="99"',
//   'sec-ch-ua-mobile': '?0',
//   'sec-ch-ua-platform': '"macOS"',
//   'upgrade-insecure-requests': '1',
//   'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36',
//   accept: 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9',
//   'sec-fetch-site': 'none',
//   'sec-fetch-mode': 'navigate',
//   'sec-fetch-user': '?1',
//   'sec-fetch-dest': 'document',
//   'accept-encoding': 'gzip, deflate, br',
//   'accept-language': 'en-GB,en-US;q=0.9,en;q=0.8'
// }
// Body:  undefined
```

</details>

<details>
  <summary>15. Response - Set Header Content Type </summary>

```Javascript

const http = require('http');

const server = http.createServer((req, res) => {
    console.log('request made');
    console.log("Url: ", req.url);
    console.log("Method: ", req.method);
    console.log("Headers: ", req.headers);
    console.log("Body: ", req.body);

    // set header content type
    res.setHeader('Content-Type', 'text/plain');
    res.write('hello, ninjas');
    res.end();
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

```Javascript
const http = require('http');

const server = http.createServer((req, res) => {
    console.log('request made');
    // console.log("Url: ", req.url);
    // console.log("Method: ", req.method);
    // console.log("Headers: ", req.headers);
    // console.log("Body: ", req.body);

    // set header content type
    res.setHeader('Content-Type', 'text/html');
    res.write('<head><link rel="stylesheet" href="#"></head>');
    res.write('<h1>Welcome!</h1>');
    res.write('<h2>hello, ninjas</h2>');
    res.end();
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

</details>

<details>
  <summary>16. Returning HTML Pages </summary>

```Javascript
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    console.log('request made');

    // set header content type
    res.setHeader('Content-Type', 'text/html');

    // send an html file.
    fs.readFile('./views/index.html', (err, data) => {
        if(err) {
            console.log(err);
            res.end();
        } else {
            res.write(data);
            res.end();
            // OR
            // res.end(data);
        }
    })

});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

</details>

<details>
  <summary>17. Routing HTML Pages</summary>

```Javascript
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    console.log('request made');

    // set header content type
    res.setHeader('Content-Type', 'text/html');

    // get path from request
    let path = './views/';
    switch (req.url) {
        case '/':
            path += 'index.html';
            break;
        case '/about':
            path += 'about.html';
            break;
        default:
            path += '404.html';
            break;
    }

    // send an html file.
    fs.readFile(path, (err, data) => {
        if(err) {
            console.log(err);
            res.end();
        } else {
            res.end(data);
        }
    })
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

</details>

<details>
  <summary>18. Set Status Codes </summary>

Status codes describe the type of response sent to the browser.

```markdown
200- OK
301- Resource moved
404- Not found
500- Internal server error
```

```markdown
100 Range- Informational Responses
200 Range- Success codes
300 Range- Codes for redirects
400 Range- User or client error codes
500 Range- Server error codes
```

```Javascript
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    console.log('request made');

    // set header content type
    res.setHeader('Content-Type', 'text/html');

    // get path from request
    let path = './views/';
    switch (req.url) {
        case '/':
            path += 'index.html';
            res.statusCode = 200;
            break;
        case '/about':
            path += 'about.html';
            res.statusCode = 200;
            break;
        default:
            path += '404.html';
            res.statusCode = 404;
            break;
    }

    // send an html file.
    fs.readFile(path, (err, data) => {
        if(err) {
            console.log(err);
            res.end();
        } else {
            res.end(data);
        }
    })
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

</details>

<details>
  <summary>19. HTTP Redirects</summary>

```Javascript

const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    console.log('request made');

    // set header content type
    res.setHeader('Content-Type', 'text/html');

    // get path from request
    let path = './views/';
    switch (req.url) {
        case '/':
            path += 'index.html';
            res.statusCode = 200;
            break;
        case '/about':
            path += 'about.html';
            res.statusCode = 200;
            break;
        case '/about-me':
            res.statusCode = 301;
            res.setHeader('Location', '/about');
            res.end();
            break;
        default:
            path += '404.html';
            res.statusCode = 404;
            break;
    }

    // send an html file.
    fs.readFile(path, (err, data) => {
        if(err) {
            console.log(err);
            res.end();
        } else {
            res.end(data);
        }
    })
});

server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000')
})
```

</details>

+NODE PACKAGE MANAGER (NPM)

<details>
  <summary>20. Install Nodemon </summary>

```Javascript
npm install -g nodemon

yarn global add nodemon
```

```Javascript
nodemon server
```

</details>

<details>
  <summary>21. Create Package.json dependencies locally </summary>

```Javascript
npm init
```

```Javascript
{
  "name": "node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "doc": "docs"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "author": "",
  "license": "ISC"
}

```

</details>

<details>
  <summary>22. Install Lodash</summary>

```Javascript
npm i --save lodash
```

package.json:

```Javascript
{
  "name": "node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "doc": "docs"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "lodash": "^4.17.21"
  }
}
```

package-lock.json:

```Javascript
{
  "name": "node",
  "version": "1.0.0",
  "lockfileVersion": 2,
  "requires": true,
  "packages": {
    "": {
      "name": "node",
      "version": "1.0.0",
      "license": "ISC",
      "dependencies": {
        "lodash": "^4.17.21"
      }
    },
    "node_modules/lodash": {
      "version": "4.17.21",
      "resolved": "https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz",
      "integrity": "sha512-v2kDEe57lecTulaDIuNTPy3Ry4gLGJ6Z1O3vE1krgXZNrsQ+LFTGHVxVjcXPs17LhbZVGedAJv8XZ1tvj5FvSg=="
    }
  },
  "dependencies": {
    "lodash": {
      "version": "4.17.21",
      "resolved": "https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz",
      "integrity": "sha512-v2kDEe57lecTulaDIuNTPy3Ry4gLGJ6Z1O3vE1krgXZNrsQ+LFTGHVxVjcXPs17LhbZVGedAJv8XZ1tvj5FvSg=="
    }
  }
}

```

</details>

<details>
  <summary>23. Install all dependencies in Package.json</summary>

```Javascript
npm install
```

</details>

+EXPRESS

<details>
  <summary>24. Express Introduction</summary>

```Javascript
// We can use express as shown as below
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

</details>

<details>
  <summary>25. Install Express</summary>

```Javascript
npm install express --save
```

```Javascript
{
  "name": "node",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "directories": {
    "doc": "docs"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.18.2",
    "lodash": "^4.17.21"
  }
}
```

</details>

<details>
  <summary>26. Display Home Page</summary>

app.js:

```Javascript
const express = require('express');

// express app
const app = express();

// listen for requests
app.listen(3000);

// get home page
app.get('/', (req, res) => {
    res.send('<h1>Home page</h1>');
});
```

</details>

<details>
  <summary>27. Routing HTML Pages</summary>

app.js:

```Javascript
const express = require('express');
const path = require('path');

const homePage = path.join(__dirname, 'views/index.html')
const aboutPage = path.join(__dirname, 'views/about.html')
const _404Page = path.join(__dirname, 'views/404.html')

// express app
const app = express();

// listen for requests
app.listen(3000);

// get home page
app.get('/', (req, res) => {
    res.sendFile(homePage);
    // res.sendFile('./views/index.html' , { root: __dirname });
});

// get about page
app.get('/about', (req, res) => {
    res.sendFile(aboutPage);
    // res.sendFile('./views/about.html' , { root: __dirname });
});
```

</details>

<details>
  <summary>28. Create Nav Links</summary>

Index.html:

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Node.js Crash Course</title>
  </head>
  <body>
    <nav>
      <a href="/"> Homepage </a>
      <a href="/about"> About page </a>
    </nav>
    <h1>Home</h1>
    <h2>Your path to becoming a Node.js ninja!</h2>
  </body>
</html>
```

about.html:

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Node.js Crash Course</title>
  </head>
  <body>
    <nav>
      <a href="/"> Homepage </a>
      <a href="/about"> About page </a>
    </nav>
    <h1>About</h1>
    <h2>Your path to becoming a Node.js ninja!</h2>
  </body>
</html>
```

</details>

<details>
  <summary>29. Redirects & 404's</summary>

app.js:

```Javascript
const express = require('express');
const path = require('path');

const homePage = path.join(__dirname, 'views/index.html')
const aboutPage = path.join(__dirname, 'views/about.html')
const _404Page = path.join(__dirname, 'views/404.html')

// express app
const app = express();

// listen for requests
app.listen(3000);

// get home page
app.get('/', (req, res) => {
    res.sendFile(homePage);
});

// get about page
app.get('/about', (req, res) => {
    res.sendFile(aboutPage);
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// 404 page
app.use((req, res) => {
    res.status(404).sendFile(_404Page);
    // res.sendFile('./views/404.html', { root: __dirname });
});
```

</details>

+VIEW ENGINES

<details>
  <summary>30. Install EJS</summary>

```Javascript
npm install ejs
```

</details>

<details>
  <summary>31. EJS Sample</summary>

```Javascript
let ejs = require('ejs');
let people = ['geddy', 'neil', 'alex'];
let html = ejs.render('<%= people.join(", "); %>', {people: people});
```

```bash
ejs ./template_file.ejs -f data_file.json -o ./output.html
```

```html
<script src="ejs.js"></script>
<script>
  let people = ["geddy", "neil", "alex"];
  let html = ejs.render('<%= people.join(", "); %>', { people: people });
</script>
```

```html
<% if (user) { %>
<h2><%= user.name %></h2>
<% } %>
```

```Javascript
let template = ejs.compile(str, options);
template(data);
// => Rendered HTML string

ejs.render(str, data, options);
// => Rendered HTML string

ejs.renderFile(filename, data, options, function(err, str){
    // str => Rendered HTML string
});
```

</details>

<details>
  <summary>32. Create EJS Pages</summary>

Index.ejs:

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width-device-width, initial-scale=1.0" />
    <title>Blog Ninja</title>
  </head>
  <body>
    <nav>
      <div class="site-title">
        <a href="/"><h1>Blog Ninja</h1></a>
        <p>A Net Ninja Site</p>
      </div>
      <ul>
        <li><a href="/">Blogs</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/blogs/create">New Blog</a></li>
      </ul>
    </nav>
    <div class="blogs content">
      <h2>All Blogs</h2>
    </div>
  </body>
</html>
```

About.ejs:

```Javascript
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog Ninja</title>
</head>
<body>
    <nav>
        <div class="site-title">
            <a href="/"><h1>Blog Ninja</h1></a>
            <p>A Net Ninja Site</p>
        </div>
        <ul>
            <li><a href="/">Blogs</a></1li>
            <li><a href="/about">About</a></1li>
            <li><a href="/blogs/create">New Blog</a></1li>
        </ul>
    </nav>
    <div class="about content">
        <h2>About Us</h2>
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quia quibusdam quaerat illo a </p>
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quia quibusdam quaerat illo a </p>
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quia quibusdam quaerat illo a </p>
    </div>
</body>
</html>

```

404.ejs:

```Javascript
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog Ninja</title>
</head>
<body>
    <nav>
        <div class="site-title">
            <a href="/"><h1>Blog Ninja</h1></a>
            <p>A Net Ninja Site</p>
        </div>
        <ul>
            <li><a href="/">Blogs</a></1li>
            <li><a href="/about">About</a></1li>
            <li><a href="/blogs/create">New Blog</a></1li>
        </ul>
    </nav>
    <div class="not-found content">
        <h2>OOPS, page not found :)</h2>
    </div>
</body>
</html>

```

</details>

<details>
  <summary>33. Render EJS Template</summary>

```Javascript
const express = require('express');
const path = require('path');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

// listen for requests
app.listen(3000);

// get home page
app.get('/', (req, res) => {
    //res.sendFile(homePage);
    res.render('index');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about');
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404');
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

</details>

<details>
  <summary>34. Render Create Blog</summary>

app.js:

```Javascript
const express = require('express');
const path = require('path');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

// listen for requests
app.listen(3000);

// get home page
app.get('/', (req, res) => {
    //res.sendFile(homePage);
    res.render('index');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about');
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create');
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404');
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

create.ejs:

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width-device-width, initial-scale=1.0" />
    <title>Blog Ninja</title>
  </head>
  <body>
    <nav>
      <div class="site-title">
        <a href="/"><h1>Blog Ninja</h1></a>
        <p>A Net Ninja Site</p>
      </div>
      <ul>
        <li><a href="/">Blogs</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/blogs/create">New Blog</a></li>
      </ul>
    </nav>

    <div class="create-blog content">
      <form>
        <label for="title">Blog Title:</label>
        <input type="text" id="title" name="title" required />
        <label for="snippet">Blog Snippet:</label>
        <input type="text" id="snippet" name="snippet" required />
        <label for="body">Blog Body:</label>
        <textarea id="body" name="body" required></textarea>
        <button type="submit">Submit</button>
      </form>
    </div>
  </body>
</html>
```

</details>

<details>
  <summary>35. Displaying Internal Dynamic content</summary>

```html
<div class="site-title">
  <a href="/"><h1>Blog Ninja</h1></a>
  <p>A Net Ninja Site</p>
  <% const firstName = 'Fred' %>
  <p>His First Name is <%= firstName %>.</p>
</div>
```

</details>

<details>
  <summary>36. Displaying Context Dynamic content</summary>

```Javascript
// get home page
app.get('/', (req, res) => {
    //res.sendFile(homePage);
    res.render('index', { title: 'Home' });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Blog Ninja | <%= title %></title>
</head>
```

</details>

<details>
  <summary>37. Iterate through Blogs Array</summary>

```Javascript
const express = require('express');
const path = require('path');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

// listen for requests
app.listen(3000);

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width-device-width, initial-scale=1.0" />
    <title>Blog Ninja | <%= title %></title>
  </head>
  <body>
    <nav>
      <div class="site-title">
        <a href="/"><h1>Blog Ninja</h1></a>
        <p>A Net Ninja Site</p>
      </div>
      <ul>
        <li><a href="/">Blogs</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/blogs/create">New Blog</a></li>
      </ul>
    </nav>
    <div class="blogs content">
      <h2>All Blogs</h2>
      <% if(blogs.length > 0){ %> <% blogs.forEach(blog => { %>
      <div class="blog-preview">
        <h3 class="title">
          <a href="/blogs/<%= blog._id %>"><%= blog.title %></a>
        </h3>
        <p class="author">Written by <%= blog.author %></p>
        <p class="snippet"><%= blog.snippet %></p>
      </div>
      <% }) %> <% }else{ %>
      <p>No blogs to show</p>
      <% } %>
    </div>
  </body>
</html>
```

</details>

<details>
  <summary>38. Include Partials</summary>

Index.ejs:

```html
<html lang="en">
  <%- include('./partials/head.ejs') %>
  <body>
    <%- include('./partials/nav.ejs') %>
    <div class="blogs content">
      <h2>All Blogs</h2>
      <% if(blogs.length > 0){ %> <% blogs.forEach(blog => { %>
      <div class="blog-preview">
        <h3 class="title">
          <a href="/blogs/<%= blog._id %>"><%= blog.title %></a>
        </h3>
        <p class="author">Written by <%= blog.author %></p>
        <p class="snippet"><%= blog.snippet %></p>
      </div>
      <% }) %> <% }else{ %>
      <p>No blogs to show</p>
      <% } %>
    </div>
    <%- include('./partials/footer.ejs') %>
  </body>
</html>
```

Nav.ejs:

```html
<nav>
  <div class="site-title">
    <a href="/"><h1>Blog Ninja</h1></a>
    <p>A Net Ninja Site</p>
  </div>
  <ul>
    <li><a href="/">Blogs</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/blogs/create">New Blog</a></li>
  </ul>
</nav>
```

Head.ejs:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width-device-width, initial-scale=1.0" />
  <title>Blog Ninja | <%= title %></title>
</head>
```

Footer.ejs:

```html
<footer>Copyright &copy; 2022</footer>
```

</details>

<details>
  <summary>39. Styling Head</summary>

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Blog Ninja | <%= title %></title>
  <style>
    @import url("https://fonts.googleapis.com/css2?family=Noto+Serif:wght@400;700&display=swap");
    body {
      max-width: 1200px;
      margin: 20px auto;
      padding: 0 20px;
      font-family: "Noto Serif", serif;
      max-width: 1200px;
    }
    p,
    h1,
    h2,
    h3,
    a,
    ul {
      margin: 0;
      padding: 0;
      text-decoration: none;
      color: #222;
    }

    /* nav & footer styles */
    nav {
      display: flex;
      justify-content: space-between;
      margin-bottom: 60px;
      padding-bottom: 10px;
      border-bottom: 1px solid #ddd;
      text-transform: uppercase;
    }
    nav ul {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
    }
    nav li {
      list-style-type: none;
      margin-left: 20px;
    }
    nav h1 {
      font-size: 3em;
    }
    nav p,
    nav a {
      color: #777;
      font-weight: 300;
    }
    footer {
      color: #777;
      text-align: center;
      margin: 80px auto 20px;
    }
    h2 {
      margin-bottom: 40px;
    }
    h3 {
      text-transform: capitalize;
      margin-bottom: 8px;
    }
    .content {
      margin-left: 20px;
    }

    /* index styles */

    /* details styles */

    /* create styles */
    .create-blog form {
      max-width: 400px;
      margin: 0 auto;
    }
    .create-blog input,
    .create-blog textarea {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 8px;
    }
    .create-blog label {
      display: block;
      margin-top: 24px;
    }
    textarea {
      height: 120px;
    }
    .create-blog button {
      margin-top: 20px;
      background: crimson;
      color: white;
      padding: 6px;
      border: 0;
      font-size: 1.2em;
      cursor: pointer;
    }
  </style>
</head>
```

</details>

+MIDDLEWARES

<details>
  <summary>40. Create Middleware</summary>

```Javascript
// middleware
app.use((req, res, next) => {
    console.log('new request made:');
    console.log('host: ', req.hostname);
    console.log('path: ', req.path);
    console.log('method: ', req.method);
    next();
});
```

```markdown
new request made:
host: localhost
path: /
method: GET
```

```Javascript
const express = require('express');
const path = require('path');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

// listen for requests
app.listen(3000);

// middleware
app.use((req, res, next) => {
    console.log('new request made:');
    console.log('host: ', req.hostname);
    console.log('path: ', req.path);
    console.log('method: ', req.method);
    next();
});

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

</details>

<details>
  <summary>41. Use Morgan Middleware</summary>

```markdown
npm install morgan --save
```

Index.ejs:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

// listen for requests
app.listen(3000);

// middleware
app.use((req, res, next) => {
    console.log('new request made:');
    console.log('host: ', req.hostname);
    console.log('path: ', req.path);
    console.log('method: ', req.method);
    next();
});

app.use(morgan('dev'));

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```markdown
new request made:
host: localhost
path: /
method: GET
GET / 304 19.124 ms - -
```

</details>

<details>
  <summary>42. Use Style.css Static File</summary>

```Javascript
// static files
app.use(express.static('public'));
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

// listen for requests
app.listen(3000);

// middleware
app.use((req, res, next) => {
    console.log('new request made:');
    console.log('host: ', req.hostname);
    console.log('path: ', req.path);
    console.log('method: ', req.method);
    next();
});

app.use(morgan('dev'));

// static files
app.use(express.static('public'));

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

head.ejs:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Blog Ninja | <%= title %></title>
  <link rel="stylesheet" href="/styles.css" />
</head>
```

public/styles.css:

```Javascript
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif:wght@400;700&display=swap');
      body{
        max-width: 1200px;
        margin: 20px auto;
        padding: 0 20px;
        font-family: 'Noto Serif', serif;
        max-width: 1200px;
      }
      p, h1, h2, h3, a, ul{
        margin: 0;
        padding: 0;
        text-decoration: none;
        color: #222;
      }

      /* nav & footer styles */
      nav{
        display: flex;
        justify-content: space-between;
        margin-bottom: 60px;
        padding-bottom: 10px;
        border-bottom: 1px solid #ddd;
        text-transform: uppercase;
      }
      nav ul{
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
      }
      nav li{
        list-style-type: none;
        margin-left: 20px;
      }
      nav h1{
        font-size: 3em;
      }
      nav p, nav a{
        color: #777;
        font-weight: 300;
      }
      footer{
        color: #777;
        text-align: center;
        margin: 80px auto 20px;
      }
      h2{
        margin-bottom: 40px;
      }
      h3{
        text-transform: capitalize;
        margin-bottom: 8px;
      }
      .content{
        margin-left: 20px;
      }

      /* index styles */

      /* details styles */

      /* create styles */
      .create-blog form{
        max-width: 400px;
        margin: 0 auto;
      }
      .create-blog input,
      .create-blog textarea{
        display: block;
        width: 100%;
        margin: 10px 0;
        padding: 8px;
      }
      .create-blog label{
        display: block;
        margin-top: 24px;
      }
      textarea{
        height: 120px;
      }
      .create-blog button{
        margin-top: 20px;
        background: crimson;
        color: white;
        padding: 6px;
        border: 0;
        font-size: 1.2em;
        cursor: pointer;
      }
```

</details>

+MONGODB

<details>
  <summary>43. Connect to MongoDB</summary>

```markdown
Mongodb Atlas
https://www.mongodb.com/cloud/atlas
```

```Javascript
const dbURI = 'mongodb+srv://admin:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority';
```

```Javascript
const { MongoClient, ServerApiVersion } = require('mongodb');
const uri = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true, serverApi: ServerApiVersion.v1 });
client.connect(err => {
  const collection = client.db("test").collection("devices");
  // perform actions on the collection object
  client.close();
});
```

</details>

<details>
  <summary>44. Connect with Mongoose</summary>

```markdown
npm install mongoose --save
```

```Javascript
const mongoose = require('mongoose');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
  .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));
```

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// middleware
app.use((req, res, next) => {
    console.log('new request made:');
    console.log('host: ', req.hostname);
    console.log('path: ', req.path);
    console.log('method: ', req.method);
    next();
});

app.use(morgan('dev'));

// static files
app.use(express.static('public'));

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```Javascript
// connected to db
```

</details>

<details>
  <summary>45. Create Database Model and Schema</summary>

models/blog.js:

```Javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const blogSchema = new Schema({
    title: {
        type: String,
        required: true
    },
    snippet: {
        type: String,
        required: true
    },
    body: {
        type: String,
        required: true
    }
}, { timestamps: true });

const Blog = mongoose.model('Blog', blogSchema);
module.exports = Blog;
```

</details>

<details>
  <summary>46. Saving a Single Blog</summary>

```Javascript
const Blog = require('./models/blog');

// mongoose sandbox routes
app.get('/add-blog', (req, res) => {
    const blog = new Blog({
        title: 'new blog 2',
        snippet: 'about my new blog',
        body: 'more about my new blog'
    });

    blog.save()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));

// mongoose sandbox routes
app.get('/add-blog', (req, res) => {
    const blog = new Blog({
        title: 'new blog 2',
        snippet: 'about my new blog',
        body: 'more about my new blog'
    });

    blog.save()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```Javascript
// {
// "title": "new blog 2",
// "snippet": "about my new blog",
// "body": "more about my new blog",
// "_id": "635bd60ce18a55b9822dc59a",
// "createdAt": "2022-10-28T13:15:56.807Z",
// "updatedAt": "2022-10-28T13:15:56.807Z",
// "__v": 0
// }
```

</details>

<details>
  <summary>47. Get all Blogs</summary>

```Javascript
//get all blogs
app.get('/all-blogs', (req, res) => {
    Blog.find()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));

// mongoose sandbox routes
// add blog
app.get('/add-blog', (req, res) => {
    const blog = new Blog({
        title: 'new blog 2',
        snippet: 'about my new blog',
        body: 'more about my new blog'
    });

    blog.save()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

//get all blogs
app.get('/all-blogs', (req, res) => {
    Blog.find()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```Javascript
// [
//   {
//   "_id": "635bd60ce18a55b9822dc59a",
//   "title": "new blog 2",
//   "snippet": "about my new blog",
//   "body": "more about my new blog",
//   "createdAt": "2022-10-28T13:15:56.807Z",
//   "updatedAt": "2022-10-28T13:15:56.807Z",
//   "__v": 0
//   },
//   {
//   "_id": "635bd7cfe18a55b9822dc59c",
//   "title": "new blog 2",
//   "snippet": "about my new blog",
//   "body": "more about my new blog",
//   "createdAt": "2022-10-28T13:23:27.292Z",
//   "updatedAt": "2022-10-28T13:23:27.292Z",
//   "__v": 0
//   }
// ]
```

</details>

<details>
  <summary>48. Get a Single Blog</summary>

```Javascript
//get single blog
app.get('/single-blog', (req, res) => {
    Blog.findById('635bd60ce18a55b9822dc59a')
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});
```

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));

// mongoose sandbox routes
// add blog
app.get('/add-blog', (req, res) => {
    const blog = new Blog({
        title: 'new blog 2',
        snippet: 'about my new blog',
        body: 'more about my new blog'
    });

    blog.save()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

//get all blogs
app.get('/all-blogs', (req, res) => {
    Blog.find()
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

//get single blog
app.get('/single-blog', (req, res) => {
    Blog.findById('635bd60ce18a55b9822dc59a')
        .then((result) => {
            res.send(result);
        })
        .catch((err) => {
            console.log(err);
        });
});

// get home page
app.get('/', (req, res) => {
    const blogs = [
        { title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur' },
        { title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur' },
    ];
    res.render('index', { title: 'Home', blogs });
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// redirects
app.get('/about-us' , (req, res) => {
    res.redirect('/about');
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

```Javascript
// {
// "_id": "635bd60ce18a55b9822dc59a",
// "title": "new blog 2",
// "snippet": "about my new blog",
// "body": "more about my new blog",
// "createdAt": "2022-10-28T13:15:56.807Z",
// "updatedAt": "2022-10-28T13:15:56.807Z",
// "__v": 0
// }
```

</details>

+REQUESTS

<details>
  <summary>49. List of Requests</summary>

```Javascript
// localhost:3000/blogs        -----> GET (Get a list of blogs)
// localhost:3000/blogs/create -----> GET (Render a form to create a new blog)
// localhost:3000/blogs        -----> POST (Create a new blog)
// localhost:3000/blogs/:id    -----> GET (Get a single blog)
// localhost:3000/blogs/:id    -----> DELETE (Delete a single blog)
// localhost:3000/blogs/:id    -----> PUT  (Update a single blog)
```

</details>

<details>
  <summary>50. Get Request with Route [/blogs]</summary>

```Javascript
// blogs routes
app.get('/blogs' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));

// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// blogs routes
// Get all Blogs
app.get('/blogs' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

</details>

<details>
  <summary>51. Post Request with Route [/blogs]</summary>

Create.ejs:

```Javascript
<html lang="en">
    <%- include('./partials/head.ejs')  %>
    <body>
        <%- include('./partials/nav.ejs')  %>
        <div class= "create-blog content">
            <form action="/blogs" method="POST">
                <label for="title">Blog Title:</label>
                <input type="text" id="title" name="title" required>
                <label for="snippet">Blog Snippet:</label>
                <input type="text" id="snippet" name="snippet" required>
                <label for="body">Blog Body:</label>
                <textarea id="body" name="body" required></textarea>
                <button type="submit">Submit</button>
            </form>
        </div>
        <%- include('./partials/footer.ejs')  %>
    </body>
</html>
```

```Javascript
// static files
app.use(express.urlencoded({ extended: true }));

// Post a new blog
app.post('/blogs', (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
});
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));
app.use(express.urlencoded({ extended: true }));
app.use(morgan('dev'));

// Routes
// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// Blogs routes
// Get all Blogs
app.get('/blogs' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});

// Post a new blog
app.post('/blogs', (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

</details>

<details>
  <summary>52. Get a Single blog with Route [/blogs/:id]</summary>

index.ejs:

```html
<html lang="en">
  <%- include('./partials/head.ejs') %>
  <body>
    <%- include('./partials/nav.ejs') %>
    <div class="blogs content">
      <h2>All Blogs</h2>
      <% if(blogs.length > 0){ %> <% blogs.forEach(blog => { %>
      <div class="blog-preview">
        <a class="single" href="/blogs/<%= blog._id %>">
          <h3 class="title"><%= blog.title %></h3>
          <p class="author">Written by <%= blog.author %></p>
          <p class="snippet"><%= blog.snippet %></p>
        </a>
      </div>
      <% }) %> <% }else{ %>
      <p>No blogs to show</p>
      <% } %>
    </div>
    <%- include('./partials/footer.ejs') %>
  </body>
</html>
```

details.ejs:

```html
<html lang="en">
  <%- include("./partials/head.ejs") %>

  <body>
    <%- include("./partials/nav.ejs") %>

    <div class="details content">
      <h2><%= blog.title %></h2>
      <div class="content">
        <p><%= blog.body %></p>
      </div>
      <a class="delete" data-doc="<%= blog._id %>">delete</a>
    </div>

    <%- include("./partials/footer.ejs") %>
  </body>
</html>
```

style.css:

```css
/* index styles */
.blogs a {
  display: block;
  margin: 40px 0;
  padding-left: 30px;
  border-left: 6px solid crimson;
}
.blogs a:hover h3 {
  color: crimson;
}
```

```Javascript
// Get a single blog
app.get('/blogs/:id', (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            console.log(err);
        });
});
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));
app.use(express.urlencoded({ extended: true }));
app.use(morgan('dev'));

// Routes
// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// Blogs routes
// Get all Blogs
app.get('/blogs' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});

// Post a new blog
app.post('/blogs', (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
});

// Get a single blog
app.get('/blogs/:id', (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            console.log(err);
        });
});

// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

</details>

<details>
  <summary>53. Delete a Single blog with Route [/blogs/:id] </summary>

details.ejs:

```html
<html lang="en">
  <%- include("./partials/head.ejs") %>

  <body>
    <%- include("./partials/nav.ejs") %>

    <div class="details content">
      <h2><%= blog.title %></h2>
      <div class="content">
        <p><%= blog.body %></p>
      </div>
      <a class="delete" data-doc="<%= blog._id %>">delete</a>
    </div>

    <%- include("./partials/footer.ejs") %>

    <script>
      const trashcan = document.querySelector("a.delete");

      trashcan.addEventListener("click", (e) => {
        const endpoint = `/blogs/${trashcan.dataset.doc}`;

        fetch(endpoint, {
          method: "DELETE",
        })
          .then((response) => response.json())
          .then((data) => (window.location.href = data.redirect))
          .catch((err) => console.log(err));
      });
    </script>
  </body>
</html>
```

style.css:

```css
/* details styles */
.details {
  position: relative;
}
.delete {
  position: absolute;
  top: 0;
  right: 0;
  border-radius: 50%;
  padding: 8px;
}
.delete:hover {
  cursor: pointer;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
}
```

```Javascript
app.delete('/blogs/:id', (req, res) => {
  const id = req.params.id;

  Blog.findByIdAndDelete(id)
    .then(result => {
      res.json({ redirect: '/blogs' });
    })
    .catch(err => {
      console.log(err);
    });
});
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const Blog = require('./models/blog');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));
app.use(express.urlencoded({ extended: true }));
app.use(morgan('dev'));

// Routes
// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// Blogs routes
// render create blog page
app.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// Get all Blogs
app.get('/blogs' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});

// Post a new blog
app.post('/blogs', (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
});

// Get a single blog
app.get('/blogs/:id', (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            console.log(err);
        });
});

//Delete a single blog
app.delete('/blogs/:id', (req, res) => {
    const id = req.params.id;
    Blog.findByIdAndDelete(id)
        .then(result => {
        res.json({ redirect: '/blogs' });
        })
        .catch(err => {
        console.log(err);
        });
});

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

</details>

+EXPRESS ROUTER & MVC

<details>
  <summary>54. Create Express Router</summary>

routes/blogRoutes.js:

```Javascript
const express = require('express');
const Blog = require('../models/blog');

const router = express.Router();

// render create blog page
router.get('/blogs/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// Get all Blogs
router.get('/blogs' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});

// Post a new blog
router.post('/blogs', (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
});

// Get a single blog
router.get('/blogs/:id', (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            console.log(err);
        });
});

//Delete a single blog
router.delete('/blogs/:id', (req, res) => {
    const id = req.params.id;
    Blog.findByIdAndDelete(id)
        .then(result => {
        res.json({ redirect: '/blogs' });
        })
        .catch(err => {
        console.log(err);
        });
});

module.exports = router;
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const blogRoutes = require('./routes/blogRoutes');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));
app.use(express.urlencoded({ extended: true }));
app.use(morgan('dev'));

// Routes
// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// Blogs routes
app.use(blogRoutes);

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});
```

</details>

<details>
  <summary>55. Scoping the URL (Routing)</summary>

```Javascript
// Blogs routes
app.use('/blogs', blogRoutes);
```

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const blogRoutes = require('./routes/blogRoutes');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));
app.use(express.urlencoded({ extended: true }));
app.use(morgan('dev'));

// Routes
// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// Blogs routes
app.use('/blogs', blogRoutes);

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

routes/blogRoutes.js:

```Javascript
const express = require('express');
const Blog = require('../models/blog');

const router = express.Router();

// render create blog page
router.get('/create', (req, res) => {
    res.render('create', { title: 'Create a new blog' });
});

// Get all Blogs
router.get('/' , (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
});

// Post a new blog
router.post('/', (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
});

// Get a single blog
router.get('/:id', (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            console.log(err);
        });
});

//Delete a single blog
router.delete('/:id', (req, res) => {
    const id = req.params.id;
    Blog.findByIdAndDelete(id)
        .then(result => {
        res.json({ redirect: '/blogs' });
        })
        .catch(err => {
        console.log(err);
        });
});

module.exports = router;
```

</details>

<details>
  <summary>56. The MVC Structure</summary>

app.js:

```Javascript
const express = require('express');
const path = require('path');
const morgan = require('morgan')
const mongoose = require('mongoose');
const blogRoutes = require('./routes/blogRoutes');

// express app
const app = express();

// register view engine
app.set('view engine', 'ejs');

const dbURI = "mongodb+srv://<accountName>:<password>@cluster0.ujjnbjl.mongodb.net/<dbname>?retryWrites=true&w=majority";
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then((result) => {
        // listen for requests
        app.listen(3000);
        console.log('connected to db');
    })
    .catch((err) => console.log(err));

// static files
app.use(express.static('public'));
app.use(express.urlencoded({ extended: true }));
app.use(morgan('dev'));

// Routes
// get home page
app.get('/', (req, res) => {
    res.redirect('/blogs');
});

// get about page
app.get('/about', (req, res) => {
    res.render('about', { title: 'About' });
});

// Blogs routes
app.use('/blogs', blogRoutes);

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
    // res.sendFile('./views/404.html', { root: __dirname });
});

```

routes/blogRoutes.js:

```Javascript
const express = require('express');
const blogController = require('../controllers/blogController');

const router = express.Router();

// render create blog page
router.get('/create', blogController.blog_create_get);

// Get all Blogs
router.get('/', blogController.blog_index);

// Post a new blog
router.post('/', blogController.blog_create_post);

// Get a single blog
router.get('/:id', blogController.blog_details);

//Delete a single blog
router.delete('/:id', blogController.blog_delete);

module.exports = router;
```

controllers/blogController.js:

```Javascript
const Blog = require('../models/blog');

// Get all Blogs
const blog_index = (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
}

// Get a single blog
const blog_details = (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            console.log(err);
        });
}

// render create blog page
const blog_create_get = (req, res) => {
    res.render('create', { title: 'Create a new blog' });
}

// post a new blog
const blog_create_post = (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
}

//Delete a single blog
const blog_delete = (req, res) => {
    const id = req.params.id;
    Blog.findByIdAndDelete(id)
        .then(result => {
        res.json({ redirect: '/blogs' });
        })
        .catch(err => {
        console.log(err);
        });
}


module.exports = {
    blog_index,
    blog_details,
    blog_create_get,
    blog_create_post,
    blog_delete
}
```

</details>

<details>
  <summary>57. Add Trash Can for Delete Button</summary>

```Javascript
<div class="details content">
    <h2><%= blog.title %></h2>
    <div class="content">
        <p><%= blog.body %></p>
    </div>
    <a class="delete" data-doc="<%= blog._id %>">
        <img src="/trashcan.svg" alt="delete icon">
    </a>
</div>
```

views/details.ejs:

```Javascript
<html lang="en">
<%- include("./partials/head.ejs") %>

<body>
  <%- include("./partials/nav.ejs") %>

  <div class="details content">
    <h2><%= blog.title %></h2>
    <div class="content">
      <p><%= blog.body %></p>
    </div>
    <a class="delete" data-doc="<%= blog._id %>">
        <img src="/trashcan.svg" alt="delete icon">
    </a>
  </div>

  <%- include("./partials/footer.ejs") %>

  <script>
    const trashcan = document.querySelector('a.delete');

    trashcan.addEventListener('click', (e) => {
      const endpoint = `/blogs/${trashcan.dataset.doc}`;

      fetch(endpoint, {
        method: 'DELETE',
      })
      .then(response => response.json())
      .then(data => window.location.href = data.redirect)
      .catch(err => console.log(err));
    });

  </script>
</body>
</html>
```

</details>

<details>
  <summary>58. Correct 404 page rendering</summary>

```Javascript
// Get a single blog
const blog_details = (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            res.status(404).render('404', { title: 'Blog not found' });
        });
}
```

controllers/blogController.js:

```Javascript
// blog_index, blog_details, blog_create_get, blog_create_post, blog_delete

const Blog = require('../models/blog');

// Get all Blogs
const blog_index = (req, res) => {
    Blog.find({}).sort({ createdAt: -1 })
        .then((result) => {
            res.render('index', { title: 'All Blogs', blogs: result });
        })
        .catch((err) => {
            console.log(err);
        });
}

// Get a single blog
const blog_details = (req, res) => {
    const id = req.params.id;
    Blog.findById(id)
        .then((result) => {
            res.render('details', { blog: result, title: 'Blog Details' });
        })
        .catch((err) => {
            res.status(404).render('404', { title: 'Blog not found' });
        });
}

// render create blog page
const blog_create_get = (req, res) => {
    res.render('create', { title: 'Create a new blog' });
}

// post a new blog
const blog_create_post = (req, res) => {
    const blog = new Blog(req.body);
    blog.save()
        .then((result) => {
            res.redirect('/blogs');
        })
        .catch((err) => {
            console.log(err);
        });
}

//Delete a single blog
const blog_delete = (req, res) => {
    const id = req.params.id;
    Blog.findByIdAndDelete(id)
        .then(result => {
        res.json({ redirect: '/blogs' });
        })
        .catch(err => {
        console.log(err);
        });
}


module.exports = {
    blog_index,
    blog_details,
    blog_create_get,
    blog_create_post,
    blog_delete
}
```

</details>

### [2-NODE.JS TUTORIAL - DAVE GRAY](#)

+INTRODUCTION

<details>
  <summary>59. The Global Object</summary>

Check Node Version:

```bs
nvm install <version>
nvm use <version>
nvm ls

node -v
```

server.js:

```js
console.log("Hello world!");

console.log(global);
```

```bs
node server
```

```js
// Hello world!
// <ref *1> Object [global] {
//   global: [Circular *1],
//   clearInterval: [Function: clearInterval],
//   clearTimeout: [Function: clearTimeout],
//   setInterval: [Function: setInterval],
//   setTimeout: [Function: setTimeout] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   },
//   queueMicrotask: [Function: queueMicrotask],
//   performance: Performance {
//     nodeTiming: PerformanceNodeTiming {
//       name: 'node',
//       entryType: 'node',
//       startTime: 0,
//       duration: 115.58020782470703,
//       nodeStart: 26.828166007995605,
//       v8Start: 44.619500160217285,
//       bootstrapComplete: 102.09924983978271,
//       environment: 61.474082946777344,
//       loopStart: -1,
//       loopExit: -1,
//       idleTime: 0
//     },
//     timeOrigin: 1672901956430.907
//   },
//   clearImmediate: [Function: clearImmediate],
//   setImmediate: [Function: setImmediate] {
//     [Symbol(nodejs.util.promisify.custom)]: [Getter]
//   }
// }
```

</details>

<details>
  <summary>60. The OS Object</summary>

server.js:

```js
const os = require("os");

console.log(__dirname);
console.log(__filename);

console.log(os.type());
console.log(os.version());
console.log(os.homedir());

console.log(os.hostname());
console.log(os.platform());
console.log(os.userInfo());
console.log(os.release());
console.log(os.uptime());
console.log(os.arch());
console.log(os.cpus());
console.log(os.endianness());
console.log(os.freemem());
console.log(os.getPriority());
console.log(os.loadavg());
console.log(os.networkInterfaces());
console.log(os.totalmem());
```

```bs
node server
```

```bs
/Users/ifeanyiomeata/Desktop/SERVER/Cloud-React-Node/node-project
/Users/ifeanyiomeata/Desktop/SERVER/Cloud-React-Node/node-project/server.js

Darwin
Darwin Kernel Version 21.4.0
/Users/ifeanyiomeata
-------------------->
```

</details>

<details>
  <summary>61. The Path Object</summary>

server.js:

```js
const os = require("os");
const path = require("path");

console.log(__dirname);
console.log(__filename);

console.log(path.dirname(__filename));
console.log(path.basename(__filename));
console.log(path.extname(__filename));
console.log(path.parse(__filename));
```

```bs
node server
```

```bs
/Users/ifeanyiomeata/Desktop/SERVER/Cloud-React-Node/node-project
/Users/ifeanyiomeata/Desktop/SERVER/Cloud-React-Node/node-project/server.js

/Users/ifeanyiomeata/Desktop/SERVER/Cloud-React-Node/node-project
server.js
.js
{
  root: '/',
  dir: '/Users/ifeanyiomeata/Desktop/SERVER/Cloud-React-Node/node-project',
  base: 'server.js',
  ext: '.js',
  name: 'server'
}
```

</details>

<details>
  <summary>62. Create Object Modules</summary>

math.js:

```js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;
const multiply = (a, b) => a * b;
const divide = (a, b) => a / b;

module.exports = { add, subtract, multiply, divide };

// exports.add = (a, b) => a + b;
// exports.subtract = (a, b) => a - b;
// exports.multiply = (a, b) => a * b;
// exports.divide = (a, b) => a / b;
```

server.js:

```js
const os = require("os");
const path = require("path");
const { add, subtract, multiply, divide } = require("./math");

console.log(add(3, 2));
console.log(subtract(3, 2));
console.log(multiply(3, 2));
console.log(divide(3, 2));
```

```bs
node server
```

```js
// 5
// 1
// 6
// 1.5
```

</details>

<details>
  <summary>63. Read File - fs.readFile()</summary>

files/starter.txt:

```txt
Hello, my name is Ifeanyi.
```

index.js:

```js
const fs = require("fs");

fs.readFile("./files/starter.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
  //console.log(data.toString());
});

// exit on uncaught errors
process.on("uncaughtException", (err) => {
  console.error(`There was an uncaught error: ${err}`);
  process.exit(1);
});
```

```bs
node index
```

```js
// Hello, my name is Ifeanyi.
```

</details>

<details>
  <summary>64. Read File with Path Module - fs.readFile()</summary>

files/starter.txt:

```txt
Hello, my name is Ifeanyi.
```

index.js:

```js
const fs = require("fs");
const path = require("path");

fs.readFile(
  path.join(__dirname, "files", "starter.txt"),
  "utf8",
  (err, data) => {
    if (err) throw err;
    console.log(data);
    //console.log(data.toString());
  }
);

// exit on uncaught errors
process.on("uncaughtException", (err) => {
  console.error(`There was an uncaught error: ${err}`);
  process.exit(1);
});
```

```bs
node index
```

```js
// Hello, my name is Ifeanyi.
```

</details>

<details>
  <summary>65. Write File - fs.writeFile()</summary>

index.js:

```js
const fs = require("fs");
const path = require("path");

fs.writeFile(
  path.join(__dirname, "files", "reply.txt"),
  "Nice to meet you!",
  (err) => {
    if (err) throw err;
    console.log("Write Complete.");
  }
);

// exit on uncaught errors
process.on("uncaughtException", (err) => {
  console.error(`There was an uncaught error: ${err}`);
  process.exit(1);
});
```

```bs
node index
```

```js
// Write Complete.
```

</details>

<details>
  <summary>66. Update File - fs.appendFile()</summary>

index.js:

```js
const fs = require("fs");
const path = require("path");

fs.appendFile(
  path.join(__dirname, "files", "reappend.txt"),
  "Hello, Nice to meet you Again!",
  (err) => {
    if (err) throw err;
    console.log("Append Complete.");
  }
);

// exit on uncaught errors
process.on("uncaughtException", (err) => {
  console.error(`There was an uncaught error: ${err}`);
  process.exit(1);
});
```

```bs
node index
```

```js
// Append Complete.
```

</details>

<details>
  <summary>67. Write + Update File Sync order</summary>

index.js:

```js
const fs = require("fs");
const path = require("path");

//Write File
fs.writeFile(
  path.join(__dirname, "files", "reply.txt"),
  "Nice to meet you Bob!",
  (err) => {
    if (err) throw err;
    console.log("Write Complete.");

    //Append to File
    fs.appendFile(
      path.join(__dirname, "files", "reply.txt"),
      "\n\nYou really have a great car!",
      (err) => {
        if (err) throw err;
        console.log("Append Complete.");
      }
    );
  }
);

// exit on uncaught errors
process.on("uncaughtException", (err) => {
  console.error(`There was an uncaught error: ${err}`);
  process.exit(1);
});
```

```bs
node index
```

```js
// Write Complete.
// Append Complete.
```

files/reply.txt:

```txt
Nice to meet you Bob!

You really have a great car!
```

</details>

<details>
  <summary>68. Write + Update + Rename File Sync order</summary>

index.js:

```js
const fs = require("fs");
const path = require("path");

//Write File
fs.writeFile(
  path.join(__dirname, "files", "reply.txt"),
  "Nice to meet you Bob!",
  (err) => {
    if (err) throw err;
    console.log("Write Complete.");

    //Append to File
    fs.appendFile(
      path.join(__dirname, "files", "reply.txt"),
      "\n\nYou really have a great car!",
      (err) => {
        if (err) throw err;
        console.log("Append Complete.");

        //Rename File
        fs.rename(
          path.join(__dirname, "files", "reply.txt"),
          path.join(__dirname, "files", "newReply.txt"),
          (err) => {
            if (err) throw err;
            console.log("Rename Complete.");
          }
        );
      }
    );
  }
);

// exit on uncaught errors
process.on("uncaughtException", (err) => {
  console.error(`There was an uncaught error: ${err}`);
  process.exit(1);
});
```

```bs
node index
```

```js
// Write Complete.
// Append Complete.
// Rename Complete.
```

files/newReply.txt:

```txt
Nice to meet you Bob!

You really have a great car!
```

</details>

<details>
  <summary>69. Read File with Promises</summary>

starter.txt:

```txt
Hello, my name is Ifeanyi.
```

index.js:

```js
const fsPromises = require("fs").promises;
const path = require("path");

const fileOps = async () => {
  try {
    const data = await fsPromises.readFile(
      path.join(__dirname, "files", "starter.txt"),
      "utf8"
    );
    console.log(data);
  } catch (err) {
    console.error(err);
  }
};

fileOps();
```

```bs
node index
```

```js
// Hello, my name is Ifeanyi.
```

</details>

<details>
  <summary>70. Read + Delete + Write + Update + Rename File with Promises</summary>

starter.txt:

```txt
Hello, my name is Ifeanyi.
```

index.js:

```js
const fsPromises = require("fs").promises;
const path = require("path");

const fileOps = async () => {
  try {
    //Read File
    const data = await fsPromises.readFile(
      path.join(__dirname, "files", "starter.txt"),
      "utf8"
    );
    console.log("#### OLD ####");
    console.log(data);

    //Delete old File
    await fsPromises.unlink(path.join(__dirname, "files", "starter.txt"));

    //Write new File
    await fsPromises.writeFile(
      path.join(__dirname, "files", "promiseWrite.txt"),
      data
    );

    //Update new File
    await fsPromises.appendFile(
      path.join(__dirname, "files", "promiseWrite.txt"),
      "\n\nNice to meet you."
    );

    //Rename new File
    await fsPromises.rename(
      path.join(__dirname, "files", "promiseWrite.txt"),
      path.join(__dirname, "files", "promiseComplete.txt")
    );

    //Read the new File
    const newData = await fsPromises.readFile(
      path.join(__dirname, "files", "promiseComplete.txt"),
      "utf8"
    );
    console.log("#### NEW ####");
    console.log(newData);
  } catch (err) {
    console.error(err);
  }
};

fileOps();
```

```bs
node index
```

```js
// #### OLD ####
// Hello, my name is Ifeanyi.
// #### NEW ####
// Hello, my name is Ifeanyi.
//
// Nice to meet you.
```

files/promiseComplete.txt:

```txt
Hello, my name is Ifeanyi.

Nice to meet you.
```

</details>

<details>
  <summary>71. Read and Write streams for large files with DataChunks</summary>

stream.js:

```js
const fs = require("fs");
const path = require("path");

const rs = fs.createReadStream(path.join(__dirname, "files", "lorem.txt"), {
  encoding: "utf8",
});
const ws = fs.createWriteStream(path.join(__dirname, "files", "new-lorem.txt"));
let count = 0;

rs.on("data", (dataChunk) => {
  try {
    ws.write(dataChunk);
    count += 1;
    //   console.log(dataChunk);
  } catch (err) {
    console.error(err);
  } finally {
    console.log(`Completed Chunk: ${count}`);
  }
});
```

```bs
node stream
```

```js
// Completed Chunk: 1
// Completed Chunk: 2
// Completed Chunk: 3
// Completed Chunk: 4
// Completed Chunk: 5
// Completed Chunk: 6
// Completed Chunk: 7
// Completed Chunk: 8
// Completed Chunk: 9
// Completed Chunk: 10
// Completed Chunk: 11
// Completed Chunk: 12
// Completed Chunk: 13
// Completed Chunk: 14
// Completed Chunk: 15
// Completed Chunk: 16
// Completed Chunk: 17
// Completed Chunk: 18
// Completed Chunk: 19
// Completed Chunk: 20
// Completed Chunk: 21
// Completed Chunk: 22
// Completed Chunk: 23
// Completed Chunk: 24
// Completed Chunk: 25
// Completed Chunk: 26
// Completed Chunk: 27
// Completed Chunk: 28
// Completed Chunk: 29
// Completed Chunk: 30
```

</details>

<details>
  <summary>72. Piping Read streams to Write files </summary>

stream.js:

```js
const fs = require("fs");
const path = require("path");

const rs = fs.createReadStream(path.join(__dirname, "files", "lorem.txt"), {
  encoding: "utf8",
});
const ws = fs.createWriteStream(path.join(__dirname, "files", "new-lorem.txt"));

try {
  rs.pipe(ws);
} catch (err) {
  console.error(err);
} finally {
  console.log(`Completed Streaming.`);
}
```

```bs
node stream
```

```js
// Completed Streaming.
```

</details>

<details>
  <summary>73. Create Folder Directory</summary>

index.js:

```js
const fs = require("fs");

fs.mkdir("./newdir", (err) => {
  if (err) throw err;
  console.log("Directory created");
});
```

```bs
node index
```

```js
// Directory created
```

</details>

<details>
  <summary>74. Find out if Folder Directory Exists</summary>

index.js:

```js
const fs = require("fs");

if (!fs.existsSync("./newdir")) {
  fs.mkdir("./newdir", (err) => {
    if (err) throw err;
    console.log("Directory created");
  });
}
```

</details>

<details>
  <summary>75. Delete Folder Directory</summary>

index.js:

```js
const fs = require("fs");

if (fs.existsSync("./newdir")) {
  fs.rmdir("./newdir", (err) => {
    if (err) throw err;
    console.log("Directory deleted successfully");
  });
}
```

```bs
node index
```

```js
// Directory deleted successfully
```

</details>

<details>
  <summary>76. NPM Nodemon</summary>

Install Nodemon:

```bs
<!-- Global Dependency  -->
npm install -g nodemon

<!-- Production  -->
npm install --save nodemon
npm install -S nodemon

<!-- Development -->
npm install --save-dev nodemon
npm install -D nodemon
```

Set Scripts-

package.json:

```json
{
  "name": "project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index",
    "dev": "nodemon index"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "date-fns": "^2.29.3"
  },
  "devDependencies": {
    "nodemon": "^2.0.20"
  }
}
```

Start Nodemon Server:

```bs
npm run dev
OR
nodemon server.js
```

```js
// [nodemon] 2.0.20
// [nodemon] to restart at any time, enter `rs`
// [nodemon] watching path(s): *.*
// [nodemon] watching extensions: js,mjs,json
// [nodemon] starting `node server.js`
// 5
// 1
// 6
// 1.5
// [nodemon] clean exit - waiting for changes before restart
```

</details>

<details>
  <summary>77. NPM Date-fns</summary>

NPM Initialization:

```bs
npm init -y
```

Setup .gitignore -

.gitignore:

```bs
node_modules
```

Install date-fns:

```bs
npm install date-fns --save
npm install date-fns --S
```

Example:

```js
import { compareAsc, format } from "date-fns";

format(new Date(2014, 1, 11), "yyyy-MM-dd");
//=> '2014-02-11'

const dates = [
  new Date(1995, 6, 2),
  new Date(1987, 1, 11),
  new Date(1989, 6, 10),
];
dates.sort(compareAsc);
//=> [
//   Wed Feb 11 1987 00:00:00,
//   Mon Jul 10 1989 00:00:00,
//   Sun Jul 02 1995 00:00:00
// ]
```

server.js:

```js
const { format } = require("date-fns");

console.log(format(new Date(), "yyyyMMdd\tHH:mm:ss"));
```

```js
// 20230105        15:11:20
```

</details>

<details>
  <summary>78. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>79. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>80. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>81. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>82. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>83. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>84. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>85. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>86. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>87. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>88. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>89. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>90. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>91. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>92. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>93. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>94. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>95. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>96. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>97. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>98. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>99. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>

<details>
  <summary>100. Sample</summary>

```bs

```

```js

```

```js

```

```js

```

```js

```

</details>
