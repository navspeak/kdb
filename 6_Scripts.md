* Load - q)\l script.q
* To suppress output within a script:

```
f:{x+1}; /suppress output with ;
f[2];
f[5]*2;
```
* To force output within a script:
```
f:{x+1};
show f[2]; /using show function
0N!f[5]*2; /using 0N! function
```
- ‘show’ formats an object to plain text and writes it to standard output
- ‘0N!’ returns the object that is passed into it
```
q)1+0N!2
2 /from the 0N!
3 /result of the expression
```

* test.q

```
show "Loading a q script!"

a:123
b:45
c:001b
d:"strings"
e:1 2 3 4 5

/- A single forward slash like this is a single line comment.
/- As we can see, we can force output by using 'show'. We can also use '0N!'.

/
We can comment out whole blocks
by starting with a single forward slash
and finishing with a single backslash
\

/- We can continue an expression over more than one line, by using whitespace -

table:([] a:10?`3; b:10?10; c:10?200;
   d:10?"")

/- without the whitespace

/tab2:([] a:10?`3; b:10?10; c:10?2.0;
/d:10?`a`b`v`d)

/- the same applies to functions

f:{[a;b;c]
   n:a*b;
   c+n}
```

* Command line arguments can be used to supply information to a script before it is executed.
- This can be achieved by supplying arguments to a q command line:
- C:\Users>q -key value
- This input can be brought into the q session by using .z.x, which returns the command line arguments as a list of strings:
```
q).z.x
"-key"
"value"
```
- Applying .Q.opt to the string list given by .z.x allows the output to be parsed as a dictionary.
```
q).Q.opt[.z.x]
key| "value"
```
- Arguments prefixed with a ‘-’ are parsed as keys, with the arguments following (delimited by spaces) being parsed as string values:
- C:\Users>q -key1 value1 value2 -key2 value3 value 4
```
q).Q.opt[.z.x]
key1| ("value1";"value2")
key2| ("value3";"value";,"4")
```

- If you have a script myscript.q:
- options:.Q.opt[.z.x];
```
if["date"~options[`print][0]; variable: .z.d];
if["time"~options[`print][0]; variable: .z.t];
```
- This script will then decide whether to print the date or time based on a users input:
- C:\Users>q myscript.q -print time
- The string values can also be cast into specific q datatypes for use in calculations or queries.
- .z.f can also be used to return the script name, supplied on the command line, as a symbol. This can be useful when logging information needs to be kept.

* testcommandline.q
```
/- we can take params from the command line
/-for using in a script
/- we can launch q like this -
/- q scriptname.q -key1 value1 -key2 value2 -key3 value3

/- .z.x holds this in string form

show .z.x

/- we can put this info into a dictionary

show inputs:.Q.opt[.z.x]

/- we can use these inputs as a switch
if["date"~inputs[`print][0]; x:.z.d];
if["time"~inputs[`print][0]; x:.z.t];
x
```
