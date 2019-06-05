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
  - max 8 arga
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
```


