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

* Meta with nested
q)meta ([]a:((1;2);(3;4));b:((2;5);(7;9)))
c| t f a
-| -----
a| J
b| J /the capital letter correlates to a nested list
/of long types
