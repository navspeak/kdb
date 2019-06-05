## Table
* A collection of named columns or a list of dictionaries
* Simple Table
```
q)([]a:1 2 3;b:`a`b`c;c:7 8 9)
a b c
-----
1 a 7
2 b 8
3 c 9
```
* Keyed table
```
q)([a:1 2 3]b:`a`b`c;c:7 8 9)
a| b c /dictionary of tables
-| ---
1| a 7
2| b 8
3| c 9
```
* Empty table
```
q)([]a:`int$();b:();c:())
a b c
-----
```
* Use ‘meta’ to retrieve table’s attributes
  - Empty table meta type
```
q)meta ([]a:();b:();c:())
c| t f a
-| -----
a|
b|
c| /empty meta table as there is no information held
```
* Simple table with attributes
q)meta ([]a:`s#1 2 3;b:`g#`a`b`c;c:`u#"abc")
```
c| t f a
-| -----
a| j   s
b| s   g
c| c   u
```
> ‘c’ gives the column names |
> ‘t’ gives the column types |
> ‘f’ gives the foreign keys |
> ‘a’ gives the attributes   

> Sorted (‘s#) The items in the list are in sorted order |
> Unique (‘u#) No duplicates within a list |
> Group (‘g#) Create a dictionary that maps each occurrences to their p |

* Meta with nested list
```
q)meta ([]a:((1;2);(3;4));b:((2;5);(7;9)))
c| t f a
-| -----
a| J
b| J /the capital letter correlates to a nested list of long types
```
* Foreign key is a field in one table that uniquely identifies a row of another table
```
q)tabid:([id:5625 5626 5627 5628];sym:`a`b`c`d)
q)tabid
id  | sym
----| ---
5625| a  
5626| b  
5627| c  
5628| d
q)tab:([]id:`tabid$5625 5626 5627 5628;price:101.1 102.3 103.5 104.6)
q) tab
id   price
----------
5625 101.1
5626 102.3
5627 103.5
5628 104.6
q)meta tab
c    | t f a
-----| ---------
id   | j tabid
price| f

q)select id,id.sym,price from tab
id sym price
--------------
5625 a 101.1
5626 b 102.3
5627 c 103.5
5628 d 104.6
```
* Virtual column i within a table represents the index of each row (in this case i has its
own operation, it cannot be assigned as a column)
```
q)exec i from tab
0 1 2 3
```
* Extract rows and columns:
```
q)t:([]a:1 2 3;b:4 5 6;c:7 8 9)
a b c
-----
1 4 7
2 5 8
3 6 9
q)
q)t[2] /take all columns from third row
a| 3
b| 6
c| 9
q)t[`a] /take column `a from all rows
1 2 3
q)t[`a`b]
1 4
2 5
3 6
```
* Reverse lookup
```
q)t?`a`b`c!3 6 9 /find one row using dictionary
2
q)t?(3 6 9) /find one row using list
2
q)t?((2 5 8);(3 6 9)) /find 2 rows using list
1 2
q)t?([]a:1 2;b:4 5;c:7 8) /find using table
0 1
```
* Operations on keyed tables 
```
q)kt1:([ks: `a`b`c] v1: 1 2 3; v2: 10 11 12)
q)kt2:([ks:`b`c`e] v1: 20 30 40; v2: 9 8 7)
q)
q)kt1
ks| v1 v2
--| -----
a | 1  10
b | 2  11
c | 3  12
q)kt2
ks| v1 v2
--| -----
b | 20 9 
c | 30 8 
e | 40 7 
q)kt1+kt2
ks| v1 v2
--| -----
a | 1 10
b | 22 20
c | 33 20
e | 40 7
```
* With unkeyed tables, we can only use arithmetic if the table consists of numeric fields
and row counts match.
```
q)t1:([]a: 1 2 3; b: 11 12 13f)
q)t2:([]a:4 5 6; b: 10 11 12)
q)t3:([]a:20 21 22 23; b:100 101 102 103)
q)t1+t2
a b
----
5 21
7 23
9 25
q)t1+t3
'length
```
