# BunnyLang Documentation

### In Order to Run BunnyLang...

### Step1:
Ensure that Scala 3.0 is installed and the proper JDK's are installed (i am using open-JDK 17.0.1)

### Step2:
All source code is located in bunnyLang.scala. If you would like to run source code then run bunnyLang.scala in the directory
src/main/scala/bunnyLang.scala . If you wish to run the test file then run testBunnyLang.scala . The directory is
src/test/testBunnyLang.scala

### Here are the following operations of BunnyLang:

#### Assign:
````
Assign(Var("someSetName"), Insert(Var("var"), Value(1)), Value("somestring")).evalSet 
|| Assign(Var("someSetName"), Insert(Var("var"), Value(1)), Value("somestring"), Value(4747)).evalSet ||
Assign(Var("someSetName"), Insert(Var("var"), Value("string stuff"), Value(85647)), Value("58463"), Value("helloworld")).evalSet
````
<u>Assign takes in minimum 3 arguments but can take infinity</u>: <b>Var</b>, <b>Insert</b>, and <b>Value*</b>

<b>Assign</b> creates a set with the name specified with Var and inserts the values in Value into the set, if there are values
in insert that have a Var name that matches the Var name in Assign then those values will be inserted as well,
otherwise those values will be inserted into the set that is specified in the Var inside the call to Insert.
You can insert as many values as you would like.
evalSet must be called on Assign() in order to return the map of Sets.
A map containing the updated sets will be returned.

<b>Var</b> is an ArithExp Object that takes in a string as a parameter which will later be used to bind a variable to a Set


````
Var("someSetName")
````

<b>Value</b> is an ArithExp Object that takes in a string or int as a parameter which will be inserted into the given set

````
Value("someValName") || Value(1)
````

<b>Insert</b> is an ArithExp Object that takes in a Var which specifies the set to insert into and a Value(s) to be inserted
evalInsert must be called on Insert() when using a single instance of Insert, **note it is not necessary to
call .evalInsert when using Insert inside of Assign().

````
Insert(Var("someSet"), Value(1)).evalInsert || Insert(Var("mySet"), Value("fun string values"), Value(123)).evalInsert
````

<b>Check</b> is an ArithExp Object that takes in a set name to check, a Value to see if that value exists in the set specified,
and a map that must be generated from either a call to Insert() or Assign(). Empty map results in false returned
A boolean value of true or false is returned upon is the value exists in the set or not
evalCheck must be called on Check() when using a single instance of Check
````
Check("someSetName", Value(1), myMap).evalCheck
````

<b>Delete</b> is an ArithExp Object that takes in a set name to delete, and a Map to delete the set from.
a map that must be generated from either a call to Insert() or Assign(). Empty map inputted results in empty map returned
The updated map will be returned upon the deletion
evalDelete must be called on Delete() when using a single instance of Delete
````
Delete("nameOfSet", myMap).evalDelete
````

<b>Macro</b> is an ArithExp Object that takes in a set name to be perform on, and an Operation such as delete or
insert that will be performed on the set specified, a map you would like to perform the operation on, and if you choose
the operation insert then you need to specify values to be inserted. if performing delete then specify Value("empty")
. The updated map will be returned with the approproate operation performed, if an empty map is given then empty Map is returned
evalMacro must be called on Macro() when using a single instance of Macro

**note the only operations that are acceptable to be defined in Macro are Insert and Delete, all other operations will
be considered illegal and result in an empty map being returned.
````
Macro("someSetName", delete, myMap, Value("empty")).evalMacro ||
Macro("someSetName", insert, myMap, Value("empty")).evalMacro
````

<b>Scope</b> is an ArithExp Object that takes in a scope name to be created, then the previous Scope is given which contains the specifications
from Assign which is described above <i>**see Assign</i>
evalScope must be called on Scope() when using a single instance of Scope
````
Scope("scopename", Scope("othername", Assign(Var("someSetName"), Insert(Var("var"), Value(1)), Value("somestring")))).evalScope
````

<b>Union</b> is an ArithExp Object that takes in two sets to perform the operation on and then returns the unified sets
that is is the set of all objects that are a member of A, or B, or both.
evalUnion must be called on Union() when using a single instance of Union
````
Union("setA", "setB")
````

<b>Intersection</b> is an ArithExp Object that takes in two sets to perform the operation on and then returns the intersection of sets
that is the set of all objects that are members of both A and B.
evalIntersection must be called on Intersection() when using a single instance of Intersection
````
Intersection("setA", "setB").evalIntersection
````

<b>Set Differance</b> is an ArithExp Object that takes in two sets to perform the operation on and then returns the set difference of sets
that is the set of all members of U that are not members of A.
evalSetDif must be called on SetDif() when using a single instance of SetDif
````
SetDif("setA", "setB").evalSetDif
````

<b>Symmetric Differance</b> is an ArithExp Object that takes in two sets to perform the operation on and then returns the symmetric differance of sets
that is the set of all objects that are a member of exactly one of A and B (elements which are in one of the sets, but not in both). For instance, for the
sets {1, 2, 3} and {2, 3, 4}, the symmetric difference set is {1, 4}. It is the set difference of the union and the intersection, (A ∪ B) \ (A ∩ B) or (A \ B) ∪ (B \ A).
evalSymDif must be called on SymDif() when using a single instance of SymDif
````
SymDif("setA", "setB").evalSymDif
````

<b>Cartesian Product</b> is an ArithExp Object that takes in two sets to perform the operation on and then returns the cartesian product of sets
that is the set whose members are all possible ordered pairs (a, b), where a is a member of A and b is a member of B
evalCartProd must be called on CartProd() when using a single instance of CartProd
````
CartProd("setA", "setB").evalCartProd
````



