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
