# Variable and Data Types

## Variables

### Definition

Variable is a name given to a memory location. It is the basic unit of storage in a program.

- The value stored in a variable can be changed during program execution
- A variable is only a name given to a memory location, all the operations done on the variable effects that memory location
- In C++, all the variables must be declared before use

### Rules of declaration

- The name of the variable contains: `letter, digits, and underscores`.
- The name of the variable is case sensitive (ie: `myName` and `myname` are different variables)
- The name of the variable does not contain any whitespace and special characters (ie `#, $, %, * etc...`)
- All the variable names must begin with a letter of the alphabet or an underscores `_`
- In C++ , reversed keywords like `for, while, if, else, float, int, double, and class etc...` cannot be used as variables name

A variable can consist of alphabets (both UPPER CASE or lower case), digits and underscores `_` character. However, the name must not start with a digit.

Variable declare pattern: **[data type] [variable name] = [value];**

```c++
#include <iostream>

int main() {
    // declare variables
    int myAge = 40;
    bool isMarried = false;
    float balance = 20.123;
    
    return 0;
}
```

### Naming conventions

To make code more readdable and maintainable, follow these naming coventions:

- Camel case:
    * Start with a lowercase letter, and capitalize subsequent words
    * Example: `currentYear, myAge, isMarried`
- Snake case:
    * Use underscores to speparate words, use lowercase letters
    * Example: `current_year, my_age, is_married`
- For constant:
    * Use all uppercase letters with underscores between words
    * Example: `MAX_AGE, MIN_AGE, LIMIT, PI`

## Data types

Data types form the foundation of data representation in C++. Every variable must be associated with a data type that defines the kind of value it can store and how that value is handled by the compiler.

- Data types determine the memory allocation, range of values, and operations supported by a variable.
- Understanding different data types is essential for writting correct, efficient, and mantainable C++ program.

### Classification of Data Types

Data types can broadly classified into three categories:

- Basic data types
- Derived data types
- User defined data types

#### Basic data types

- int
- float
- double
- char
- bool
- void

#### Derived data types

- array `[]`: stores multiple values of the same type in contiguous memory locations
- pointer `*`: stores the memory address of another variable
- reference `&` / `&&`: acts as an alias for an existing variable
- function: it is used to represent a derived type because they have a specific return type and parameter types

#### User defined data types

- class: It combines data and functions into a single unit.
- struct: Use to groups related variables under one name.
- union: It allows multiple members to share the same memory location
- typedef/using: use to create type aliases which are alternative names for existing data types. From C++11 and later, heavily favors the **using** syntax.
- enum/enum class: used to represent a fixed set of related, named choices.

### Example of basic data types definition

In this lesson, we only focus into basic data types.


```c++
#include <iostream>

// define a function
void returnNothing();

int main() {
    int age = 37;
    float balance = 102.123f;
    double salary = 7000000.0;
    char letterA = 'A';
    bool emailVerified = true;

    // invoke function
    returnNothing();
    
    return 0;
}

// concrete implement function
void returnNothing() {
    cout << "Just print out this line then stop";
}
```

### Data types modifiers

C++ provides type modifiers that can alter the **size**, **range** or representation of certain fundamental data types.

The commonly used modifiers are short, long, signed, and unsigned.

- **short**: Specifies a smaller integer type when supported.
- **long**: Specifies an integer type wiht  at least as much storage as int.
- **signed**: Allows an integer type to represent both positive and negative values.
- **unsigned**: Allows an integer type to represent ONLY non-negative values and provides a larger positive range.

#### Example:

```c++
short int a;
long int b;
signed int c;
unsigned int d;
long long int e;

// long int or shortened by long;
long int a = 10;
long b = 10;

cout << "Size of a: " << sizeof(a) << endl;
cout << "Size of b: " << sizeof(b) << endl;

// Size of a: 8
// Size of b: 8
```

#### Tips to remember modification rules

Remember the modifiers change the **size** or **sign** of standard data types (`int, char, double`). The compiler applies three absolute rules when you use them:

- **You can combine size and sign modifiers**: You can use one size modifier and one sign modifier together on the same variable (e.g., `unsigned long`)
- **Implicit `int` rule**: If you use a modifier by itself without specifying a data type, the compiler automatically assumes you mean `int`. (e.g., `long = long int`, `long long = long long int`)
- **No conflicting combinations**: You cannot combine opposites (e.g., `signed unsigned int` or `short long int` will cause a compile error).


C++ just allows us to modify these data types, all the types out of this list are not able to modify the size, sign.

- **int**: `[signed | unsigned] [short | long | long long] [int]`
- **char**: `[signed | unsigned] char`
- **double**: `[long] double`

**Example:**

```c++
// int
signed short a0 = 10;
signed short int a1 = 10;
signed int a2 = 10;
signed long a3 = 10;
signed long int a4 = 10;
signed long long int a5 = 10;
signed long long a6 = 10;

unsigned short b0 = 10;
unsigned short int b1 = 10;
unsigned int b2 = 10;
unsigned long int b3 = 10;
unsigned long b4 = 10;
unsigned long long int b5 = 10;
unsigned long long b6 = 10;

// char
signed char c0 = 'C';
unsigned char c1 = 'C';

// double
long double d0 = 123.213;
```

### Operator `sizeof` in C++

The `sizeof` operator is a unary compile-time operator used to determine the size of variables, data types, and constants in bytes at compile time.

It can also determine the size of classes, and unions.

**Key features of `sizeof` operator:

- **Compile-time evaluation**:
    * The `sizeof` operator is evaluated during the compilation of the program. This means that its results are known before the program runs.
- **Determines size in Bytes**:
    * It returns the number of bytes required to store a particular data type or object in memory.
- **Flexible usage**:
    * It can be used with basic data types, user-defined types, variables and even expressions.
- **Its operand is unevaluated**:
    * `sizeof(i++)` give the size of `i`, and `i` never incremented. Same reason `sizeof(*p)` is safe even when `p` is null, the compiler only looks at the type.

Syntax:

```c++
sizeof(int); // 4 bytes
// or
sizeof(10); // 4 bytes
```

> You may found `sizeof` return different results on the different operating system. It is because `sizeof` doesn't depend on CPU, it depends on the ABI's data model, which the OS + compiler pick. That's why Windows x64 and Linux x64 on identical hardware, disagree.

Two separate things are going on:

- **Pointer width**:
    * A 64-bit process has a 64-bit address space, so pointers (and therefore `size_t`, `ptrdiff_t`, `intptr_t`) double from 4 to 8 bytes.
- **Which integer type absorbed the change**:
    * Unix chose [LP64](https://archive.opengroup.org/public/tech/aspen/lp64_wp.htm) `long` and pointers both become 64-bit.
    * Microsoft choose [LLP64](https://learn.microsoft.com/en-us/windows/win32/winprog64/abstract-data-models) only `long long` and pointers grow, `long` stay 32-bit, because decades of Windows code assumed `sizeof(long) == sizeof(int) == sizeof(void)`. Neither is "wrong", the standard permits both.

## Global variables and scope variables

In programming, the scope of a variable is defined as the extent of the program code within which the variable can be accessed or declared or worked with.

There are mainly two types of variable scropes:

- Local variables
- Global variables

### Local variables

Variables defined within a function or block are said to be local to those functions.

Anything between `{` and `}` is said to be inside a block.

Local variables do not exist outside the block in which they are declared, i.e they cannot be accessed or used outside that block.

Declaring local variables:

```c++
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    /*
    x is belong to main function only, it stay in between curly braces {} and valid to main function block. Cannot accessed or used outside of main function.
    */
    count << x << endl; // 10
    
    return 0;
}
```

### Global variables

Global variables can be accessed from any part of the program.

- They are available throughout the lifetime of a program.
- They are declared at the top of the program outside all the functions or blocks

Declaring global variables:

```c++
#include <iostream>
using namespace std;

int x = 10;

cout << x << endl;
int main() {

    cout << x << endl; // 10
    return 0;
}
```

Whenever there is a local variable defined with same name as that of a global variable then the compiler will give precedence to the local variable.

```c++
#include <iostream>
using namespace std;

int x = 10;
int main() {
    int x = 20;
    cout << x << endl; // 20
    return 0;
}
```

**When a variable is referenced outside its scope:**

- A local variable cannot be accessed outside the function/block where it is declared resulting in a compiler error.
- A global variable can be accessed anywhere in the program unless explicitly hidden by a local variable

```c++
#include <iostream>
using namespace std;

void localVariable() {
    int y = 20; // Local variable
}

int main() {
    localVariable();
    
    // accessing local variable y outside of its scope will cause compilation error
    cout << y << endl; // error: ‘y’ was not declared in this scope
    return 0;
}
```

### Using the `extern` keyword

If a global variable is defined after it is used in the program, the compiler throws an error.

To solve this, we use the `extern` keyword, which tells the compiler that the variable is defined elswhere in the program.

```c++
#include <iostream>
using namespace std;

extern int x;
int main() {
    cout << x << endl; // 10
    return 0;
}

int x = 10;
```

### Global and local variables with the same name

When a local and global variables share the same name:

1. The local variable takes precendence within the block where it is declared.
    ```c++
    // example 1: local variable overshadows global variable
    #include <iostream>
    using namespace std;

    // global variable
    int x = 10;
    int main() {
        // local variable
        int x = 20;
        cout << x << endl; // 20
        return 0;
    }
    ```
    
    ```c++
    // example 2: nested local variable
    #include <iostream>
    using namespace std;

    // global variable
    int x = 10;
    int main() {
        // local variable
        int x = 20;
        {
            int x = 30;
            cout << x << endl; // 30
        }
        return 0;
    }
    ```
2. The global variable is overshadowed but still exists and can be accessed using the scope resolution operator `::`
    ```c++
    #include <iostream>
    using namespace std;

    // global variable
    int x = 10;
    int main() {
        // local variable
        int x = 20;
        {
            int x = 30;
            cout << ::x << endl; // 10
        }
        return 0;
    }
    ```
