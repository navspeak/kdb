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
* Lookup assignment
```
q)dy2:(`a`b`c)!(1 2 3;4 5 6;7 8 9)
q)dy2[`c]:9 3 6 /amend existing key
q)dy2
a| 1 2 3
b| 4 5 6
c| 9 3 6
q)dy2[`d]:8 8 8 /add new key
a| 1 2 3
b| 4 5 6
c| 9 3 6
d| 8 8 8
q)dy2[`a;0]:3f /type safe
'type
```
* Operation like  find (?), drop ( ), and take (#)

```
q)dict:`a`b`c!10 11 12
q)
q)dict?10 / find values
`a
q)dict?10 12 / find multiple values
`a`c
q)
q)`a _ dict / drop keys
b| 11
c| 12
q)`a`b _ dict / drop multiple keys
c| 12
q)dict _ `a
b| 11
c| 12
q)
q)`b`c`g#dict / take
b| 11
c| 12
g|
```
* Arithmetic Operations
```
q)d1:`alpha`bravo`charlie`delta`echo`foxtrot!10 15 3 21 6 30
q)d2: `alpha`charlie`bravo`foxtrot!10 8 6 30
q)
q)d2*2
alpha | 20
charlie| 16
bravo | 12
foxtrot| 60
q)
q)d1+d2 /result shows all the distinct domains,
alpha | 20 /and only adds those present in both
bravo | 21
charlie| 11
delta | 21
echo | 6
foxtrot| 60
```
* Logical operators will also match on dictionary ranges according to keys:
```
q)d1=d2
alpha | 1
bravo | 0
charlie| 0
delta | 0
echo | 0
foxtrot| 1
```
* Other operators libe avg
``` 
q)dy2:(`a`b`c)!(1 2 3;4 5 6;7 8 9)
q)avg dy2 /average on whole dictionary by index
4 5 6f
q)avg each dic /average on each value of dictionary
a| 2
b| 5
c| 8
```
* Relationship between a dictionary and a table
```
q)show dy2:(`a`b`c)!(1 2 3;4 5 6;7 8 9)
a| 1 2 3
b| 4 5 6
c| 7 8 9
q)show tab:flip dy2
a b c
-----
1 4 7
2 5 8
3 6 9
q)type tab: flip dy2
98h /unkeyed table

q)show tab2:([]a:1 2 3;b:4 5 6;c:7 8 9)
a b c
-----
1 4 7
2 5 8
3 6 9
q)tab2~tab /both are the same
1b
q)dy2~flip tab2 /table can be flipped back to dictionary
1b
```
* The value in dict must be a list in order to flip into table
```
q)dy4:(`a`b`c)!(1 2 3)
q)dy4
a| 1
b| 2
c| 3
q)type each dy4
a| -7 /values are atoms
b| -7
c| -7
q)tab:flip dy4
'rank
q)tab:enlist dy4 /put the dictionary elements into a list
q)tab /as table is a list of dictionaries
a b c
-----
1 2 3
q)flip enlist each dy4 /convert each atom to singleton list
a b c
-----
1 2 3
q)tab~flip enlist each dy4
1b
```
