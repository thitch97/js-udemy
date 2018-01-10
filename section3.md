# Udemy JS Course - Section 3

## Comparison Operators
```javascript
console.log(3 < 2 < 1);
```

When this is run, the expression is evaluated left to right since the operators have the same precedence.

This means that "3 < 2" is evaluated and false is returned. thus, we are left with (false < 1). 'false' is coerced to 0, which is less than 1. Therefore 0 < 1 returns false.

In order to prevent unexpected behaviour, it is safer to use the "strict" versions of comparison operators.

These include: strict equality "===" & strict inequality "!=="

These operators compare operands without coercion.

## Existence

Javascript coerces expressions of nonexistence to false for evaluation
One problem that this could cause is that 0 is also coerced to false, even though 0 is not necessarily an indication of nonexistence. In such cases, it may be necessary to implement the following:

```javascript
var a;

a = 0;

if (a || a === 0) {
  
  console.log("Something is there");
}
```
