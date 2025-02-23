## C++ Basics

<details><summary>

## Statements

</summary>

There are many different kinds of statements in C++:

- Declaration statements
- Jump statements
- Expression statements
- Compound statements
- Selection statements (conditionals)
- Iteration statements (loops)
- Try blocks

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

</details>


<details><summary>

## Comments

</summary>

- Single line comments
- Multiline Comments (cannot be nested)

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

</details>

<details><summary>

## Objects and Variables

</summary>

- Objects represent a region of storage.
- A named object is called a **variable**.
- Compiler determines where and how to retrieve values.
- Variables are created at runtime when memory is allocated.

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

</details>

<details><summary>

## Variable Initialization

</summary>

- Combines variable **definition** and **assignment**.
- When an object is defined, an initial value can be provided.

  ```cpp
  #include <iostream>
  
  int main()
  {
      int width { 5 };    // define variable width and initialize with initial value 5
      std::cout << width; // prints 5
      return 0;
  }
  ```

</details>

<details><summary>

## Types of Initialization

</summary>

- **Default Initialization:** Variables declared without an explicit initializer contain garbage values.
    - **For primitive types** (like `int`, `double`), the value is undefined.
    - **For class types** (without a user-defined constructor), members are also uninitialized.

    ```cpp
    int x;   // Uninitialized (contains garbage value)
    double y; // Uninitialized (contains garbage value)
    ```

- **Copy Initialization:** Uses `=` to initialize a variable.
    - Can involve implicit conversions.
    - May be less efficient than direct initialization for complex objects.

    ```cpp
    int x = 10;    // Copy initialization
    std::string s = "Hello"; // Copy initialization
    ```


- **Direct Initialization:** Uses parentheses `()`.
    - Avoids an extra copy for objects.
    - Preferred for class objects and constructors.

    ```cpp
    int x ( 10 );         // Direct initialization
    std::string s ( "Hello" ); // Direct initialization
    ```

- **List Initialization (Brace Initialization / Uniform Initialization):** Uses `{}`.
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
        - Note that this restriction on narrowing conversions only applies to the list-initialization, not to any
          subsequent assignments to the variable
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

- **Value Initialization and Zero Initialization:** Explicitly initializes a variable with a default value (zero or
  equivalent). In cases where zeroing occurs, this is called zero-initialization.
    - Ensures that built-in types are zero-initialized.
    - Useful for initializing arrays and structs.

    ```cpp
    int a {};      // Initialized to 0
    double b {};   // Initialized to 0.0
    std::string s {}; // Initialized to an empty string
    ```

- **Aggregate Initialization:** Used for initializing aggregate types (structs, arrays).
    - Directly assigns values to members.

    ```cpp
    struct Point {
    int x, y;
    };
    
    Point p = {10, 20};  // Aggregate initialization
    int arr[3] = {1, 2, 3}; // Array initialization
    ```

- **Static Initialization:** Variables declared as `static` are zero-initialized if not explicitly assigned.
    - Ensures a known starting state.

    ```cpp
    static int x; // Initialized to 0 (default for static storage duration)
    ```

- **Dynamic Initialization:** Uses `new` to allocate memory dynamically.
    - Useful when heap memory allocation is needed.

    ```cpp
    int* p = new int(10); // Dynamic initialization
    delete p; // Free memory
    ```

- **Constant Initialization:** Uses `const` or `constexpr` for compile-time constants.
    - Ensures immutability and potential compiler optimizations.

    ```cpp
    const int x = 42;   // Constant initialization
    constexpr int y = 100; // Evaluated at compile time
    ```

</details>



<details><summary>

## Instantiation

</summary>

The term **instantiation** is a fancy word that means a variable has been created (allocated) and initialized (this
includes
default initialization). An instantiated object is sometimes called an **instance**. Most often, this term is applied to
class type objects, but it is occasionally applied to objects of other types as well.

</details>

<details><summary>

## Initializing multiple variables

</summary>

```cpp
int a = 5, b = 6;          // copy-initialization
int c ( 7 ), d ( 8 );      // direct-initialization
int e { 9 }, f { 10 };     // direct-list-initialization
int i {}, j {};            // value-initialization
```

**Note**: In the below statement, variable a will be left uninitialized, and the compiler may or may not complain.

```cpp
int a, b = 5;     // wrong: a is not initialized to 5!
int a = 5, b = 5; // correct: a and b are initialized to 5
```

</details>


<details><summary>

## The [[maybe_unused]] attribute (C++17)

</summary>

[[maybe_unused]] attribute allows us to tell the compiler that we’re okay with a variable being unused.
The compiler will not generate unused variable warnings for such variables.

```cpp
#include <iostream>

int main()
{
    [[maybe_unused]] double pi { 3.14159 };  // Don't complain if pi is unused
    [[maybe_unused]] double gravity { 9.8 }; // Don't complain if gravity is unused
    [[maybe_unused]] double phi { 1.61803 }; // Don't complain if phi is unused

    std::cout << pi << '\n';
    std::cout << phi << '\n';

    // The compiler will no longer warn about gravity not being used

    return 0;
}
```

</details>