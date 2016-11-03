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

A server is like an operator handling routes between HTTP request and responses.

2. What is Node.js?

A js framework that makes it possible to run js without a browser. It can be used to create a server application.  

3. What is express?
Is a node.js library for creating server applications.

4. What is a client? What does a client do?
Client makes the request the server responds to.

5. How do the server and the client communicate?
Via HTTP.

6. Debugging:
- 6a. How do you view server logs?
Install the morgan package.

- 6b. How do you view client logs?
Godgle Dev tools.

---
### Part 2: HTTP Requests - 15 minutes

1. What is an HTTP Request?
A call for response from the server.

2. GET Requests
- 2a. What is a GET request?
We want to read something from the server

- 2b. When do you use GET requests?
when we want read data from the server to be rendered.

- 2c. How do you send data in a GET request?
app.get('path', (request, response) => {
	some callback function
}

3. POST Requests
- 3a. What is a POST request?
A http method
- 3b. When do you use POST requests?
When we want to write or edit something on the server side.
- 3c. How do you send data in a POST request?
app.post('path', (callback) => {
	some callback function
}
---

### Intermission

---
### Part 3: Ajax - 15 minutes

1. Ajax
- 1a. What is Ajax?
ajax is a technique for doing HTTP response/request.

- 1b. When should you use Ajax?
When we need to post or get data from the server side to the client side without updating the browser.  

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
Dependning on how the mouse curser moves in a div, geo coordinates get updated and displayed in the browser seamlessly.

- 2b. In what order is `A` through `F` printed?
A & F, B & C & E, D

- 2c. Describe the events that happen between each letter. When does the server get hit?

console.log('a');  
There is a jQuery listener to a click that runs a functions that converts mouse position to geo coordinates and

console.log('b');  
the click has happen, we denounce a var which hold a function that to the mouse position to geo coordinates conversion.

console.log('c');  
Here we get the geo coordinates from the server and update

console.log('d');
the map display div.

conosle.log('e');
we log to conosle when the update of map div is finished.

---

### Intermission

---
### Part 4: Jade - 20 minutes

1. Jade
- 1a. What is Jade?
A template engine that renders what is called "views" from the model view controller abstraction.

- 1b. Why should we use Jade?
Beacause intendation is AMAZING and static sites SUCKS compared to the puggies in that pug allows us to INCLUDE, EXTEND and use BLOCK to make rendering stuff a really fast process which will save us time and increase our margin of profit.

2. Explain the difference between 'server side' JavaScript and 'client side' JavaScript.

client side manipulates the DOM where server side maniuplates the functionality of routings in the HTTP response/request cyle.   

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

depends if what we tell node and express to do in index.js, but lets say that we have set the template engine to jade, and that the folder where index.jade is located is set to be the root dir, then yes, becase its in a script tag.

- 3b. Is `y` executed server side or client side? Does the client ever see `y`?
client side, we can se the y value if we console.log it.

- 3c. Is `z` executed server side or client side? Does the client ever see `z`?
it's not js. it will get printed out as html?

- 3d. When is `boop.js` executed? Does the client ever see `boop.js`?

Like if we have it in a public dir and link it up like a css like we do here, yeah.

---
### Part 5: Request Lifecycle - 15 minutes

5. Given the following code snippet in an express application:

```js
app.get('/home', function (request, response) {
	response.render('index', { z: 3 } );
});
```


- 5a. List the complete order of events, starting from the browser making a `GET` request to `/home`. Assume that `index` refers to the Jade file in Part 4. Be sure to describe when each JavaScript statement (`x`, `y`, `z`, and `boop.js`) gets executed.

we use HTTP method to get things from the home dir, we rina callback function that takes a string and a object as parameters.

- 5b. What is displayed on the page?
whatever the output from the function render has from the input.

- 5c. What is visible from 'view page source'?

.. everything?
