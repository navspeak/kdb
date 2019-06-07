* niladic functions
```
q)f:{1+1} or f:{[]:1+1}
q)f[]
2
```
* Monadic
```
q)f:{x+1} or f:{[arg1]:arg1+1}
q)f[1]
2
```
* dyadic
```
q)f:{x+y} or f:{[arg1+agr2]:arg1+arg2}
q)f[1;1]
2
```
* triadic
```
q)f:{x+y+z} or f:{[arg1+arg2+arg3]:arg1+arg2+arg3}
q)f[1;1;1]
3
``````
* Multivalent - implicit not allowed
  - max 8 args
  - For more use dictionary
```
q)d:(10?" ")!1+ til 10
q)d
i| 1
y| 2
c| 3
z| 4
m| 5
l| 6
w| 7
h| 8
e| 9
v| 10
q)f:{[d] (+/)d}
q)f[d]
55
q) type f
100h
```
## Special function
```
q)f:+
q)+[1;2]
3
q)f[1;2]
3
q)1+2
3
q)1 f 2
'type
  [0]  1 f 2
       ^
```
## Structure of a function
```
q)get {[x;y;z] d:x+y+z+12;.k.k:1;10}
0xa07a41794178410316020d0b04810002a10004 /byte representation
`x`y`z /argument names
,`d /local variable
``.k.k /global variable
12 /constant
10 /constant
"{[x;y;z] d:x+ y +z+12;.k.k:1;10}" /string form
q)get[{[x;y;z] d:x+y+z+12;.k.k:1;10}][1]
`x`y`z /get first element from the list - function arguments
```
## Function within a function
```
q)f:{x+1}
q)g:{f[x]*2}
q)g[2]
6
```
## In - line functions
```
q)z:{f:{x+1};f[x]+2} /defining a function within a function
q)z[3]
6
q)g:{{x+1}[x]+2} /same result but without assigning to a variable
q)g[3]
6
```
## A projection of a function allows us to set one or more of the variables
```
q)/- create simple diadic function
q)f:{x+y}
q)/- create a projection where x is fixed
q)g:f[2]
q)g
{x+y}[2]
q)g[10] /g is equivalent to g:{2+y}
12
A projection retains its definition if the original function is redefined:
q)f:{x*y*z}
q) /- create the original projection
q)h:f[10]
q) /-change the original function
q)f:{x+2*y*5*z}
q)h
{x*y*z}[10]
q)/- the projection doesn't change
```
## A projection of a projection is the same as a projection of the original function:
```
q)f:{x*y*z}
q)/- define h as a projection of f with x = 10
q)h:f[10]
q)h
{x*y*z}[10]
q)/-define n as a projection of h
q)n:h[;5]
q)/-this is equal to a projection of f; i.e. f[10; ;5]
q)n
{x*y*z}[10][;5]
q)n[2]
100
```
## Links
https://code.kx.com/q4m3/6_Functions/
https://code.kx.com/q4m3/A_Built-in_Functions/#a88-ssr
