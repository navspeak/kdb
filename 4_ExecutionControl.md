https://code.kx.com/q4m3/A_Built-in_Functions/#a88-ssr

* The general template of the if statement is
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
  
* The general template of if-else is
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
