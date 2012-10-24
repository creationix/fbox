# FBox

A simple flexbox style component for laying out a page using CSS absolute positioning and fixed width and height.

## Install

```sh
component install creationix/fbox
```

## Usage

```js
var HBox = require('fbox').HBox;
var VBox = require('fbox').VBox;

// The minimal interface to work as fbox items
function Cell() {
  // Must export your root element as this.el
  this.el = document.createElement("div");
}
// Must respond to resize commands and set your own width and height
// The offset (top or left) will be set by fbox
Cell.prototype.resize = function (width, height) {
  this.el.style.width = width + "px";
  this.el.style.height = height + "px";
};

var box = new HBox();
// el will be created if not passed in via the constructor
document.body.appendChild(box.el);

// positive values are absolute sizes
box.add(new Cell(), 200);
// Negative values are flex ratios
box.add(new Cell(), -1);
box.add(new Cell(), -2);
// Tell box to resize itself and it's children
box.resize(500, 200);
// the sizes are now [200, 100, 200]

// fboxes can be nested in eachother
var vbox = new fbox.VBox();
vbox.add(new Cell());
vbox.add(new Cell());
box.add(vbox, -1);

// Items can be removed by index as well
box.remove(1);
```
