# Node-Tutorial
Learn NodeJS by Ifeanyi Omeata

## Tutorial

---

### [1-NODE CRASH COURSE 1 - NET NINJA](#)

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
  <summary>8. Sample</summary>

```Javascript

```

```Javascript

```

```Javascript

```

</details>

<details>
  <summary>9. Sample</summary>

```Javascript

```

```Javascript

```

```Javascript

```

</details>

<details>
  <summary>10. Sample</summary>

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
