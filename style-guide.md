## Punctuation, Spacing, Linebreaks

Too little spacing makes code cramped and claustrophobic.

```javascript
// no good

if(condition) doSomething();

while(iterator) iterator--; 

for(var i=0; i<100; i++) doSomething();
```
Let your code [breathe](https://www.youtube.com/watch?v=e8zRiaLOkfc&feature=kp)!

```javascript
// much better
if ( condition ) {
  doSomething();
}

while ( iterator ) {
  iterator--;
}

// var statement here isn't ideal, keep reading...
for ( var i = 0; i < 100; i++ ) {
  doSomething();
}
```

All blocks should use curly braces. They're optional for one-liners, but leaving off braces can introduce ambiguity. Further, if you add to a block later then you need to be sure to add braces. Better to just do it up front.

Leave spaces even between consecutive parens.

```javascript
while ( returnsBool( val ) ) {
  // makes it easier to count your parens
}

while ( returnsBool( val )) {
  // can get a little funky with more nesting
}
```

However... when you have consecutive punctuation that aren't the same, condense.

```javascript
// nope
myFunction( { param: "someValue" } );
myOtherFn( [ "value1", "value2" ] );

// yep
myFunction({ param: "someValue" });
myOtherFn([ "value1", "value2" ]);
```


## Declaration and Assignment

Each variable should get it's own `var`. Using commas is error-prone. Suck it up and just type out `v`-`a`-`r`.

```javascript
// no good
var example = function() {
  var num = 1,
      ltr = "a";
};


// SO good
var example = function() {
  var num = 1;
  var ltr = "a";
};
```

All `var` statements should be at the top of the function scope.

```javascript
// no good
var example = function() {
  // statements ...

  var num = 1;
  var ltr = "a";
};


// SO good
var example = function() {
  var num = 1;
  var ltr = "a";

  // statements ...
};
```

ECMA6 block-level declarations (`let` and `const`) should likewise occur at the top of _their_ scope, i.e. the block. Prefer `let` over `var` when it becomes feasible. 

Try to avoid function declarations. Hoisting weirdness is hard to debug.

```
// not so good
function myFn() {}

// oh yeah
var myFn = function() {};
```

## Literals and Nesting
For object literals, put the colon directly next to the property name.

```javascript
// naw
var obj = {
  someProp : "someValue",
  someOtherProp : "anotherValue"
};

// yee-haw
var obj = {
  someProp: "someValue",
  someOtherProp: "anotherValue"
};
```

Don't open or close too many braces or brackets at once. Use newlines. C'mon now, let it breathe. Just be sensible.

```javascript
// yuck
var collection = [{ key: "value", 
  colors: ["green", "blue"]
}, { key: "otherValue",
  colors: ["red", "orange"]
}];

// so pretty
var collection = [
  { 
    key: "value", 
    colors: [ "green", "blue" ]
  }, { 
    key: "otherValue",
    colors: [ "red", "orange" ]
   }
];
```

## Classes and Inheritance

Wrap your classes in an [IIFE](). It's not really necessary but it helps keep the code in a logical bundle, and is also nice for subclassing. It's ok to use a function declaration here; it helps draw attention to the constructor, and it should _always_ be the first thing in the IIFE anyway. This is inspired by the compiled JS from CoffeeScript `class` declarations.

```javascript
var Person = (function() {
  
  function Person( name ) {
    this.name = name;
  }

  Person.prototype.work = function() {
    // awesome method code
  };

  return Person;

})();
```

Use `Object.create` for subclassing. Use a polyfill if you're worried about older browsers. When subclassing, pass the superclass constructor into the IIFE.

```javascript
var Child = (function( _super ) {
  
  function Child( name ) {
    this.name = name;
  }

  Child.prototype = Object.create( _super.prototype );

  Child.prototype.play = function() {
    // awesome method code
  };

  return Child;

})( Person );
```

When it becomes possible, or if you're compiling ES6 code to ES5, go ahead and use the new `class` syntax.

## Iteration
Totally optional.

Prefer `Array.prototype` methods over everything else! Use a polyfill for `Object.keys` if you need it. Yes, `forEach` and friends are somewhat slower than a `for` loop, but don't prematurely optimize. Plus, you get closure scope for free with the `Array.prototype` iterators, which can come in handy.

```javascript
// bad
for ( var i = 0; i < arr.length; i++ ) {
  // code
}

var key;
for ( key in obj ) {
  if ( Object.hasOwnProperty( key ) ) {
    // code
  }
}

// good
arr.forEach( function( item ) {
  // code
});

Object.keys( obj ).forEach( function( key ) {
  // code
});
```