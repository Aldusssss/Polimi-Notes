# Modules 6-9: Input/Output and Control Structures

## Topic Overview

C++ programming, input/output management and control structures. The modules cover reading and writing data with `cin` and `cout`, variable declarations, the `iostream` library, the steps for creating and running a program, the operating system, readability and documentation of code, and the control structures (`while`, `do-while`, `for`, `if-else`) with the operators needed to use them.

---

## Key Points Summary

1. Input/output management in C++ through `cin`
2. Importance of code reuse and of libraries
3. Role of variable declarations in memory allocation and type checking
4. Syntax for declaring several variables of the same type
5. How the extraction operator `>>` works
6. Keyboard input is read as a sequence of characters
7. Need for separators (e.g. space) between input data
8. Conversion from a sequence of characters to a numerical value
9. Risk of deadlock if the user does not know that data must be entered
10. Importance of guiding the user in entering data

**Key Quotes:**
> "For those who must learn to solve problems professionally it is never useful to reinvent the wheel; one has to make the most of all the problems that have already been solved, and fortunately computer science makes it possible to reuse a solved problem."

> "The longer a program is useful, the longer it stays in use, but a program does nothing more than model a reality, and reality changes."

> "It is extremely important that whoever has to correct or modify a program can easily understand the program to be modified."

> "Write correct programs, yes, but above all write programs that speak to whoever reads them."

> "Robust is any object that resists when subject to pressures it was not designed for."

---

## Handling Input in C++ with `cin`

The lesson introduces the handling of data input in C++, using the `cin` object and the extraction operator `>>`. `cin` is seen as a variable able to store an unlimited number of characters typed by the user on the keyboard.

**Key Points:**
- The `cin` object stores the characters entered from the keyboard
- The `>>` operator is used to extract data from `cin` and assign it to a variable
- The input is read as a sequence of characters that must be converted into the data type of the destination variable
- A separator character (such as a space) must be used to distinguish consecutive numerical values
- If `cin` is empty, the execution of the program is suspended while waiting for the user's input

**Explanation:**
The statement `cin >> variable` extracts a sequence of characters from `cin`. These characters are transformed into a value of the type associated with the variable. The extraction ends when a character not compatible with the expected data type is met (e.g. a space for an integer), which acts as a separator. The user enters data into `cin` line by line, confirmed with the Enter key.

**Example:**
To provide the program with the values 25 and 3, the user must type on the keyboard the sequence of keys: "2", "5", one or more spaces, "3", and finally Enter.

**Calculation Steps:**
- The user types "2" and "5"
- Then enters a space as a separator, so that the input is not interpreted as the single number 253
- Then types "3"
- Finally presses Enter. This inserts all the characters typed ("2", "5", " ", "3") into the variable `cin`
- The first read statement extracts "2" and "5", converts them into the integer value 25 and assigns it to the variable. The space ends this first extraction
- The second read statement extracts "3" and assigns it to the next variable

---

## Importance of Variable Declarations

The declaration of a variable is fundamental in languages like C++. It serves both for the system to allocate memory and use the correct coding, and to verify that the operations used on the variable are consistent with its type.

**Key Points:**
- Allows the system to allocate adequate space in memory
- Ensures that the information is represented with the appropriate coding (e.g. integer, float, character)
- Allows the compiler to verify that the properties associated with the type are not violated during use (type checking)
- In case of incompatibility, the compiler reports the error, sometimes suggesting a fix
- Declarations can be factored, declaring several variables of the same type in a comma-separated list (e.g. `int base, exponent;`)

---

## Managing User-Program Interaction for Input

A potential deadlock problem during input is highlighted: the program stops waiting for data, but the user is not aware that they must provide it, resulting in an infinite mutual wait.

**Special Circumstances:**
- If the program waits for an input and the user does not know they must provide it, how should the situation be handled? The program should guide the user while entering data, for example by printing a message on screen asking for the information to be entered

---

## Input/Output Handling in C++ (`cin` and `cout`)

In C++, `cin` and `cout` are objects that manage streams of characters for input and output operations. `cin` is associated with the standard input (generally the keyboard) and uses the extraction operator (`>>`) to read data and convert it into the type of the destination variable. `cout` is associated with the standard output (generally the screen) and uses the insertion operator (`<<`) to convert data into a sequence of characters and display it.

**Key Points:**
- `cin` and `cout` are objects that represent unlimited streams of characters
- The extraction operator `>>` reads from `cin`, transforming the characters into the requested data type
- The insertion operator `<<` writes to `cout`, transforming a value into its character format
- The semantics of the operators `>>` and `<<` change according to the type of the variable they are used with
- Several read or write operations can be chained in a single statement (e.g. `cin >> base >> exponent;`)

**Explanation:**
When a statement like `cin >> variable;` is executed, the system runs a subprogram that extracts a sequence of characters from the input (e.g. "1", "2", "3") and transforms it into the corresponding numerical value (e.g. 123) to assign to the variable. Conversely, a statement like `cout << variable;` takes the internal value of the variable (e.g. 15625), converts it into a sequence of characters ("1", "5", "6", "2", "5"), and inserts it into the output stream, making it visible on the screen. These operators are polymorphic (overloaded), that is, their behavior automatically adapts to the type of the variable (integer, float, etc.).

---

## Using the iostream Library

The complex functionality of the `cin` and `cout` objects and of the related operators is not defined by the programmer but is made available through libraries provided with the C++ compiler. The library specific to input/output handling (Input/Output Stream) is `iostream.h`.

**Key Points:**
- The declarations of `cin` and `cout` are complex and handled by standard libraries
- The library for stream-based I/O is called `iostream.h`
- It is included in the program with the statement `#include <iostream.h>`
- The inclusion happens before compilation and is handled by the preprocessor
- The library also defines other useful elements, such as `endl` for the end-of-line character

**Explanation:**
To use `cin`, `cout`, `endl` and the operators `>>` and `<<`, the programmer must include the library `iostream.h` at the beginning of the source file. This is done through the preprocessor directive `#include <iostream.h>`. During compilation, this line is replaced with the content of the library, which contains all the declarations needed for the I/O operations to work correctly. Without this inclusion, the compiler would not recognize `cin`, `cout` and the other related elements.

---

## Output Formatting and User Interaction

It is essential that a program guides the user, showing clear messages both to request data and to present results. This is achieved by sending to `cout` not only the values of the variables, but also descriptive text strings.

**Key Points:**
- Use `cout` with strings between double quotes to display messages and prompts for the user
- It is good practice to precede the request for data with a message explaining what the program does
- Combine strings and variables in a single `cout` statement to create a formatted and readable output
- Use `endl` to insert an end-of-line character and move to the next line on the screen
- The printing of a numerical value can occur in a field of predefined width (e.g. 8 characters) with right justification

**Explanation:**
To display a message, a string of characters enclosed in double quotes is inserted into `cout`, for example: `cout << "Enter the base:";`. To present a result in an understandable way, strings and variables can be chained, as in: `cout << "The result of " << base << " raised to " << exponent << " is " << power;`. To go to a new line and improve readability, `endl` is inserted in the output stream. It is also possible for the system to allocate a fixed number of characters for printing a value (e.g. 8 characters), right-justifying the number and leaving spaces on the left if the value does not fill the whole field.

**Example:**
Instead of simply printing the numerical result (e.g. 15625), it is much more understandable for the user to see a complete message such as: "The exponentiation of 25 by 3 is 15,625".

**Calculation Steps:**
- A sequence of elements is sent to `cout`:
- The string "The exponentiation of "
- The value of the variable base (e.g. 25)
- The string " by " (note the leading space to separate it from the previous number)
- The value of the variable exponent (e.g. 3)
- The string " is "
- The value of the variable power (e.g. 15625)
- The corresponding C++ statement would be: `cout << "The exponentiation of " << base << " by " << exponent << " is " << power;`

---

## Steps for Creating and Running a Program

The steps needed to go from identifying a problem to obtaining the result through a computer are described.

**Key Points:**
- Define clearly and precisely what is to be obtained, the starting data and the desired results
- Understand the strategy to use to solve the problem (e.g. computing a power through successive products)
- Identify the objects and variables involved (e.g. base, exponent, power, partial product)
- Write the program in a high-level language (such as C++) using an editor program, which helps to enter and correct the code
- Translate (compile) the program from the high-level language into machine language through a translator program (compiler)
- Run the program in machine language, providing the input data to obtain the results as output

---

## The Operating System

The operating system is a complex program that acts as an interface between the user's requests and the complexity of the computer's hardware and software.

**Key Points:**
- It is the real interface between human wishes and the complexity of modern electronic computers
- It knows the precise situation of everything that happens in the machine and the characteristics of the various units
- It receives commands from the user (e.g. by typing the name of a program or clicking an icon) and triggers the operations needed to satisfy the request
- It manages the loading of programs (e.g. editor, compiler) into the execution memory
- It takes care of storing programs, associating the name given by the user with the specific area of memory, simplifying the interaction for humans

**Explanation:**
When a user wants to run an editor program, the operating system receives the command, goes to fetch the editor program from where it is stored, places it in the execution memory and starts its action. Once the user has finished and saves their work, the operating system manages the storage of the file, asking the user only to provide a name.

---

## Importance of Program Maintenance and Documentation

A program does not have the computing system as its only user, but also humans. For this reason, it must be written so that it is easily readable, understandable and modifiable.

**Key Points:**
- Programs need to be consulted again to correct errors (debugging). Often whoever corrects is not the same person who wrote the program
- Even a correct program needs changes over time, because the reality it models (e.g. the structure of a company) changes
- To be able to modify a program at reasonable cost, it is extremely necessary that it be written clearly and that it "speak", that is, explain its parts and the process it models
- The most immediate form of documentation is comments, statements ignored by the computer but which help humans understand the program better

**Example:**
A program that manages the information systems of a company, modeling the relationships and exchanges of information. If the structure of the company changes, the program must be updated to reflect this new reality.

**Calculation Steps:**
- The company reality changes, and if the information system supporting it is not modified accordingly, there would be a discrepancy between an updated company and an outdated information system, making it ineffective

---

## Importance of Code Readability and Maintainability

A program must be easily readable and understandable not only by whoever writes it, but also by whoever will have to modify or correct it in the future. The maintainability of software is a crucial aspect, since a program can behave unexpectedly because of data sequences not foreseen during development.

**Key Points:**
- A program is a static entity that represents a dynamic execution
- The writing of the program must make its components evident, possibly separate and corresponding to specific parts of the real world
- The goal is to write correct programs that "speak" to whoever reads them, clearly showing their structure and function
- Readability is obtained by choosing suitable names for the variables and by using comments

---

## The Use of Comments in Programming

Comments are phrases added to a program that are not considered by the computing system (compiler) but are fundamental for the human user. They serve to explain the logic, structure and purpose of parts of the code, improving understanding.

**Key Points:**
- Comments do not affect the translation and execution of the program
- They are extremely useful to allow humans to understand the program
- They can be used to describe the general purpose of the program
- They are useful to clarify the function of variables whose names are not self-explanatory
- They can signal restrictions on the data domain that are not imposed by the type of the variable (e.g. an integer variable that must be only positive)
- They make it possible to describe a sub-problem in words before implementing it in code, favoring a reading by levels of abstraction
- They can be used to allow a "dual reading" of the program: one for the computer (code) and one for humans (natural language text)

**Example 1 (multi-line comment):**
In C++, multi-line comments begin with the character sequence `/*` and end with `*/`. This type of comment is useful to describe the general purpose of a program at the start of the file. For example: `/* compute the exponentiation of an integer base to a positive integer exponent */`.

**Example 2 (single-line comment):**
Single-line comments begin with the double slash `//` and end at the end of the line itself. They are often used for short comments, such as attaching an explanation to a variable declaration or flagging a specific condition. For example, to indicate that an `int` variable exponent must in fact be positive: `// This must be a positive value; careful, if a negative one is given it does not work`.

**Example 3 (comment describing a complex operation):**
Use a comment to describe a complex operation that is then detailed by a series of statements. For example, instead of directly writing the code for a multiplication through successive sums, a comment such as `// Perform the product pot_partial times base` can be inserted. This allows the reader to understand the general intent at a higher level, without having to immerse themselves in the implementation details right away.

---

## Code Readability and Indentation

Indentation, that is, the way lines of code are aligned and shifted to the right, is a fundamental element of readability. A correct and consistent indentation discipline makes the structure of the program (e.g. the bodies of loops) immediately visible.

**Key Points:**
- The alignment of information (comments, curly brackets) is not random but follows a precise discipline
- An indented block of code (shifted to the right) indicates that it is part of a larger structure located further to the left
- The further to the left a statement is, the higher the level of the program structure it belongs to
- A program without an indentation logic is extremely hard to understand

**Explanation:**
In the course a consistent approach will be adopted, such as shifting the body of a do-while loop two characters inwards to show clearly that it is the body of the loop and belongs to that structure.

---

## Control Structures: Loops and Alternatives

The C++ language offers several control structures to manage the flow of execution. The choice of the correct structure is fundamental for the correctness of the program. The do-while and while loops and the if-else conditional structure are analyzed.

**Key Points:**
- The `do-while` loop executes its body at least once, since the condition for staying is checked at the end. This makes it unsuitable if the body of the loop may need not to be executed at all (e.g. computing the power with exponent 0)
- The `while` loop checks the condition for staying at the beginning. This allows the body of the loop to be executed zero or more times, solving the do-while problem with a zero exponent
- The `if-else` structure allows selecting which block of code to execute according to whether a condition is true. It is used to handle alternative situations
- If an `if` or `else` block must contain more than one statement, they must be grouped into a single block with curly brackets {}

**Example 1 (while):**
Syntax: `while (condition) { loop_body; }`

It is introduced to correctly handle the case in which the exponent is 0. If the exponent is 0, the condition of the while loop will be immediately false and the body will not be executed, leaving the correct result (which is 1, initialized earlier).

**Example 2 (if-else):**
Syntax: `if (condition) { statement_if_true; } else { statement_if_false; }`

It is used to handle the indeterminate case of 0 raised to 0. The condition `if (base == 0 && exponent == 0)` checks this situation. If true, it prints an error message; otherwise (`else`), it proceeds with the computation of the power as done before.

---

## Comparison and Assignment Operators in C++

In C++ (and in C), there is a fundamental distinction between the assignment operator and the equality comparison operator. This design choice reflects the philosophy of the language.

**Key Points:**
- The equality comparison operator is `==` (double equals)
- The assignment operator is `=` (single equals)
- This distinction is necessary because the symbol `=` had already been "spent" on the assignment operation
- Other languages, such as Pascal, made different choices (`:=` for assignment and `=` for comparison), reflecting a different philosophy (Pascal as a teaching language)
- The philosophy of C/C++ is that of an efficient language designed for expert programmers

**Explanation:**
The condition to check whether base and exponent are both zero is written as `base == 0 && exponent == 0`. The double equals `==` is used to compare the value of the variable base with the constant 0. Using a single equals would be an error, since it would try to assign 0 to the variable base instead of comparing it.

---

## Assignment, Comparison and Logical Operators in C++

In C++, the assignment operator (`=`) is distinct from the equality comparison operator (`==`). Assignment is a common operation, so it uses the shortest symbol. For comparison and other logical operations, character sequences such as `==`, `!=` (not equal) and `&&` (logical AND) are used, which must not be separated by spaces.

**Key Points:**
- Assignment: `=`
- Equality comparison: `==`
- Inequality comparison: `!=`
- Logical product (AND): `&&`
- The symbols of compound operators (e.g. `==`, `!=`, `&&`) must not be separated by spaces

**Explanation:**
Operators have an order of precedence. The equality operator (`==`) has higher precedence than the logical product operator (`&&`). In an expression like `base == 0 && exponent == 0`, the two equality conditions are evaluated first and then their Boolean results (true/false) are combined with the AND operator. Parentheses, although not necessary here, can be used to make the code more readable or to force a different order of evaluation.

---

## Robustness of a Program

Robustness is an important characteristic of a program, indicating its ability to withstand and handle incorrect uses or unforeseen data in its domain, without terminating abnormally or producing wrong results.

**Key Points:**
- A robust program is one that responds in a controlled way to incorrect use
- Example: a program that receives a negative exponent when it expects a positive value

**Special Circumstances:**
- If a program receives data outside its domain (e.g. a negative exponent), it should at least report the error to the user and terminate execution to avoid wrong calculations. A better solution is to allow the user to enter the correct data again, for example through a read loop that ends only when the data are valid

---

## Choice of Loop: Initial vs. Final Condition

The choice between a loop with an initial condition (such as `while` and `for`, which may be executed zero or more times) and a loop with a final condition (such as `do-while`, which is executed at least once) depends on the logic of the program.

**Key Points:**
- Final-condition loop (`do-while`): executed one or more times
- Initial-condition loop (`while`, `for`): executed zero or more times

**Explanation:**
For reading and validating input data, the final-condition loop is favored, since the body of the loop must be executed at least once to ask the user for the data. This gives the final-condition loop a "stronger semantics", because its mere presence in the code guarantees that the statements inside it will be executed at least once.

---

## Abbreviated Assignment Operators in C++

The C++ language offers abbreviated forms for assignment operations in which the variable that receives the result is also the first operand of the operation. This allows writing more concise code.

**Key Points:**
- `power *= base` is equivalent to `power = power * base`
- `products_left--` is equivalent to `products_left = products_left - 1`
- `counter++` is equivalent to `counter = counter + 1`

---

## Handling Negative Exponents

To compute the power with a negative exponent, the mathematical rule is used whereby a raised to a negative exponent equals 1 divided by a raised to the same exponent with the sign changed (a^−n = 1 / a^n).

**Key Points:**
- The mathematical rule is: a^−n = 1 / a^n

**Explanation:**
One approach to implement it is: if the exponent is negative, this information is stored (e.g. in a variable `sign`), the exponent is converted to positive and the power is computed normally. At the end, if the original exponent was negative, the final result will be 1 divided by the value of the computed power. It is possible to initialize the variable `sign` to 1 at the time of its declaration, assuming that the standard case is the one with a positive exponent.

---

## The `for` Loop in C++

The `for` loop is the third type of loop in C++ and gathers in a single line the initialization statement, the condition for staying in the loop and the statement to execute at the end of each iteration.

**Key Points:**
- The syntax is `for (initialization; condition; update) { ... }`
- The initialization is executed only once before the loop starts
- The condition is evaluated before each iteration
- The update is executed at the end of each iteration
- If the body of the loop contains a single statement, the curly brackets are not necessary

**Explanation:**
A while loop for computing the power can be transformed into a for loop. For example, `for (products_left = exponent; products_left > 0; products_left--)` moves the initialization (`products_left = exponent`), the condition (`products_left > 0`) and the update (`products_left--`) into the declaration of the loop, leaving in the body only the statement that updates the power.

---

## Division Between Integers and Type Conversions (Promotion)

In C++, division between two integer values produces an integer result, truncating any fractional part. To obtain a result with a decimal part (float or double), at least one of the operands must be of floating-point type.

**Key Points:**
- Division between integers truncates the decimal part (e.g. `1 / 2` gives 0)
- To obtain a fractional result, at least one operand must be of type float or double

**Explanation:**
The expression `1 / power`, where both are integers, will almost always give 0. To solve this, at least one of the operands must be turned into a floating-point value (e.g. `1.0 / power` or `1 / (float)power`). When an operation takes place between different types (e.g. int and float), the C++ system performs an automatic "promotion", converting the operand of "lower" type (int) to the "higher" type (float) to avoid loss of information. The inverse conversion, from float to int, is a "demotion" because the fractional part is lost.

---

## Tasks and Suggestions

- Exercises will be proposed in the next lesson
