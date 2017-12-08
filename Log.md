# Novemember 28th 2017 :octocat:
------------------------------------------------------------------------------------------------------------------------------------------
## What We've Learnt

We learned how to create our own host.

We drew ellipses that follow the mouse on one canvas

## What We Still Don't Know
> How to share the server between us :metal:

> How to all edit at the same time :heart:

## Creative Ideas
Put in a Nature Of Code

ex: Click and then it adds an object that spirals around.

We think that a mousex, mousey type of code would create too many glitches since there would be 4 contributors at a time.

## Our Code

### Sketch.js:
function setup() {

	createCanvas(windowWidth, windowHeight);
  
}

function draw() {

	fill(random(255), random(255), random(255));
  
	ellipse(mouseX, mouseY, 30, 30);
  
}

### Index.html:

### Server.js:
var express = require('express');

var app = express();

var server = app.listen(3000);

app.use(express.static('public'));

console.log("Running");


# Novemember 30th 2017 :octocat:
------------------------------------------------------------------------------------------------------------------------------------------
## What We've Learnt
Sockets
-Sending and receiving data


## What We Still Don't Know
How to run it from two different computers

## Creative Ideas
Herouku
(Shiffman videos on twtter bots)

## Our Code

### Sketch.js:
var socket;
function setup() {
	createCanvas(windowWidth, windowHeight);
	socket = io.connect('http://localhost:3000');
	socket.on('mouse', newDrawing);
}

function newDrawing(data){
	noStroke();
	fill(random(255), data.x, data.y);
	ellipse(data.x, data.y, 30, 30);
}

function mouseDragged(){
	console.log('Sending: ' + mouseX + ',' + mouseY);

	var data ={
		x: mouseX,
		y: mouseY
	}

	socket.emit('mouse', data);

	noStroke();
	fill(random(255), mouseX, mouseY);
	ellipse(mouseX, mouseY, 30, 30);
}

function draw() {
}


### Index.html:
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1">

	<title>our_server</title>

	<script src="../libraries/p5.js"></script>
	<script src="../libraries/p5.dom.js"></script>
	<script src="../libraries/p5.sound.js"></script>
	<script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
	<script src="sketch.js"></script>

	<style>
		body {
      margin:0;
			margin-left:45px;
			padding:0;
			overflow: hidden;
		}
		canvas {
			margin:auto;
		}
	</style>
</head>
<body>
</body>
</html>

### Server.js:
var express = require('express');

var app = express();
var server = app.listen(3000);

app.use(express.static('public'));

console.log("Running");

var socket = require('socket.io');

var io = socket(server);

io.sockets.on('connection', newConnection);

function newConnection(socket){
    console.log(newConnection + socket.id);
    socket.on('mouse', mouseMessage);

    function mouseMessage(data){
      socket.broadcast.emit('mouse', data);
      console.log(data);
    }
}

# December 8th 2017 :octocat:
------------------------------------------------------------------------------------------------------------------------------------------
## What We've Learnt
- How to use nature of code with our canvases


## What We Still Don't Know
- How to make it so that the walkers walk in the same direction (probably using multiple sockets?)

## Creative Ideas
Herouku
(Shiffman videos on twtter bots)

## Our Code

### Sketch.js:
var socket;

function setup() {
	createCanvas(windowWidth, windowHeight);
	background(50, 50, 50);
	socket = io.connect('http://localhost:3000');
	socket.on('mouse', newDrawing);
}
var Walker = function(x, y, c) {
    this.position = createVector(x, y);
    this.colour = c;
}

Walker.prototype.display = function() {
    strokeWeight(3);
    stroke(this.colour, random(255),random(255));
    point(this.position.x, this.position.y);
}

Walker.prototype.walk = function() {
    var StepSize = createVector(random(-5, 5),random(-5, 5));
    this.position.add(StepSize);
}

var w = [];
var i = 0;

function mousePressed(){
	console.log('Sending: ' + mouseX + ',' + mouseY);
	w[i] = new Walker(mouseX, mouseY, random(255));
	i++;
	var data ={
		x: mouseX,
		y: mouseY
	}

	socket.emit('mouse', data);

}

function newDrawing(data){
	w[i] = new Walker(data.x, data.y, random(255));
	i++;
}

draw = function() {
    for (var z = 0; z <w.length; z++){
        w[z].walk();
        w[z].display();
    }
}
### Index.html:
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1">

	<title>our_server</title>

	<script src="../libraries/p5.js"></script>
	<script src="../libraries/p5.dom.js"></script>
	<script src="../libraries/p5.sound.js"></script>
	<script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
	<script src="sketch.js"></script>

	<style>
		body {
      margin:0;
			margin-left:45px;
			padding:0;
			overflow: hidden;
		}
		canvas {
			margin:auto;
		}
	</style>
</head>
<body>
</body>
</html>

### Server.js:
var express = require('express');

var app = express();
var server = app.listen(3000);

app.use(express.static('public'));

console.log("Running");

var socket = require('socket.io');

var io = socket(server);

io.sockets.on('connection', newConnection);

function newConnection(socket){
    console.log(newConnection + socket.id);
    socket.on('mouse', mouseMessage);

    function mouseMessage(data){
      socket.broadcast.emit('mouse', data);
      console.log(data);
    }
}


