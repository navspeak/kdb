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
* ``` q) if[count (); show "some text"] /- defaults to 0b ... counts() is count empty list ```
