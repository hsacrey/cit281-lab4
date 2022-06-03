## Lab 4

In this lab, I created my first Fastify Node.js web server, initialized it as a Node.js project folder using Node Package Manager (npm), and added Fastify to the project using npm.
I also added a second route with query parameters.

#### p4-data.js:
```javascript
// Require the Fastify framework and instantiate it
const fastify = require("fastify")();
// Handle GET verb for / route using Fastify
// Note use of "chain" dot notation syntax
fastify.get("/", (request, reply) => {
  reply
    .code(200)
    .header("Content-Type", "text/html; charset=utf-8")
    .send("<h1>Hello from Lab 4!</h1>");
});
fastify.get("/name", (request, reply) => {
    console.log("Query Object:", request.query);
    let first = request.query.first;
    let last = request.query.last;
    //ALTERNATIVE: const{first, last} = request.query;
    const name =  (first && last) ? `${first} ${last}` : "Guest";
    reply
    .code(200)
    .header("Content-Type", "text/html; charset=utf-8")
    .send(`<h1>Hello ${name}!</h1>`);

});
fastify.get("/cit", (request, reply) => {
  console.log("Query Object:", request.query);
  reply
  .code(200)
  .header("Content-Type", "text/html; charset=utf-8")
  .send(`<h1>Hello!</h1>`);

});
fastify.get("/cit/student/:id", (request, reply) => {
  console.log("Query Object:", request.params);
  console.log('id:', request.params.id)
  reply
  .code(200)
  .header("Content-Type", "text/html; charset=utf-8")
  .send("ID:" + request.params.id);
});
fastify.get("*", (request, reply) => {
  console.log("Query Object:", request.params);
  console.log('id:', request.params.id)
  reply
  .code(404)
  .header("Content-Type", "application.html; charset=utf-8")
  .send("<h1>PATH NOT FOUND >:(</h1>");
});
// Start server and listen to requests using Fastify
const listenIP = "localhost";
const listenPort = 8080;
fastify.listen(listenPort, listenIP, (err, address) => {
  if (err) {
    console.log(err);
    process.exit(1);
  }
  console.log(`Server listening on ${address}`);
});

```
