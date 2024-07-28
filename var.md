# Var

The `var` statement declares function-scoped or globally-scoped variables, optionally initializing each to a value.

Importantly, other block constructs, including `block statements`, `try...catch`, `switch`, headers of `one of the for statements`, do not create scopes for var, and variables declared with var inside such a block can continue to be referenced outside the block.

## Hoisting

`var` declarations, wherever they occur in a script, are processed before any code within the script is executed. Declaring a variable anywhere in the code is equivalent to declaring it at the top. This also means that a variable can appear to be used before it's declared. This behavior is called hoisting, as it appears that the variable declaration is moved to the top of the function, static initialization block, or script source in which it occurs.

Only a variable's declaration is hoisted, not its initialization. The initialization happens only when the assignment statement is reached. Until then the variable remains `undefined` (but declared):

```javascript
function doSomething() {
    console.log(bar); // undefined
    var bar = 111;
    console.log(bar); // 111
}
```

## Redeclarations

Duplicate variable declarations using `var` will not trigger an error, even in strict mode, and the variable will not lose its value, unless the declaration has an initializer.

```javascript
var a = 1;
var a = 2;
console.log(a); // 2
var a;
console.log(a); // 2; not undefined
```

`var` declarations can also be in the same scope as a function declaration. In this case, the var declaration's initializer always overrides the function's value, regardless of their relative position. This is because function declarations are hoisted before any initializer gets evaluated, so the initializer comes later and overrides the value.

```javascript
var a = 1;
function a() {}
console.log(a); // 1
```

A `var` declaration within a function's body can have the same name as a parameter.

```javascript
function foo(a) {
    var a = 1;
    console.log(a);
}

foo(2); // Logs 1
```

A `var` declaration within a `catch` block can have the same name as the `catch`-bound identifier, but only if the `catch` binding is a simple identifier, not a destructuring pattern. This is a `deprecated syntax` and you should not rely on it. In this case, the declaration is hoisted to outside the `catch` block, but any value assigned within the `catch` block is not visible outside.

```javascript
try {
    throw 1;
} catch (e) {
    var e = 2; // Works
}
console.log(e); // undefined
```
