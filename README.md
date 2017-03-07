# JavaScript-Convention

Extend JavaScript through convention.

## Constants with Upper Case

Always assume that uppercase varaibles are constant. 
As a rule, don't try to update/modify them on run time.

``` JavaScript
var IS_DEBUG = false;
var VERSION = '1.0';
var PI = 3.1415;
```
## Default Values with Null Comparison

Check the expression against null using the equality operator.
When using the equality operator, checking for null also checks for undefined.

```JavaScript
var DEBUG = (DEBUG != null) ? DEBUG : false;

if (window.key == null) window.key = 'default';

function foo(name) {
  if (name == null) name = 'defalut name';
}
```

## Default Value for Reference Types with the Or Operator

The Or operator returns the first none false expression, or the last (right most) expression.

The value of false, 0, empty string, undefined or null results to a false expression.
This effectively only useful for arrays, objects and functions since undefined or null are its only false value.

``` JavaScript
// Variable
var option = option || {};

window.key = window.key || [];

function foo(callback) {
  callback = callback || function() {};
}
```

## Namespaces with Object Notation

Create a new object (easily using object notation) for namespaces.
Functions and variable which belong to that namespace is defined as key-value pair for that object. 

``` JavaScript
ns = {
  PI: 3.1415,
  getCircumference: function(radius) {
    return 2 * ns.PI * radius;
  }
};
```

``` JavaScript
// Reusing existing namespace
window.ns = window.ns || {};

// Adding to an existing namespace
ns.getArea: function(radius) {
  return ns.PI * radius * radius;
};
```

## Labeled Arguments with Object

Pass and object as an argument.
The object's key value pair shall represent the paramete where the key acts as the label.

``` JavaScript
window.ns = window.ns || {};

ns.foo = function(arg) {
  return arg.x * arg.y;
}

ns.foo({ x: 1, y: 2 });
```

## Singletons with Object Notation

Build with an object notation and assigned to a variable.

``` JavaScript
window.ns = window.ns || {};

ns.singleton = {
  
  // Property
  name: 'mySingleton',
  
  // Method
  setName: function(newName) {
    this.name = newName;
  }
}

console.log(ns.singleton.name); // 'mySingleton'
ns.singleton.setName('yourSingleton');
console.log(ns.singleton.name); // 'yourSingleton'
```

## Class with Prototype

Use the original official way of creating classes in JavaScript.
Define the properties inside the constructor.
Define the methods through prototype.

``` JavaScript
window.ns = window.ns || {};

// Class MyClass
ns.MyClass = (function() {
  
  // Constructor
  var MyClass = function() {
    
    // Property
    this.name = 'myClass'
  };
  
  // Method
  MyClass.prototype.setName = function(newName) {
    this.name = newName;
  };
  
  return MyClass;
})();

ns.newClass = new ns.MyClass();
console.log(ns.newClass.name); // 'myClass'
ns.newClass.setName('yourClass');
console.log(ns.newClass.name); // 'yourClass'
```

## Sub Classing with Direct Reference

``` JavaScript
window.ns = window.ns || {};

// Class MyClass
ns.MyClass = (function() {
  
  // Constructor
  var MyClass = function() {};
  
  // Method
  MyClass.prototype.fooOne = function() {};
  
  return MyClass;
})();

// Class MySubClass
ns.MySubClass = (function() {
  
  // Constructor
  var MySubClass = function() {
    
    // Super Class Constructor
    na.MyClass.call(this);
  };
  
  // Inheritance
  MySubClass.prototype = new na.MyClass();
  MySubClass.prototype.constructor = MySubClass;
  
  // New Method
  MySubClass.prototype.fooTwo = function() {};
  
  // Method Override
  MySubClass.prototype.fooOne = function() {
    
    // Super Class Method
    na.MyClass.prototype.fooOne.call(this);
  };
  
  return MySubClass;
})();
```
## Events and Event Handlers with Array of Functions

Create a new property of type array of functions to represent the event and to hold the event handlers.
To represent the event, give the new property the event's name.
To 'trigger' the event, loop through the array and run each function providing the right arguments.

``` JavaScript
window.ns = window.ns || {};

ns.myObject = {

  // Event
  initialize: [],
  
  // Method
  initializer: function(data) {
  
    // Trigger Event
    this.initialize.forEach(function(handler) {
      handler.call(handler, data);
    });
  }
}

ns.myObject.initialize.push(function(data) {
  console.log(data);
});

ns.myObject.initializer('Hello World');
```





