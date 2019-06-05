## Dictionary
* A dictionary is a mapping between a domain list and range list
* Domain list is the key and range list is the value
* A foundation of a table (table is a list of dictionaries)
* We can create a dictionary like this:
```
q) /- dictname: `list`of`keys ! values
q) dict: `a`b`c ! 10 11 12
q) dict
a| 10
b| 11
c| 12
q) dict[`a] 
10
```
* Joining dict
```
q)dy1:(`a`b`c)!(7 8 9;`d`e`f;101b)
q)dy1,:`c`d!8 7 /join in place
q)
q)dy1
a| 7 8 9
b| `d`e`f
c| 8 /existing key is amended
d| 7 /new key is added
```
