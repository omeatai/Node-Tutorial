# Node-Tutorial
Learn NodeJS by Ifeanyi Omeata

## Tutorial

---

### [1-NODE CRASH COURSE 1 - NET NINJA](#)

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
  <summary>18. Status Codes/summary>

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

```

</details>

<details>
  <summary>19. Sample</summary>

```Javascript

```

```Javascript

```

```Javascript

```

</details>

<details>
  <summary>20. Sample</summary>

```Javascript

```

```Javascript

```

```Javascript

```

</details>


### [2-NODE CRASH COURSE 2 - NET NINJA](#)

<details>
  <summary>1. Sample</summary>

```Javascript

```

```Javascript

```

```Javascript

```

```Javascript

```

</details>
