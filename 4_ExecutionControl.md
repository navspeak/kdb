https://code.kx.com/q4m3/A_Built-in_Functions/#a88-ssr

## The general template of the if statement is
  - if[cond; expr1; expr2; ...; exprN]
  - If the condition is true then all expressions are evaluated.
```
q)a:b:0
q)if[a>0; b:10] /- false condition
q)b
0 /- assignment not executed
q)if[a=0;b:10] /- true condition
q)b
10 /- assignment executed
```
  - The condition can be a numerical value - zero evaluates to false, nonzero evaluates to true.
  - if does not return a value
  
## The general template of if-else is
   - $[cond1; expr1; cond2; expr2; ... ; falseexpr]
   - If cond1 is true, expr1 is executed, else-if cond2 is true, expr2 is executed.
   - Once a true condition is met, no other conditions are evaluated.
   - If all conditions are false then falseexpr is executed.
 
``` 
q)a:1
q)$[a<0; b:10; a>0; b:20; b:30] /- a>0
q)b
20 /- second assignment executed
```
  - A value is returned in an if-else statement.
```
q)a:1
q)$[a<0; 10; a>0; 20; 30] /- a>0
20 /- second assignment executed
```

## Vector Conditional
The general form of the vector conditional is
| ?[vector condition; true expr; false expr]
- The true expr and false expr must either be vectors of the same length as the vector condition or atoms.
- Where the vector condition returns true, the true expr is returned, where it returns false, the false expr is returned.
```
q)p:4 2 6 8 3 7 4 9 6
q)p>5 /- vector condition
001101011b /- returns a boolean vector
q)?[p>5; p; -1]
-1 -1 6 8 -1 7 -1 9 6
q)/- where boolean vector is true
q)/- the corresponding element of p is returned
q)/- where boolean vector is false, -1 is returned
```

## While Loops
While loops are available in q - but they should be used sparingly
Often adverbs can be used to get the same result more efficiently.
The general form is
| while[cond; expr1; expr2; ...; exprN]
- While the condition is true, the expressions will be executed in the order they appear in the statement.
```
q)a:b:c:0
q)while[a<10; a+:1; b+:2; c+:3]
q)a
10
q)b
20
q)c
30
```
## Do Loops
q also allows do loops.
These repeat an operation a specified number of times.
The general form is
| do[number of iterations; expr1; expr2; ...; exprN]
- This can be useful for timing operations.
```
q)a:1000?100f
q)b:1000?100f
q)\t a xexp b
0
q)\t do[10000; a xexp b]
448
q)
q)/-alternative syntax for timing operations
q)\t:10000 a xexp b
448
```
