## Basic Operation
* 5 * 2 + 4 =>  20 - Right to left
* \v => to check variable names
## Atoms - singluar entity
* It has a specific data type - this could be integer, float, character, symbol, etc.
* To force the type, we specify the type as a single letter after the atom. Lke a:1 (no forced type. 64 bit long)
a:5f. 
* type 5f => -7h => - tells atom, 7 for float

char | rep | num rep  | name | size (byte) | example 
---- | --- | ---      | ---  |  ---        |   ---
b |1 |boolean |1 |1b
g |2 |guid |16 |
x |4 |byte |1| 0x01
h |5 |short| 2 |32h
i |6 |int |4 | 12i
j |7 |long |8 |22
e |8 |real |4 |3.1e
f |9 |float |8 |1.234
c |10 |char | 1 |“c”
s |11 |symbol | *| \`a
p |12 |timestamp| 8 |2013.06.04D16:10:31.795334000
m |13 |month |4| 2012.03m
d |14 |date |4 |2011.01.01
z |15 |datetime | 8 |2013.06.04T16:11:24.635
n |16 |timespan |8 |13:12:15.012365478
u |17 |minute |4 |12:30
v |18 |second |4| 11:12:30
t |19| time| |4| 11:20:30.123

* .z.d => current date .z.t => current time
*  date stored as 4 byte signed integer and is denoted by yyyy.mm.dd
``` q)2000.01.01=0 => 1b ```
* Implicit type promotion: ```3i+3h => 6i /- promote short to int``` or ```3e+3f => 6f /- real to float ```
* Implicit bool promotion: ``` q) if[count (); show "some text"] /- counts() is count empty list => 0 ```
* Changing types of items - casting **($)**
  - new type $ object to change
    - `int$5h =>5i /- named rep or 6$5h =>5i /- number rep or "i"$5h => 5i /- char rep 
    - "I" $ "4" /- from a string
  - To cast to a string, we use the keyword string
    - string `text => "text" or string 1234 => "1234"
 
## List - collection of atoms
```
q) l1:til 5 => 0 1 2 3 4 
q) l1 * 5 => 0 5 10 15 20
q) l1 > 3 => 00011b
q) type l1 => 7h (note it is +ve denoting list)
q) type each l1 => -6 -6 -6 -6 -6h
==
q) emptyList:() => type emptyList => 0h
q) emptyListWithType:`int$() => type emptyListWithType => 6h
==
q) mixedTypeList: (100i;200h;300j;400e) => 0h | type each mixedTypeList => -6 -5 -7h -8h
== Equal and matches ==
q) l1: (100i;200i;300i;400i) | l2: (100i;200h;300j;400e)
q) l1 ~ l1 => 0h (matches => no)
q) l1 = l2 => 1111h (NOTE: = considers just the value not datatype)
== Singleton list ==
q) enlist 100i => ,100
q)type enlist 100i => 6h
q)type each enlist 100i => ,-6h
== Nested list - depth level of 2 or more ==
q)(1;2;(3;4))
1
2
3 4
q)type (1;2;(3;4)) => 0h
== Use index ===
q) l1: 1 2 3 4 5 6 => l1[0] = 1 => l1[0, 3, 1] => 1 4 2
== Matrix ==
q)mm:(1 2 3;4 5 6;7 8 9)
q)mm
1 2 3
4 5 6
7 8 9
==Indexing at depth===
q)mm[0;] /take all from first row
    1 2 3
q)mm[;0] /take first item from all rows
    1 4 7
q)mm[1;1] /take second item from second row
     5
q)mm[2;10]  /returns null of proper type as column
     0N /index is out of range
q)mm[0;1]:12
q)mm
      1 12 3
      4 5 6
      7 8 9
``` 
## List Operations
* Join (,)
  - 1,2 (atom to atom)
  - \`a,\`b\`c\`d (atom to list)
* Drop (_)
  - 2_1 2 3 4 5 /drop first 2 => 3 4 5
  - -2_1 2 3 4 5 /drop last 2 => 1 2 3
  - 1 2 3 4 5 _ 2 /drop item with index 2 => 1 2 4 5
* Cut (-)
  - 1 3 4 cut 1 2 3 4 5 6 /cut at index 1, 3 and 4
  ```
      2 3
      ,4
      5 6
   ```
* Take(#)
  - 2#1 2 3 4 5 /take first 2 => 1 2
  - -2#1 2 3 4 5 /take last 2 => 4 5
  - 10#1 2 3 4 5 /repeat take => 1 2 3 4 5 1 2 3 4 5
  - 2 3#1 2 3 4 5 /2x3 matrix
    ```
    1 2 3
    4 5 1
    ```
* Sublist (similar to Take)  
  - 2 sublist 1 2 3 4 5 /take first 2 => 1 2 
  - -2 sublist 1 2 3 4 5 /take last 2 => 4 5
  - 10 sublist 1 2 3 4 5 /take only what's available => 1 2 3 4 5
  - 2 3 sublist 1 2 3 4 5 /takes 3 items starting from position 2 =>3 4 5
* Find (?)
  - 1 2 3 4 5?3 /find the position of 3 =>2
  - 1 2 3 4 5?7 /not found => 5 /return the maximum index+1
  - 1 2 2 3 4?2 /only return the first occurrence
* Random (?)
  - 5?1 2 3 4 5 /pick 5 random items from the list => 1 3 2 2 4
  - 5?10 /pick 5 random items less than 10 => 8 5 5 9 2
  - 5?\`2 /pick 5 random symbols with length 2 => \`ab\`hg\`ij\`fr\`dc
  - 5?" " /pick 5 random characters => "akdlm"
  - -5?10 /pick 5 distinct random items less than 10 => 1 6 2 9 4
* ? is overloaded.If the left arg = list & right = atom of the same type, i.e. list ? atom finds the first occurence of the atom in the list. 
```
q)lst:8 1 9 5 4 6 6 1 8 5
q)lst?8 => 0
```
* A number as the left argument to the ? operator and a list as the right argument,number ? list would randomly select number amount of elements from list.
```
q)5?lst
6 6 4 1 5
```
* Count
```
q)count 1 2 3 4 /count number of elements in list => 4
q)count enlist 1 2 3 4 /counts the first dimension of the enlisted structure => 1
q)count (1 2 3;4 5 6) /2 lists in a nested list => 2
q)count each (1 2 3;4 5 6) /count each list in a nested list => 3 3
q)count () /works on an empty list => 0
q)count 5 /works on an atom => 1
```
* First, Last
```
q)first 42 /operates on atoms and lists => 42
q)ls: 3 7 8 2 1 4 2 8 0 5
q)first ls => 3
q)last ls => 5
q)ls2:enlist(10)
q)ls2
,10
q)first ls2 /acts as a dual to \`enlist' => 10
q)nls:(1 2; 4; 5 6 7; 8 9; 0 10 11 12 13)
q)first each nlst /can be used on each row of a nested list
1 4 5 8 0
```
* Raze
```
q)type (1 2 3;4 5 6)
0h
q)raze (1 2 3;4 5 6) /raze removes one level of structure
1 2 3 4 5 6
q)type raze (1 2 3;4 5 6)
7h
q)raze a:(1 2;4 5;(8 9;10 11))
1
2
4
5
8 9
10 11

q)0N!raze a /only one level removed
(1;2;4;5;8 9;10 11)
1
2
4
5
8 9
10 11
q)(raze/) a /can be combined with over adverb to produce single list
1 2 4 5 8 9 10 11
```
* distinct - returns the distinct items within a group of entities
```
q)syms:\`a\`b\`c\`a\`a\`d\`c
q)distinct syms => `a`b`c`d
```
* except - excludes the specified item from a list or dictionary
```
q)l1:45 60 20
q)l2:45 20 90 80
q)l1 except l2
,60
q)l2 except l1
90 80
```
* inter - returns the elements common to both arguments
```
q)list1:1 2 3 4
q)list2:2 3 6 7
q)list1 inter list2
2 3
```
* group - applied to a list, returns a dictionary of positions for each distinct element
* union - returns a list of the distinct elements of its combined arguments
```
q)list1:3 4 5 6
q)list2:6 7 8
q)list1 union list2
3 4 5 6 7 8
q)list2 union list1
6 7 8 3 4 5
```
* flip - takes a simple list, column, dictionary, or table and transposes it
* in - returns a boolean result on whether a specified item is in a list
```
q)fruit:\`apple\`banana\`apple\`pear
q)\`apple in fruit => 1b
q)\`orange in fruit => 0b
```
* reverse
* string - can be applied to any data type and the result will be a list of characters 
forming a string
```
q)string `banana
"banana"
q)string 1 2 3
,"1"
,"2"
,"3"
q)raze string 1 2 3
"123"
```
* where
```
q)l1:2 4 6 2
q)l2:8 8 4 3
q)l2 where l1<6
8 8 3
q)l2 where l1=6
,4
```
* Timing operations
```
q)\t 1000000?10
21
/the returned time is given in milliseconds
```
To time the operation, repeated say n times, use the command \t:n
```
q)\t:100 1000000?10
1863
```
  - Vector operations are much quicker than the alternatives e.g.
```
q)d:1000000?200
q)
q)/vector form of operation
q)\t r3:sum d where d>100
27
q)/adverb form of operation
q)\t {if[x>100;r2+::x];}each d
291
q)/while loop form of operation
q)i:0
q)\t while[i<count d;if[d[i]>100;r1+:d[i]];i+:1]
932
```
## Links
https://code.kx.com/v2/ref/
https://code.kx.com/q4m3/2_Basic_Data_Types_Atoms/
https://code.kx.com/v2/ref/#z
export QHOME=/Users/navspeak/Downloads/q

## Questions:
Suppose we have a list, which is defined as:

    list:2 6 4 12 8

2 6,4 _ list 
-3#list,6 
4#list?4 
-8?list 
6 sublist list 
(list?10)#4,list 

Suppose we have two lists:

    list: 2 4 4 7 3
    list2: 4 7 8 1

Match the input with the corresponding output.

list except list2 
list2 except list 
distinct list 
list2 inter list 
list inter list2 
list2 union list 
reverse list 
list union list2 
list where list2<5 
