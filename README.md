# Node-Tutorial
Learn NodeJS by Ifeanyi Omeata

## Tutorial

---

### [1-NODE CRASH COURSE 1 - NET NINJA](#)

<details>
  <summary>1. How to use Fetch with json</summary>

```Javascript
fetch('http://example.com/movies.json')
  .then((response) => response.json())
  .then((data) => console.log(data));
```

```Javascript
var myRequest = new Request('products.json');//GET
var myRequest = new Request('products.json', {method: "post"});//POST

fetch(myRequest)
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(console.error);
```

</details>



