# Modules 1-5: Programming Fundamentals and Program Translation

## Topic Overview

C++ programming, algorithms and the structure of the computer. The modules develop a program that computes the power of an integer, gradually moving from natural language and flow charts to C++ code, and use it to introduce the basic structure of a computer, the binary representation of data and the translation of a source program into machine language.

---

## Key Points Summary

1. Writing a program to compute the power of an integer
2. Use of flow charts to represent the logic of the program
3. Gradual transformation from natural language to a programming language (C++)
4. Understanding the essential characteristics of an electronic computer
5. Identification of all the possible situations in a process
6. Solving problems in successive steps and decomposing them into sub-problems
7. Use of iterative constructs (loops) to manage complexity
8. Importance of the reusability and generalization of a program
9. The concept of "identifiers" to represent variable data (e.g. base, exponent)
10. Basic structure of a computer: memory unit, I/O unit, processing unit

**Key Quotes:**
> "A program has a greater value the wider the set of data to which it can be applied or, in mathematical terms, the wider the domain of data our program can handle."

> "The cornerstone of this course is the ability to design, and one designs only gradually, taking individual decisions one after another."

> "Modern developments in programming techniques and languages are all aimed at making sure that, in the presence of errors that are bound to exist, those errors can be corrected more easily."

---

## Developing a Program for Exponentiation

The initial problem is to write a program able to compute a positive integer base raised to a positive integer exponent. The proposed approach is to develop the solution gradually.

**Key Points:**
- The problem is to compute the power of a positive integer
- The solution is first developed with flow charts and natural language
- The final goal is to translate the solution into a C++ program
- The transformation path helps to understand the architecture of the computer

**Explanation:**
It starts by using natural language and flow charts to describe the instructions. Then, over the course of 8 lessons, this scheme is transformed into a program written in a specific programming language, C++. This process also serves to understand the essential characteristics of an electronic computer in order to write better programs.

---

## Key Principles of Programming

The first example program highlighted three fundamental aspects that will be central to the whole programming course.

**Key Points:**
- All the possible situations, even the rarest and most exceptional ones that may arise during the process, must be identified, and for each situation the program must provide the actions to take
- The solution is written in successive steps, where the solution to complex sub-problems is detailed in terms of simpler sub-problems
- Iterative constructs, called loops, are a powerful tool for breaking down the complexity of problems

---

## Reusability and Generalization

A program gains more value the wider the set of data it can handle. A program specific to computing "5 to the power of 7" has limited usefulness.

**Key Points:**
- A program is more valuable if it can be applied to a wide domain of data
- Specificity (e.g. computing only 5^7) limits reusability
- Generalization is obtained by using identifiers in place of constant values
- Identifiers are names that represent variable values

**Explanation:**
To make a program reusable, the specific values (e.g. 5 and 7) are replaced with generic names called "identifiers" (e.g. "base", "exponent", "power"). In this way the program can be applied to a wide range of pairs of values, increasing its domain of applicability and therefore its value.

---

## Basic Structure of an Electronic Computer

To understand how a program is executed, a simplified structure of the computer is presented, made up of three main units.

**Key Points:**
- **Memory unit:** meant to store all the information useful for the execution of a program, associating values with identifiers in dedicated "boxes"
- **Input and Output (I/O) units:** allow the computer to receive data (input, e.g. from the keyboard) and provide results (output, e.g. on the screen). They manage the interaction with the user
- **Processing unit:** has the ability to carry out processing, that is, to perform operations on the stored data

**Explanation:**
When a program is executed, it interacts with different parts of the computer. The user provides data through an input unit (keyboard), these data are saved in "boxes" of the memory unit associated with identifiers. The processing unit takes these data, performs the calculations and saves the result back in memory. Finally, the result is communicated to the user through an output unit (screen).

---

## Programming Languages: Syntax and Semantics

A computer is not able to understand a complex natural language such as Italian. It must therefore receive commands expressed in a language with a much simpler and more rigid syntax.

**Key Points:**
- Computers require languages with simple and unambiguous syntax
- Mathematical symbols are used for the operators (e.g. "*" for multiplication)
- "Keywords" are terms with a fixed meaning that cannot be used freely by the programmer
- "Syntax" is the way an instruction is written
- The assignment operator "=" separates the identifier that receives the value from the expression that computes it

**Explanation:**
Programming languages use symbols (often taken from mathematics, such as "*" for multiplication) and "keywords" (words with a predefined meaning, such as "raised to" in the example). "Syntax" defines how to write an instruction, while "semantics" defines its meaning. For example, the assignment instruction "power = base raised to exponent" uses the symbol "=" and the keyword "raised to" to define a calculation and where to store its result.

**Example:**
The first computer brought to the Politecnico from the United States by Professor Dada in 1954 had only 1024 words of memory, executed 70 instructions per second and cost $120,000 at the time.

---

## Problem Decomposition and Solution Strategy

The computer usually has no hardware component to directly perform complex operations such as exponentiation. It is therefore necessary to break the problem down into simpler operations that the computer can perform.

**Key Points:**
- Complex problems must be solved using simpler tools
- The programmer must invent a solution strategy (algorithm)
- Exponentiation can be done through repeated multiplications
- The multiplication operator in programming languages is typically represented by the asterisk symbol (*)

**Explanation:**
The problem of computing "base raised to exponent" is solved using a lower-level operation, multiplication. The programmer must invent a strategy (algorithm) to obtain the desired result. Elementary mathematics suggests that exponentiation can be obtained by repeating the multiplication operation: the base is multiplied by itself as many times as the exponent indicates. This requires designing a process, typically a loop, that generates a succession of partial values up to the final result.

**Example:**
Computing the value of 5 raised to the seventh power.

**Calculation Steps:**
- The instruction "read base" acquires the value 5 and stores it in the memory box "base"
- The instruction "read exponent" acquires the value 7 and stores it in the box "exponent"
- The instruction "raise base to exponent and assign the result to power" sends the values 5 and 7 to the processing unit
- The processing unit computes 5^7, obtaining 78,125
- The result 78,125 is stored in the memory box "power"
- The instruction "write power" transfers the value 78,125 to the screen for the user
- The program ends

---

## Implementing Exponentiation with an Iterative Loop

To compute the value of a base raised to an exponent, an iterative construct (a loop) is used. The challenge is to go from the initial value (base) to the final value (base raised to exponent) through a series of partial values, always using the same instruction inside the loop.

**Key Points:**
- The complex problem of exponentiation is solved by repeating a simpler operation (the product)
- The instruction inside a loop must be the same at every iteration
- Considerable intellectual ability is needed to decompose a complex problem into simple repetitive operations
- A variable "partial" is used to store the intermediate results
- A possible implementation initializes the variable partial to 1 and runs the loop a number of times equal to the exponent

**Explanation:**
The proposed solution is to associate the same name, for example "partial", with every partial value. At each iteration of the loop, the value of "partial" is updated. It starts from an initial value and repeats an update instruction. A variant initializes "partial" to 1 (the neutral element of the product) and runs the loop "exponent" times. The instruction in the loop is `partial = partial * base`. At the end of the loop, the final result contained in "partial" is assigned to a variable "power".

---

## The Concept of Variable

The identifiers used in the program, such as "base", "exponent", "power" and "partial", are called variables. A variable represents a "box" in memory whose associated value can change during the execution of the program.

**Key Points:**
- Variables are identifiers that represent values that can change
- Two types of variables can be distinguished: those needed for the specification of the problem (data and results, e.g. "base", "power") and those tied to the solution strategy (working variables, e.g. "partial")

**Explanation:**
The variable "partial" is an obvious example, since its value changes every time the body of the loop is executed. The other variables such as "base", "exponent" and "power" also change value, but less frequently: "base" and "exponent" after the read operation, and "power" at the end of the loop, when the final value of "partial" is assigned to it.

---

## Loop Control Through a Counter

To execute the body of the loop a specific number of times (equal to the exponent), the condition for staying in the loop must be translated into a simple test that the computer can understand. This is achieved by introducing a variable that acts as a counter.

**Key Points:**
- The computer can only perform simple tests, typically the comparison between two values
- A counter is needed to manage the number of executions of a loop
- The choice of the variable name is important for readability (e.g. `iterDone`)
- A naming convention is suggested: use a capital letter at the start of the words after the first in a compound variable name (e.g. `iterDone`)

**Explanation:**
Two main strategies are presented:

1. **Increasing counter:** a variable (e.g. `iterDone`) is introduced to count the iterations already executed. It is initialized to 0 before the loop and incremented by 1 at each iteration. The condition for staying in the loop is `iterDone < exponent`
2. **Decreasing counter:** a variable (e.g. `iterLeft`) is introduced to count how many iterations are missing. It is initialized to the value of the exponent before the loop and decremented by 1 at each iteration. The condition for staying is `iterLeft > 0`

**Example 1 (increasing counter):**
Using a variable `iterDone` to count the completed iterations.

**Calculation Steps:**
- Initialize the variable to zero before the loop: `iterDone = 0`
- At each execution of the body of the loop, increment the variable: `iterDone = iterDone + 1`
- The condition for staying in the loop is that the value of `iterDone` is less than the value of `exponent`

**Example 2 (decreasing counter):**
Using a variable `iterLeft` to count the remaining iterations.

**Calculation Steps:**
- Initialize the variable to the value of the exponent before the loop: `iterLeft = exponent`
- At each execution of the body of the loop, decrement the variable: `iterLeft = iterLeft - 1`
- The condition for staying in the loop is that the value of `iterLeft` is greater than zero

---

## Program Correctness

This addresses the problem of how to be sure that a program does what the problem specification requires.

**Key Points:**
- Formal proof of correctness is complex and used only in extremely critical cases
- Testing is the common alternative for gaining confidence in the correctness of a program
- Testing does not guarantee correctness 100%

**Explanation:**
There are formal methods for mathematically proving the correctness of programs, but their formalism and the effort required limit their use to critical cases, such as the software that manages a nuclear reactor. As an alternative, "testing" is used, that is, trying the program with various data in order to be "sufficiently confident" that it works correctly, without having an absolute guarantee.

**Example:**
An example of a program where guaranteeing correctness is essential is the one that manages the core of a nuclear reactor. In these cases, because of the potentially catastrophic consequences of an error, every possible effort must be made to ensure the correctness of the program, resorting even to complex formal methods.

---

## Program Testing Strategies

The task of computer engineering is to provide techniques for writing correct programs. However, errors are inevitable. Modern development aims to make errors easier to correct, and this is achieved through testing the program.

**Key Points:**
- It is crucial to choose sets of test data capable of "touching" the program in all its significant points
- **First strategy (specification-based):** create the test data starting from what the program must do, trying to cover all possible cases
- **Second strategy (structure-based):** once the program is written, use a set of input data that guarantees that all the different internal parts of the program are executed and checked

**Example:**
To test a program that raises a number to a power (e.g. 5^7), a simpler but significant case is chosen, such as 5 squared (5^2).

**Calculation Steps:**
- Using the exponent 2 is the simplest example that forces the program to execute the body of the loop at least twice
- This makes it possible to test not only the entry into the loop but also the condition for staying in it and the repetition of the body of the loop itself

---

## From Graphical (Flow Chart) to Textual Representation

The solution of a problem, initially represented in a two-dimensional graphical way with a flow chart, must be transformed into text, that is, a one-dimensional succession of instructions that the computer can execute.

**Key Points:**
- A flow chart is a two-dimensional representation, whereas executable code is a one-dimensional succession of instructions
- Textual instructions are executed one after the other, unless the flow is altered
- Control structures (e.g. do-while loops) are preferable to jumps (goto) because they improve the structure and readability of the program

**Explanation:**
The main problem in this transformation is how to handle branches and loops, where an instruction can have several possible successors. Two solutions are presented:

1. **Jump instructions:** an instruction is labeled (e.g. `loop:`) and a conditional jump instruction (e.g. `if condition holds go to loop`) is used to alter the sequential flow of execution. This makes it possible to go back or to skip forward in the code
2. **Control structures:** compound instructions that manage an entire block of logic, such as a loop, are used. For example, an instruction like `do [body of the loop] while [condition]` represents the entire loop in a structured way. This is the solution preferred by modern programming languages (Pascal, C, C++) because it makes the program clearer, more readable and easier to modify

---

## Functional Abstraction: Implementing Multiplication Through Sums

If a computer cannot perform a complex operation such as multiplication, this can be implemented through a loop of simpler operations, such as addition.

**Example:**
The operation `partial * base` is replaced by an inner loop that repeatedly performs sums.

**Calculation Steps:**
- A temporary variable, `partial_product`, is introduced, initialized to 0 (the neutral element for the sum)
- A loop is run that repeats `base` times
- At each iteration, the value of partial is added to `partial_product`
- At the end of the loop, the result contained in `partial_product` is the new value of partial

**Considerations:**
- When nested logic is introduced (a loop inside another), it becomes essential to use clear and meaningful variable names to maintain readability. For example, `partial` is renamed `partial_pow`, `iter_left` is renamed `products_left`, and `partial_product` and `sums_left` are introduced for the inner loop

---

## Introduction to C++ Syntax

The basic syntactic rules for transforming pseudo-code into a C++ program are presented.

**Key Points:**
- **Statement terminator:** in C++, every statement (simple or compound) must end with a semicolon (;). This allows several statements on one line or a single statement across several lines
- **Keywords in English:** the keywords of the pseudo-code are replaced by their English equivalents. "execute" becomes `do`, and "as long as" becomes `while`
- **Syntax of the while loop:** the condition for staying in the loop is always enclosed in round brackets () after the keyword `while`
- **Body of the loop:** if the body of a loop (or of another structure) contains more than one statement, it must be grouped (typically between curly brackets {})

---

## Program Structure and Subprograms (Functions)

A complex problem is divided into smaller sub-problems, whose solutions are organized through subprograms. C++ represents the solutions of both the main program and the individual sub-problems by means of functions.

**Key Points:**
- A non-trivial problem requires a subdivision into smaller sub-problems, creating a tree structure
- The solution to the starting problem is the main program, while the solutions to the sub-problems are handled by subprograms
- In C++, both the main program and the subprograms are represented by "functions"
- Each function is characterized by a name (identifier), can receive information (parameters) between round brackets and can return a result
- The main program in C++ is always represented by the function named `main`
- The return type `void` indicates that the function returns no value
- The code of a function, that is, the sequence of statements that compose it, is enclosed between curly brackets {}

---

## Data Representation: Bits and Binary Coding

All the information inside an electronic computer is represented by physical elements that can take only two states, conventionally indicated by the digits 0 and 1. These elements are called bits.

**Key Points:**
- Every type of data (numbers, text, etc.) is represented by elements that can be in only two states (0 or 1)
- The single element of information is called a "bit" and can only discriminate between two values
- To represent information that can take more than two values, a succession of bits is used
- With "n" bits it is possible to represent 2 to the power of "n" different values
- The one-to-one correspondence table between a piece of information and its representative succession of bits is called the "binary coding" of the information

**Example:**
Calculating how many values can be represented with 1, 2 and 3 bits.

**Calculation Steps:**
- With 1 bit, 2 pieces of information are represented (0, 1)
- Adding a second bit, for each value of the first (0 or 1), the second can be 0 or 1. So there are 2 × 2 = 4 possible values
- Adding a third bit, for each of the 4 previous configurations, a 0 or a 1 can be added, multiplying by 2 again. So there are 2 × 2 × 2 = 8 values
- As a result, with n elements (bits) there can be 2^n different configurations

---

## Representation of Numerical Information

Numerical information, such as integers or numbers with a fractional part, is represented using specific binary codings, such as binary numeration for integers or floating-point notation for real numbers.

**Key Points:**
- **Unsigned positive integers:** represented using the rules of binary numeration. The minimum number of bits typically used is 16
- **Signed integers:** an additional bit is used to represent the sign (+ or −). If 16 bits in total are used, 1 bit is for the sign and 15 for the absolute value
- **Numbers with a fractional part (fixed point):** a certain number of bits is assigned to the sign, another to the integer part and another to the fractional part
- **Numbers with a fractional part (floating point):** the values are transformed into exponential notation, separating the mantissa (significant digits) from the exponent (magnitude of the number). This format is called "float"

**Explanation:**
Floating-point representation is the most used for numbers with a fractional part. A number like 25.38 is transformed into exponential notation, for example 0.2538 × 10^2. In this way the "mantissa" (0.2538), which represents the significant digits, is separated from the "exponent" (+2), which defines its magnitude (both for large numbers and very small ones). This method is so efficient that it is also used to represent very large integers that would exceed the standard representation capacity. The name "floating point" comes from the fact that, to perform operations such as addition, the numbers are aligned by bringing them to the same exponent, an operation equivalent to shifting (a "movement" of) the point.

**Example:**
To represent the numbers from 0 to 31 (32 values), 5 bits are needed (since 2^5 = 32).

The representation of the number 25 unsigned and of the numbers +25 and −25 signed is shown, where an additional bit is dedicated to indicating whether the value is positive or negative.

The number 25.38 is represented as 0.2538 × 10 to the power of +2.

**Calculation Steps:**
- The succession of significant digits (mantissa: 0.2538) is separated from the magnitude of the value (exponent: +2)
- This makes it possible to represent very large numbers (with a large positive exponent) or very small ones (with a large negative exponent) using few bits for the exponent

---

## Representation of Textual Information and ASCII Coding

Non-numerical information, such as text, is represented by breaking it down into its smallest element, the character. There are different codings to associate a binary value with each character; one of the most important is the ASCII coding.

**Key Points:**
- Textual information (books, articles, programs) is represented as a sequence of characters
- The set of characters to be represented includes: uppercase and lowercase letters (e.g. 26 × 2 = 52), the 10 decimal digits, punctuation marks and control characters
- Control characters are not printable but serve to manage the text (e.g. end of line, end of file) or for communication between hardware components
- The ASCII coding (American Standard Code for Information Interchange) is a standard that uses 8 bits to represent 256 different characters, a number considered sufficient for most applications

---

## Memory Organization: Bytes and Cells

The computer's memory is organized into fundamental units called bytes. The size of the memory and the allocation for the different data types are based on multiples of bytes.

**Key Points:**
- The amount of bits necessary to store a single character (typically 8 bits) has a specific name: "byte"
- The byte is the minimum element of memory organization, since most of the information is of character type
- Memory sizes are defined in multiples of bytes: Kilobyte (KB, about 1000 bytes, precisely 2^10), Megabyte (MB, about a million), Gigabyte (GB, about a billion), Terabyte (TB, about a thousand billion)
- The bytes in memory are grouped into "cells", which can contain 2, 4 or 8 bytes depending on the architecture
- A modern computer typically assigns 2 or 4 bytes for storing an integer value and 4 or 8 bytes for a floating-point value

---

## Machine Language, Code Translation and Programming

This part of the lesson explores the path of a program written in C++ from the moment of its creation to its execution by an electronic computer. It concentrates in particular on the complex translation process that transforms the source code, understandable to humans, into machine language, the only form the computer is able to understand and execute, highlighting the challenges and technical solutions involved.

### Key Points

1. Representation of a program in memory as a succession of characters, organized in lines and successive positions to ease scanning
2. The translation process from the source language (e.g. C++) to machine language
3. Role of the translator program in analyzing and transforming the code, which solves the problem of making the program quickly executable by the computer
4. Scanning and interpretation of the source code character by character to identify elements such as variables and operators. This includes recognizing identifiers (variable names) and assignment operators, and understanding the syntax to determine the operation to execute
5. Inefficiency of directly executing the source code and need for translation, even for modern, fast computers with ample memory, because of the complexity of interpreting character by character
6. The transformation of the source code into a form suitable for quick use by the computer
7. Dependence of the translated program on the specific architecture of the computer and its instruction set, since every computer has a unique repertoire of instructions it is able to execute
8. The use of registers (e.g. "register a") as temporary memory for data and results in the processing unit, which temporarily hold the values the processing unit must operate on and the results obtained, before they are stored permanently in main memory
9. Assembly language as an intermediate representation of machine instructions (e.g. load, multiply, store). This form is more concise than the source code and closer to machine language
10. The final coding of the instructions into sequences of bits (object or absolute language), where each instruction is represented by a sequence of bits with specific fields for the operation code and the memory addresses, making it the only form directly understandable and executable by the computer

**Key Quote:**
> "All the programs the computer executes must in the end be transformed into this language."

---

## Translation from Source Language to Machine Language

A program written in a high-level language such as C++ (source language) is not executed directly by the computer. It must first be transformed, by a special program called a translator, into a sequence of elementary instructions that the processor is able to understand and execute (machine language or object language). This process is fundamental for efficiency, since the direct interpretation of the source text would be extremely slow.

**Key Points:**
- The computer does not execute the program in the source format (e.g. C++), but executes it after transforming it into a format it can represent and execute quickly
- The form into which the program is transformed depends strictly on the internal structure and the specific instruction set of each computer
- The translation depends on the data type associated with the variables (e.g. `int` or `float`), since the bit-level operations for a multiplication between integers are different from those for a multiplication between floating-point numbers. This implies that the same operation in C++ (e.g. multiplication) can require completely different sequences of machine instructions depending on the data type of the operands
- The final result of the translation is the object (or absolute) language, a sequence of bits that represents the instructions and that is the only language the computer truly understands

**Explanation:**
The translator analyzes the source program, which is a sequence of characters. For example, faced with the instruction `pot_partial = pot_partial * base;`, the translator performs a scan. It recognizes `pot_partial` as a variable identifier, `=` as the assignment operator, and `pot_partial * base` as an expression. It understands that it must compute the product of the values of the two variables and assign the result to the variable on the left. The semicolon, for instance, indicates the end of an identifier and of the statement itself. This single C++ statement is then broken down into a series of simpler machine instructions, specific to the computer's architecture.

**Example:**
Consider a C++ statement: `pot_partial = pot_partial * base;`. Suppose a simple computer with a processing unit equipped with a single temporary register called "register a".

**Calculation Steps:**
- The C++ statement is translated into the following sequence of three machine instructions:
- `load a, pot_partial`: this instruction loads (copies) the value contained in the memory box of the variable `pot_partial` into "register a"
- `multiply a, base`: this instruction multiplies the value currently in "register a" by the value of the variable `base`. The result of the product is stored again in "register a", overwriting the previous value
- `store a, pot_partial`: this last instruction takes the final result in "register a" and saves (stores) it in the memory box corresponding to the variable `pot_partial`, updating its value

**Tips:**
- To allow the translator to operate correctly, the type of every variable used in the program (e.g. base, exponent, power, pot_partial) must be declared. This is done using keywords such as `int` for integers or `float` for floating-point numbers. The type declaration is fundamental because it defines the convention for representing the value in memory and the operations that can be performed on it
