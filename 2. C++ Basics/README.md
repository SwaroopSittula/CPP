## Statements

There are many different kinds of statements in C++:

* Declaration statements
* Jump statements
* Expression statements
* Compound statements
* Selection statements (conditionals)
* Iteration statements (loops)
* Try blocks

```cpp
// preprocessor directive
// Indicates we would like to use the contents of iostream library in the current code
#include <iostream> 

// `main` - Function Indentifier, `int` - Return type
// The `main` function should always return an `int`
int main() 
{
   std::cout << "Hello world!";
   
   // Program sends a value back to the operating system in order to indicate whether it ran successfully or not.
   return 0; 
}
```

## Comments

* Single line comments
* Multiline Comments
    - Multiline comments cannot be nested

```cpp
#include <iostream> 

// Single line comment

/* Multiline comment
   line1
   line2 */

/* Multiline comment
 * with matching asterisk on the left 
 * to make it easier to read (beautify)
 */
int main() 
{
   std::cout << "Hello world!";
   return 0; 
}
```

## Objects and Variables

- In C++, we use objects to access memory.
- An **object** represents a region of storage (typically RAM or a CPU register) that can hold a value.
- A named object is called a **variable**.
- Objects also have associated properties.
- Compiler will figure out where and how to retrieve the value.
- Variables are actually created at runtime, when memory is allocated for their use.
- Each variable has an **identifier**, a **type (data type)**, and a **value** (and some other attributes)

### Random Access Memory (RAM)

- The main memory in a computer
- When we run a program, the operating system loads the program into RAM.

### Variable Definition

A definition statement can be used to tell the compiler that we want to use a variable in our program.

### Variable Creation

At runtime (when the program is loaded into memory and run), each object is given an actual storage location (such as
RAM, or a CPU register) that it can use to store values.
The process of reserving storage for an object’s use is called **allocation**.

```cpp
// program that first allocates a single integer variable named x 
// then allocates two more integer variables named y and z

int x; // define a variable named x (of type int)
int y, z; // define two integer variables, named y and z
```

### Variable assignment

- **Assignment**: Giving value to a variable
- **Assignment Operator**: Below is **copy-assignment** (copies the value on the right-hand side of the `=` operator to
  the variable on the left-hand side of the operator.)

```cpp
int width; // define an integer variable named width
width = 5; // assignment of value 5 into variable width

// variable width now has value 5
```

### Variable Initialization

- Combines variable **definition** and variable **assignment**
- When an object is defined, you can optionally provide an initial value for the object.

```cpp
#include <iostream>

int main()
{
    int width { 5 };    // define variable width and initialize with initial value 5
    std::cout << width; // prints 5

    return 0;
```

---

### Types of Initialization

#### Default Initialization

Occurs when a variable is declared without an explicit initializer.

```cpp
int x;   // Uninitialized (contains garbage value)
double y; // Uninitialized (contains garbage value)
```

- **For primitive types** (like `int`, `double`), the value is undefined.
- **For class types** (without a user-defined constructor), members are also uninitialized.

#### Copy Initialization

Uses an existing value to initialize a variable.

```cpp
int x = 10;    // Copy initialization
std::string s = "Hello"; // Copy initialization
```

- Can involve implicit conversions.
- May be less efficient than direct initialization for complex objects.

#### Direct Initialization

Uses parentheses `()` for initialization.

```cpp
int x ( 10 );         // Direct initialization
std::string s ( "Hello" ); // Direct initialization
```

- Avoids an extra copy for objects.
- Preferred for class objects and constructors.

#### List Initialization (Brace Initialization / Uniform Initialization)

Uses curly braces `{}` to initialize a variable.

```cpp
int x { 10 };          // List initialization (preferred in modern C++)
std::vector<int> v { 1, 2, 3, 4 }; // List initialization
```

- Direct List Initialization
- Copy List Initialization

```cpp
int width { 5 };    // direct-list-initialization of initial value 5 into variable width (preferred)
int height = { 6 }; // copy-list-initialization of initial value 6 into variable height (rarely used)
```

- Prevents **narrowing conversions** (e.g., `double → int`).
- More consistent with modern C++.
- **List-initialization disallows narrowing conversions**
  ```cpp
  int main()
  {
      // An integer can only hold non-fractional values.
      // Initializing an int with fractional value 4.5 requires the compiler to convert 4.5 to a value an int can hold.
      // Such a conversion is a narrowing conversion, since the fractional part of the value will be lost.
  
      int w1 { 4.5 }; // compile error: list-init does not allow narrowing conversion
  
      int w2 = 4.5;   // compiles: w2 copy-initialized to value 4
      int w3 (4.5);   // compiles: w3 direct-initialized to value 4
  
      return 0;
  }
  ```
  - Note that this restriction on narrowing conversions only applies to the list-initialization, not to any subsequent assignments to the variable

#### Value Initialization and Zero Initialization

Explicitly initializes a variable with a default value (zero or equivalent).
In cases where zeroing occurs, this is called zero-initialization.

```cpp
int a {};      // Initialized to 0
double b {};   // Initialized to 0.0
std::string s {}; // Initialized to an empty string
```

- Ensures that built-in types are zero-initialized.
- Useful for initializing arrays and structs.

#### Aggregate Initialization

Used for initializing aggregate types (structs, arrays).

```cpp
struct Point {
    int x, y;
};

Point p = {10, 20};  // Aggregate initialization
int arr[3] = {1, 2, 3}; // Array initialization
```

- Directly assigns values to members.

#### Static Initialization

Variables declared as `static` are zero-initialized if not explicitly assigned.

```cpp
static int x; // Initialized to 0 (default for static storage duration)
```

- Ensures a known starting state.

#### Dynamic Initialization

Uses `new` to allocate memory dynamically.

```cpp
int* p = new int(10); // Dynamic initialization
delete p; // Free memory
```

- Useful when heap memory allocation is needed.

#### Constant Initialization

Uses `const` or `constexpr` for compile-time constants.

```cpp
const int x = 42;   // Constant initialization
constexpr int y = 100; // Evaluated at compile time
```

- Ensures immutability and potential compiler optimizations.

---