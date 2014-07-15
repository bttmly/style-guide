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

```javascript

while ( returnsBool( val ) ) {
  // makes it easier to count your parens
}

while ( returnsBool( val ))


```

## Declaration and Assignment

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