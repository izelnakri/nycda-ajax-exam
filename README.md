Instructions:

- Add your answers inline to the markdown file.
- Use your own words.
- Come up with an answer from memory. Write it down, even if the answer is "I don't know."
- Then, we will go over the answers in class. Write down your revised answer below your original answer.
- There are two intermissions. We will go over the answers to the previous parts during those times.
- Finally, submit all of your answers in a file to canvas. This is so Lloyd and I can get a sense of your understanding.

---
### Part 1: Servers - 20 minutes

1. What is a server? What does a server do?
Server is a computed. A HTTP server is computer program that listens to HTTP requests and responds with data.

2. What is Node.js?
It is a JavaScript runtime that lets us run JS programs in our computers.

3. What is express?
Express is a node module/library that lets us create HTTP servers easily.

4. What is a client? What does a client do?
Client is the party that makes HTTP Requests. It is either a browser, or a program that makes HTTP Requests.

5. How do the server and the client communicate?
Through HTTP Protocol. Client makes an HTTP Request with a header and body(empty if its GET), then server gives an HTTP Response with header and body(actual response content).

6. Debugging:
- 6a. How do you view server logs? In the terminal. (All the logs morgan package generate or our console.log()'s in node)
- 6b. How do you view client logs? Browser console, via developers tools.

---
### Part 2: HTTP Requests - 15 minutes

1. What is an HTTP Request?
It is a request from a client to the server with header and body. Request finishes when server gives a response.

2. GET Requests
- 2a. What is a GET request? It is an HTTP method for obtaining data or files from the server. It could be a webpage, file or JSON data.

- 2b. When do you use GET requests? ^^

- 2c. How do you send data in a GET request?
We don't send any valuable data with GET requests, although the client will send some HTTP Request Header as the meta information of a request.

3. POST Requests
- 3a. What is a POST request?
It is an HTTP method for posting/creating some data on the server.

- 3b. When do you use POST requests?
When we want to create a new resource on the server.

- 3c. How do you send data in a POST request?
When a user clicks on submit on a web form, web browser will fire a POST request. Also, you can fire POST request via ajax($.get()) in your browser.

---

### Intermission

---
### Part 3: Ajax - 15 minutes

1. Ajax
- 1a. What is Ajax?
Ajax stands for Asynchronous JavaScript and XML. It is an HTTP request that get initiated from a browser JavaScript.

- 1b. When should you use Ajax?
When we want to obtain or send data without reloading a page.

2. Given the following code snippet:

```js
console.log("A");
$('#map').click(function(event) {
	console.log("B");
	var coordinates = convertMouseCoordinatesToGeoCoordinates(event);

	console.log("C");
	$.get('/map', { lat: coordinates.x, lon: coordinates.y }, function(response, status) {
		console.log("D");
		mapDisplay.update(response);
	});

	console.log("E");
});
console.log("F");
```

- 2a. Describe what seems to be happening.
We would like to update the map display whenever use clicks on the element that has map id. When a user clicks on the map we update the coordinates based on the cursor location of the user and then we update the displayed map.

- 2b. In what order is `A` through `F` printed?
A - F - B - C - E - D

- 2c. Describe the events that happen between each letter. When does the server get hit?
1- browser prints 'A'.
2 - Then it puts a click listener on '#map' with a callback function.
3 - browser prints 'F'.
======
When a user clicks on the '#map':
======
4 - Browser prints 'B', then:
5 - convertMouseCoordinatesToGeoCoordinates function runs and returned value is saved to coordinates variable
6 - browser prints 'C'
7 - Browser makes an AJAX get request to /map with latitudes and longitudes passed in as query parameters
8 - browser prints 'E'
9 - When AJAX get request to /map finishes, browser prints 'D' and it updates the mapDisplay with response

---

### Intermission

---
### Part 4: Jade - 20 minutes

1. Jade
- 1a. What is Jade?
Jade/Pug is a rendering engine/templating language that has a terse syntax.

- 1b. Why should we use Jade?
Jade lets us put logic on our views, thus we can have more dynamic web pages. Our pages could receive data from the server,
display different html tags based on the data/logic. After server finishes rendering all our Pug/Jade code will get turned into an html string that server can send back to client.

2. Explain the difference between 'server side' JavaScript and 'client side' JavaScript.
Server side JavaScript is the JS code that runs on the server with Node.js .
Client side JS is the JS code that runs on the browser via the browsers JS engine.

3. Given this example `index.jade` file:

```js
doctype html
html
	head
		script(src='boop.js')
		script.
			var x = 1;
	body
		- var y = 2;
		h2= z + y
```

- 3a. Is `x` executed server side or client side? Does the client ever see `x`?
  x will get executed on the client side. Client will see x since it is inside a <script> tag and runs in inside the browser.

- 3b. Is `y` executed server side or client side? Does the client ever see `y`?
y will be executed on the server side. Server will run that code during rendering and client will never see the y.

- 3c. Is `z` executed server side or client side? Does the client ever see `z`?
z will be executed on the server side. Client will never see the z however it will see the result of z + y operation. Z is based on what we pass in to the template from our server during rendering.

- 3d. When is `boop.js` executed? Does the client ever see `boop.js`?
boop.js will be read when browser downloads the html of a page. As soon as browser sees the src of a script tag it will try to download that script and will try to run it. In other words browser will download boop.js and run it.

---
### Part 5: Request Lifecycle - 15 minutes

5. Given the following code snippet in an express application:

```js
app.get('/home', function (request, response) {
	response.render('index', { z: 3 } );
});
```

- 5a. List the complete order of events, starting from the browser making a `GET` request to `/home`. Assume that `index` refers to the Jade file in Part 4. Be sure to describe when each JavaScript statement (`x`, `y`, `z`, and `boop.js`) gets executed.

The code above tells our express server to listen to GET /home requests. During that request our callback code will run. Our server will try to render the index.pug template and will pass 3 as 'z' to the pug template before rendering. After that server will send the html string that gets returned from the render() function to the client and HTTP Response body.

- 5b. What is displayed on the page?
It will be a second header styled '5'

- 5c. What is visible from 'view page source'?
The HTTP Response body of the request. In other words the actual response of the server. This is what browser sees when the request finishes.
