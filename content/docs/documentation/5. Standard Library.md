# The Standard Library

The standard library of HalideOS is a set of a few abstractions for some common data structures and utility 
functions that we used to again and again for the kernel as well as the shell programs. 

All the classes and the functions are encapsulated in the `hldstd` namespace for clarity.

* Files: `include/halidestdlib.h` and `src/halidestdlib.cpp`
* Namespaces: `hldstd`, `hldstd::math`

{{< columns >}}
## Classes
* `hldstd::string`
* `hltstd::stack<T>`

<--->

## Functions
Refer below for details on return types with accurate namespaces.

* `hldstd::stringCompare`
* `hldstd::stringLength`
* `hldstd::math::pow`
* `hldstd::math::abs`

{{< /columns >}}

---

## **Classes**

## `hldstd::string`

A regular string class to maintain a character array and it's size, with some conversion functions.

**Functions**

* `string(int x);` - Contructor to convert `int` to `string`
* `string(double x, int digits_after_point);` - Constructor to convert `double` to `string`
* `string(char *str);` - Constructor to convert a raw `char*` to `string`
* `string(bool val);` - Constructor to convert `bool` to `string`
* `string(string &other);` - Copy Constructor
* `int size();` - Returns size of the string
* `char at(int i);` - Returns the character at index i of the string
* `char *c_ptr();` - Returns a raw `char *` to the string
* `int to_int();` - Converts the `string` to `int`
* `double to_double();` - Converts the `string` to `double`


{{< expand "Examples - Click to Expand" >}}

```C++
#include <halidestdlib.h>

// Various ways to construct a hldstd::string
hldstd::string a = "From char *";
hldstd::string b = 10; 
hldstd::string c = false;
hldstd::string d(10.21343, 3);
hldstd::string e = a;

// Utility Functions
hldstd::string s = "FooBarBaz";

int s_size = s.size() // returns 9
char s_char = a.at(3) // returns 'B'
char* s_ptr = s.c_ptr() // returns a pointer to 
						// the char array stored in the class

// Conversion
hldstd::string i = "1201032";
hldstd::srting j = "1213.21434"

int i_int = i.to_int(); // return 1201032
double j_double = j.to_double(); // returns 1213.21434

```
{{< /expand >}}


## `hldstd::stack<T>`

A standard stack or LIFO list with the standard operations. This is a template class, the stack 
can hold any data-type `T`

**Functions**

All functions are template functions with `<typename T>`

* `stack(int size, T x);` - Constructor to initialise the stack with size and the first element;
* `bool pop();` - `false` for underflow, `true` for successful pop
* `bool push(T x);` - `false` for overflow, `true` for successful push
* `T top();` - Returns the top element of the stack
* `bool isEmpty();` - Check if stack is empty or not.

{{< expand "Examples - Click to Expand" >}}

```C++
#include <halidestdlib.h>

hldstd::stack<int> st(20, 0);

st.push(1);
st.push(2);
st.push(3);

st.pop();

int x = st.top(); // returns true
bool e = st.isEmpty(); // returns false
```
{{< /expand >}}

---

## **Functions**

Some simple mathematical functions are declared in the `math` namespace.

* `int hldstd::stringCompare(char *, char *)` - Compare 2 strings from the char pointers
* `int hldstd::stringLength(char *)` - Get length of string
* `double hldstd::math::pow(double x, int y)` - x^y
* `int hldstd::math::abs(int x)` - |x|