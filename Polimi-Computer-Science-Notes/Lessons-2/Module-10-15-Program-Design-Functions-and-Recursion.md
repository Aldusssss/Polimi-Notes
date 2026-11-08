# Modules 10-15: Program Design, Functions and Recursion

## Topic Overview

The lessons cover the development cycle from a problem in natural language to its coding in C++, with an emphasis on the specification. They deal with input/parsing, pseudocode, loop design, termination with a sentinel/EOF, functions and interfaces (global variables, parameters by value/by address, return value), the environment model and recursion, comparing iterative and recursive approaches for the power and the factorial. They include a case study on Fermat and practical tips.

---

## Key Points Summary

1. Program development cycle: from the formulation in natural language to the coding in C++
2. Difference between the design phase and the specification phase; greater attention to the specification in this lesson
3. Handling data in sequence instead of just two numbers
4. Possible incompleteness of the specification and how to behave in such cases
5. Five exercises: 1 on two numbers; 2 and 3 on a sequence of numbers; the last 2 on a sequence of characters
6. Availability of commented code and explanatory notes, which students may modify
7. Use of pseudocode and flow charts in the design of the algorithm
8. Passage from pseudocode to C++, to be analyzed by the students
9. Scenario and choice of simple input data to guide the solution strategy
10. Introduction of variables and identification of sub-problems in the intermediate versions of the program

**Key Quotes:**
> "The goal is, even if we use Italian, to express it with the greatest possible conciseness and precision."

> "Defining in a single place what can change is the simplest way to keep everything else consistent."

> "The identification of sub-problems and their solution through specific functions requires that the functions cooperate with each other to achieve the desired objective in the whole program."

> "The function, defined up to formal parameters, becomes completely autonomous thanks to parameter passing, applying to different inputs and outputs without changing its description."

> "Recursion is a very powerful conceptual tool that allows, in certain situations, to describe the function directly using the specification of the problem, without choosing a solution strategy."

> "Whenever we have a situation in which an object needs to use itself, we speak of a recursive-type definition."

> "In the presence of recursive functions, it is absolutely necessary to have a dynamic mechanism for activating the copy of the local environment."

---

## Program Development Cycle (Analysis, Specification, Design, Coding)

Complete process to go from the real problem, often incomplete, to a sufficiently precise specification, up to the design with scenarios and the coding in C++. It includes building intermediate versions with pseudocode and possible reformulations of the strategy, and the introduction of new variables and sub-problems.

**Key Points:**
- Starting from a problem in natural language, often not completely defined
- Analysis phase to obtain a sufficiently precise specification
- Greater attention to the specification phase in this lesson
- Design with scenarios and simple input data (manageable with pen and paper)
- Intermediate versions of the program with pseudocode, enclosed between double quotes
- Iterations on the design: new variables, new sub-problems, adjustments to the strategy
- Progressive approach to the final program
- Commented code with explanatory notes for particular choices or new concepts

**Explanation:**
The instructor introduces a systematic approach: from the real problem an analysis is carried out to clarify the requirements. A specification precise enough to start the design is produced. Scenarios are used to reason on concrete and simple data. The solution evolves through intermediate versions with pseudocode, identifying the sub-problems and variables needed. The design is refined up to the C++ coding, with commented code and notes. The lesson emphasizes the specification because it is often incomplete and requires operational decisions.

**Example:**
Problem: compute the sum of a sequence of data provided in succession by the user. Type of values: signed integers (variable of type `int`). Input mode: the user enters the values one by one, with an optional "+" or "−" sign, followed by the digits; the system sends them to `cout` as an echo on screen. When Enter is pressed, the sequence of characters is queued in `cin` and transformed into an integer value stored in a variable whose name is to be defined. The program must also handle an empty sequence of elements, to prepare for special cases in more complex programs. Two variants of the specification: 1) provide the size of the sequence first (e.g. 5 elements) and then the values; 2) do not provide the size and signal the termination of the sequence. Design: use an initial-condition loop to handle even empty sequences. Preferred iterative strategy: maintain a variable `sum` and update it with each new addend stored in the variable `addend`. For the variant with size: introduce a variable `size` and a variable `howMany` to track the addends read and compare with `size`. Evaluation: the solution with size known in advance is fragile (counting one element more or less is enough to put the program in crisis); it is more reasonable not to fix the size and to provide a termination mechanism.

**Calculation Steps:**
- Definition of the type: signed integers, variable of type `int`
- Input mode: characters with sign and digits, echo on `cout`, acquisition on `cin`, parsing into `int`
- Choice of the specification: initial size vs. signaled termination
- Initial-condition loop to allow empty sequences
- Incremental sum: variable `sum`, variable `addend`
- Control of the loop with the variable `howMany` and comparison with `size`
- Analysis of the limits of the size known in advance and motivation for the variant with termination

**Considerations:**
- The specification may be incomplete: document the assumptions and show how to behave
- Guide the non-expert user with input one by one and echo on screen
- Support empty sequences for compatibility with more complex programs
- Prefer the iterative sum to avoid many temporary variables
- Avoid fixing the size in advance because of counting errors
- Comment the code and provide explanatory notes for particular choices
- Use scenarios with simple data to design the strategy

**Special Circumstances:**
- If the specification turns out to be incomplete, how should it be handled? Carry out an analysis phase to make it precise, make the assumptions explicit and update the solution strategy
- If an empty sequence of elements occurs, how should it be handled? Design the initial-condition loop to handle the empty case and return the correct sum (typically 0)
- If the user miscounts the number of elements, how should it be handled? Avoid asking for the size in advance and adopt a termination mechanism for the sequence

---

## User Input and Parsing in C++ (`cin`, `cout`, Echo, Transformation into `int`)

Input mode with sign and digits, echo on `cout`, queuing on `cin`, reading through suitable statements and storage in an integer variable. Importance of choosing clear variable names (e.g. addend, sum, size, howMany).

**Key Points:**
- The user enters a "+" or "−" sign and digits
- Echo on `cout` for each character typed
- When Enter is pressed, the input is queued in `cin`
- Read statement that transforms the sequence of characters into an integer
- Storage in a variable of type `int` whose name is to be defined

**Explanation:**
The input flow is described step by step: the user enters the characters, the system echoes them on screen, and on confirmation with Enter the data are available on `cin` for reading. A parsing function/statement converts the characters into an `int`. The clear organization of the variables makes it easier to update the sum later.

**Considerations:**
- Guide the user while typing to reduce errors
- Ensure that the reading handles the sign and non-empty sequences
- Comment the code to clarify the transformation from `char` to `int`

**Special Circumstances:**
- If the user enters non-numeric input, how should it be handled? Provide a validity check and a request to re-enter

---

## Pseudocode, Flow Charts and Intermediate Versions

Use of pseudocode and flow charts to express the algorithm, with intermediate versions that may contain sub-problems in Italian, enclosed between double quotes, up to the final program.

**Key Points:**
- Pseudocode as a non-formalized language for specifying algorithms
- Flow charts to represent control
- Intermediate versions with parts that are not yet executable
- Refactoring of variables and sub-problems during the iterations

**Explanation:**
The design favors initial clarity through pseudocode and flow charts. The iterations add implementation details and gradually replace the pseudocode with C++. This progression makes it possible to handle special cases and to clarify the specification.

**Considerations:**
- Maintain the greatest conciseness and precision even in natural language
- Isolate sub-problems and assign clear names

**Special Circumstances:**
- If new sub-problems emerge during development, how should it be handled? Note the updated specification, introduce new variables and refine the flow

---

## Designing an Initial-Condition Loop for Sequences of Data

Choice of using an initial-condition loop to handle empty sequences too and to iteratively update the sum with each new input.

**Key Points:**
- Handling of staying in the loop with an initial condition
- Use of a variable `howMany` for counting when the size is known
- Update of `sum` with `addend` at each iteration
- Preference for the incremental sum over storing all the data

**Explanation:**
The loop controls the reading of data and the update of the sum. In the variant with size, `howMany` is compared with `size`. In the variant with termination, an end-of-input signal is evaluated. The choice of the incremental sum reduces the number of variables and simplifies memory.

**Considerations:**
- Design the exit condition in a robust way
- Minimize temporary variables

**Special Circumstances:**
- If the input may be empty, how should it be handled? Establish that the initial sum is 0 and that the loop is not entered if there is no data

---

## Evaluating Specifications: Size in Advance vs. Termination

Analysis of the pros and cons of the two variants of the specification. The variant with size in advance is fragile because of counting errors; the variant with termination is preferable for robustness and generality.

**Key Points:**
- **Size in advance:** requires a variable `size` and a check with `howMany`
- Risk of error if the count of elements is wrong (one more or one less)
- **Termination:** the data are provided and the end of the sequence is signaled
- Wider applicability and reduction of operating errors

**Explanation:**
The lesson shows a first solution that asks for the size, but highlights its practical limits. It proposes as more reasonable an approach that does not require the size and uses an end-of-input mechanism, making the program less vulnerable to user errors.

**Considerations:**
- Design the user interface so that the end of the data is clear

**Special Circumstances:**
- If the user enters a number of elements different from the expected one, how should it be handled? Prefer the variant with termination to avoid inconsistencies

---

## Input Termination with a Sentinel Value and with EOF

Two strategies to terminate a sequence of inputs: 1) a sentinel value chosen so that it cannot belong to the data; 2) end-of-data signaling via EOF, on Windows with Ctrl+Z, detected through a function associated with `cin` that becomes true at the end of the stream.

**Key Points:**
- A sentinel value implies a constraint on the data that can be entered
- The user can specify the end value (variable `end`)
- EOF is handled as a function associated with `cin` (`cin.eof()`)
- `cin.eof()` is false during reading and becomes true at the end of the stream
- It requires including the I/O functionality (`iostream.h` mentioned)

**Explanation:**
If a value that will not appear in the sequence cannot be guaranteed, EOF is used. On Windows the user presses Ctrl+Z to signal the end of the data. After a read operation, `cin.eof()` is tested: if it is false, the data read is valid and is processed; if it becomes true, the loop is exited. With the sentinel value, a constraint is imposed in advance: for example, if the data are positive, a negative one ends the sequence. The user can choose the sentinel as long as it does not belong to the data.

**Example:**
The user enters a sequence of integers separated by at least one space, without an iterative prompt for each addend. At the end, they press Ctrl+Z. The program keeps reading until `cin.eof()` becomes true, updating the sum and then requesting the next addend.

**Calculation Steps:**
- An initial message is shown explaining: enter integers separated by spaces, press Ctrl+Z to end
- The loop is structured as `while (cin.eof() is not true) { update sum; read next addend }`
- When the user sends only the end character (Ctrl+Z), `eof()` becomes true and the loop is exited

---

## Loop Structures: External Condition vs. `break` from an Infinite Loop

A loop can be governed by a condition for staying that becomes false in order to exit, or it can be an infinite loop (e.g. `while(1)`) with an internal break statement (`break`) when the termination condition occurs.

**Key Points:**
- **Version 1:** `while (condition)` with a condition based on `cin.eof()` not being true
- **Version 2:** `while (1)` with the check inside and `break` at the end condition
- Semantic equivalence if the exit condition is correctly detected
- The choice affects readability and the location of the termination logic

**Explanation:**
If `while (cin.eof() is not true)` is adopted, the condition is explicit at the entry. Alternatively, `while (1)` is written and in the body the program reads and tests EOF or the end condition: if true, `break` is executed. Both models are acceptable; the second centralizes the break in the body.

**Example:**
Implementation with `while (1)`: the program tries to read the next addend; if after the read `cin.eof()` is true, it does `break`; otherwise it updates the sum and continues.

**Calculation Steps:**
- Initialization of the sum before the loop
- Inside the loop: input; test `eof()`; if true `break`; otherwise `sum += addend`
- At the end, print the result

---

## Order of Reading and Updating in the Loop

If the continuation condition depends on the value read (e.g. sentinel or EOF), a first element must be read before entering the loop. In the body of the loop, the typical order becomes: process the current element, then acquire the next.

**Key Points:**
- First read outside the loop to be able to test the condition at the entry
- In the body: update the sum, then read the next addend
- Ensures that the last value is not lost and that the condition can be evaluated

**Explanation:**
The condition "is there more data to acquire?" requires a datum to test. A preliminary read is therefore done. Then, at the start of each iteration, a valid addend is available: the sum is updated and then the next is read, preparing the condition for the following iteration.

---

## Symbolic Constants for Readability (`const int false`)

Replacing literal values such as 0 with symbolic constants improves readability. A constant defined with `const` cannot be modified during execution.

**Key Points:**
- `const int false;` used in place of 0 in Boolean conditions
- Improves the understandability of comparisons/conditions
- Immutability constraint during the program

**Explanation:**
By defining `const int false` with an appropriate value, the code becomes more expressive: comparisons and conditions are clearer than using 0. This approach reduces ambiguity and helps maintenance.

---

## Batch Input Mode Without an Iterative Prompt

An expert user can provide all the integers in sequence, separated by at least one space, and end with Ctrl+Z. The program reads and processes without asking for confirmations for each addend.

**Key Points:**
- Reduces the verbosity of the interaction
- Requires clear initial instructions on separators and termination
- Compatible with iterative reading from the stream

**Explanation:**
At startup, a message is printed: enter all the data, separated by spaces, and press Ctrl+Z to end. The loop consumes the available integers until it receives EOF.

---

## Introduction to Functions and Code Reuse

Functions encapsulate fragments of code, have a name and can be called several times. They allow modularity, reuse and easy maintenance: changes in one place propagate to all the calls.

**Key Points:**
- Definition similar to `main` but with a name chosen by the user
- Expressive name (e.g. `raiseToPower`) following lexical conventions
- Code enclosed between curly brackets
- Calls replace duplications of the fragment
- **Advantages:** single point of modification, fewer errors, global consistency

**Explanation:**
The replicated fragment (computation of the power) is encapsulated in a dedicated function. In the program, the three copies are replaced by three calls to the function. If the algorithm is changed, only the definition of the function is modified.

**Example:**
A function is defined that assumes positive base and exponent and returns the power. The body is the simplified version of the algorithm already developed for exponentiation with an integer exponent, here limited to the positive exponent.

**Calculation Steps:**
- Definition of the function with an appropriate signature (return type and parameters)
- Implementation of the iterative algorithm or another method for the positive power
- Replacement in `main` of the duplicated fragments with calls to the function

---

## Case Study: Computational Check of Fermat's Last Theorem

A program that reads positive integers x, y, z and an integer n with n > 2 (in the check: n not less than three), computes x^n, y^n, z^n separately and checks whether x^n + y^n = z^n. If the equality occurred, an anomaly is reported; otherwise consistency with Fermat's theorem is confirmed.

**Key Points:**
- Input checks: x > 0, y > 0, z > 0, n >= 3
- Computation of the three powers in dedicated variables
- Comparison of the sum with z^n
- Expectation: no equality for n > 2
- Use of `return` to terminate `main` in case of non-conforming input

**Explanation:**
x, y, z, n are acquired and validated. For each of x, y, z, the powers to the exponent n are evaluated, using the `raiseToPower` function or a reused fragment. x^n + y^n is compared with z^n. If equal, the user is informed that there is probably an error in the code; otherwise a confirmation message in line with the theorem is printed.

**Example:**
If one of x, y, z is less than or equal to zero, or if n is less than three, a message is printed or the program terminates immediately with `return` to interrupt the execution of the `main` function.

**Calculation Steps:**
- Immediate validation after the read
- If it fails, execution of `return`; this differs from `break`, which would only interrupt a loop, not the whole function

---

## Declaration and Definition of Variables and Functions Must Precede Use

In C++ the semantics of the language require that both variables and functions be declared and/or defined textually before their use. This guarantees that, at the time of use, the compiler and the runtime know the meaning associated with the identifiers.

**Key Points:**
- A variable must be declared before its use in the program
- A function must have its meaning defined (implementation and/or prototype) before its call
- The `main` function, although it is the first to be executed, may require that the functions called by `main` be defined before `main`
- The function name (for example `raise_power`) represents a subprogram, not a variable

**Explanation:**
The lesson stresses that, like variables, functions also need a textual definition prior to their use. In the case of the function `raise_power` called by `main`, its description must precede that of `main` in order to be resolved correctly at compilation and execution time.

**Example:**
In the program, `main` calls `raise_power` to compute the power. For this to be possible, the meaning of `raise_power` must be defined before `main`. The structure of the program shows `raise_power` with its local variable `products_left`, and the presence of global variables `base`, `exponent`, `power` to communicate with `main`.

**Calculation Steps:**
- `raise_power` is defined before `main`
- `products_left` is declared/defined as a local variable of the function
- Global variables `base`, `exponent`, `power` visible to both functions are prepared
- `main` uses `raise_power`, which operates through the global and local environments

**Considerations:**
- Ensure the correct textual order of definitions and declarations
- Verify the visibility of the identifiers in the functions that use them

---

## Global Environment and Local Environment in the Environment Model

The environment model represents, for each statement being executed, the set of elements on which that statement can operate. The global environment contains objects available to the whole program; each function has a local environment that contains the variables internal to the function.

**Key Points:**
- **Global environment:** includes elements defined at program level (e.g. `cin` and `cout` thanks to `iostream.h`)
- **Local environment of a function:** contains the local variables defined inside it
- **Graphical representation:** rectangles as containers of variable objects
- `main` can operate on the global environment because it is graphically contained inside it
- Functions can operate on their own local environment and on the global environment, not on the local environments of other functions

**Explanation:**
Before the execution of `main`, the global environment is created with the objects defined at program level (`cin` and `cout`). On entering `main`, the local environment of `main` is created. Variable declarations during `main` cause memory allocations (boxes) in the local environment of `main`. During the statements, the pertinent rectangles (local or global) are operated on.

**Example:**
The presence of `include iostream.h` before the definition of `main` makes `cin` and `cout` available to all the functions of the program. `main` can read and write from/to `cin` and `cout` without declaring them locally.

**Calculation Steps:**
- `include iostream.h` is inserted at the top
- `cin` and `cout` become global-level objects
- `main` uses `cout` to print and `cin` to read without further definitions

**Considerations:**
- Do not confuse the global environment with static or global variables defined elsewhere
- Local variables must not be used outside the function

**Special Circumstances:**
- If there are several functions with the same names for local variables, how should it be handled? Keep the scopes separate and do not access between different local environments

---

## Semantics of the Function Call and Return Information

When `main` calls a function (`raise_power`), a copy of the local environment of the called function is created and the information needed for the return is recorded: the next statement to execute in the caller and the environment to return to.

**Key Points:**
- Creation of the local environment of the called function at the time of the call
- Storage of the resume statement in the caller (e.g. `X_to_n = power`)
- Storage of the return environment (the environment of `main`)
- Execution of the function's statements in its local environment with access to the global environment
- Termination of the function restores control to the caller

**Explanation:**
When `main` calls `raise_power`, the system prepares the local environment of the called function and notes where to return and which statement to execute on resuming (`X_to_n = power` in `main`). This is represented by an arrow in the graphical model. After the execution of the `for` loop in `raise_power`, the function terminates and control returns to `main` to execute the statement following the call.

**Example:**
The statement to execute after the call is `X_to_n = power`. The return environment is that of `main`. This makes it possible to use the result computed by the called function.

**Calculation Steps:**
- During the call the resume statement is noted
- `raise_power` is executed
- At the end it returns to `main` and `X_to_n = power` is executed

**Considerations:**
- Ensure that the information needed for the return is correctly maintained (call stack)
- Ensure that the variables used after the call are visible in the caller

**Special Circumstances:**
- If there are multiple nested calls, how should it be handled? Correctly maintain the activation stack with return information for each call

---

## Communication Between Functions Through Global Variables

To allow several functions to operate on common data, some variables can be defined at global level. In the example, `base`, `exponent`, `power` are global to let `main` and `raise_power` communicate.

**Key Points:**
- Global variables visible to all the functions of the program
- `base`, `exponent`, `power` used as a communication channel between `main` and `raise_power`
- Local variables remain confined to their functions (`products_left` in `raise_power`; X, Y, Z, n, X_to_n, Y_n, Z_n in `main`)
- Globals let the called function compute and the caller read the result

**Explanation:**
Since `base`, `exponent` and `power` are used both in `main` and in `raise_power`, they are moved to global level. `main` sets the values of `base` and `exponent` and the function `raise_power` updates `power`. On return, `main` reads `power` to continue the processing.

**Example:**
`main` copies the values X and n into `base` and `exponent`. `raise_power` initializes `power` to 1, then computes the result through a `for` loop. At the end, `main` uses `power` to set `X_to_n`.

**Calculation Steps:**
- `main` sets `base = X` and `exponent = n`
- `raise_power` initializes `power = 1`
- It runs the `for` loop and updates `power = power * base`
- It returns to `main`, which executes `X_to_n = power`

**Considerations:**
- Limit the use of globals to the minimum necessary to avoid strong coupling
- Clearly document the use of globals as a communication channel

**Special Circumstances:**
- If there are name conflicts or side effects on the globals, how should it be handled? Use naming discipline and isolate writes in a dedicated function

---

## Reading Data and Transformation Through `cin`

The read statement from `cin` extracts characters, transforms them into the corresponding types (integers in this case) and assigns the values to the destination variables.

**Key Points:**
- `cin` contains characters that are extracted and converted
- The user must enter values for X, Y, Z, n separated by at least one space
- At the end of the read, X, Y, Z, n receive the corresponding values

**Explanation:**
After the `cout` statements that guide the user, `cin` is executed for X, Y, Z, n. The characters entered are extracted and converted into the corresponding integers; the variables receive the values and the program can proceed with the computation.

**Example:**
The program instructs the user to enter the values for X, Y, Z, n, separating them with at least one space. `cin` reads and converts the characters into integers.

**Calculation Steps:**
- `cout` shows the prompt
- The user enters X Y Z n
- `cin` extracts, converts and assigns to the variables

**Considerations:**
- Verify that the data are reasonable before proceeding with the calculations
- Handle input errors or invalid formats

**Special Circumstances:**
- If there are non-numeric characters in unexpected positions in the input, how should it be handled? Perform validation and repeat the input request

---

## Computing the Power with a `for` Loop and the Counter `products_left`

The computation of X^n is done by a `for` loop that iteratively updates the variable `power` by multiplying by `base` and decrementing a counter (`products_left`) as long as the condition for staying is satisfied.

**Key Points:**
- Initialization: `power = 1`
- Initial assignment: `products_left = exponent`
- Test for staying: `products_left > 0`
- Body of the loop: `power = power * base`
- Update of the counter: decrement of `products_left` (from 3 to 2, then to 1, then to 0 in the example)
- Exit from the loop when `products_left == 0`

**Explanation:**
Inside `raise_power`, `power` is identified in the global environment because it is not local, and is initialized to 1. `products_left` (local) is set equal to the `exponent` (global). `products_left > 0` is checked, and the body is executed: `power = power * base`. After each iteration `products_left` is decremented: from 3 to 2, from 2 to 1, from 1 to 0. When it is no longer true that `products_left > 0`, the loop is exited and the function ends.

**Example:**
Illustrated example: exponent = 3, `products_left` initialized to 3. Iterations: 3 > 0, update `power`; decrement to 2. 2 > 0, update `power`; decrement to 1. 1 > 0, update `power`; decrement to 0. 0 > 0 is false, exit.

**Calculation Steps:**
- Set `power = 1`
- Set `products_left = 3`
- Iteration 1: condition true, update `power`, `products_left = 2`
- Iteration 2: condition true, update `power`, `products_left = 1`
- Iteration 3: condition true, update `power`, `products_left = 0`
- Condition false, exit from the loop

**Considerations:**
- Ensure correct access to `base` and `power` in the global environment during the updates
- Avoid unhandled overflow during the iterative multiplication

**Special Circumstances:**
- If there is a negative exponent, how should it be handled? Define the desired semantics (fractional powers or error handling) before the implementation

---

## Return to the Caller and Environment Management

When a function ends, the environment of the caller and the statement from which to resume must be known. The calls create a copy of the local environment of the called function, with return information: a pointer to the environment of the caller (`main`) and the next statement to execute. At the end, the activated local environment is deleted and the memory is returned to the system.

**Key Points:**
- Two pieces of return information: environment of the caller and restart statement
- Execution of the assignment in the caller (e.g. `X_to_n = power`) in the caller's environment
- Creation of a new copy of the local environment at each call; old copies are not reused
- Deallocation of the local environment at the end of the function; reuse of the memory for later calls
- Reason for non-reuse: recursive functions require several simultaneous copies of the local environments

**Explanation:**
During the call to `raise_power`, a new instance of the local environment of the function is created and the information to return to `main` is noted: which environment made the call and which statement to execute afterwards. This makes it possible to correctly resume the execution of `main` (for example by assigning the result to the local variable `X_to_n` or `Y_to_n`). The model imposes that every call have its own copy, guaranteeing isolation and correct behavior in the presence of recursion. At the end of the function, the local environment is destroyed and the memory freed.

**Example:**
`main` assigns the value of X to `base`, the value of n to `exponent`, calls `raise_power`, then assigns `X_to_n = power`. It then repeats the scheme with Y: assigns `base = Y`, `exponent = n`, calls `raise_power` again, then `Y_to_n = power`. Each call creates a second (new) copy of the local environment of `raise_power`, with a pointer to the environment of `main` and a reference to the next statement (`Y_to_n = power`).

**Calculation Steps:**
- Preparation of the data in `base` and `exponent`
- Call to `raise_power` and interruption of `main`
- Execution of the function on `base` and `exponent`, with the result in `power`
- Return to `main` and assignment of the result to the appropriate local variable
- Repetition of the cycle with Y, creating a new copy of the local environment

**Considerations:**
- Always note the next statement in the return information
- Ensure the correct correspondence between the environment of the caller and that of the callee
- Avoid reusing old local environments so as not to introduce errors, especially in recursive contexts
- Correctly handle the deallocation of the memory of the local environment at the end of the function

**Special Circumstances:**
- If recursive calls are expected, how should memory be handled? Create and maintain independent copies of local environments, ensuring correct deallocation on return

---

## Interface Through Global Variables

Before the introduction of parameters, communication between `main` and `raise_power` takes place through global variables that act as the interface: `base` and `exponent` to provide the input data, `power` to return the result.

**Key Points:**
- Global variables used: `base`, `exponent`, `power`
- `main` transfers data into `base` and `exponent`, calls `raise_power`, the function computes and writes into `power`
- At the end, `main` reads `power` and transfers it into `X_to_n`, `Y_to_n`, `Z_to_n`, depending on the call
- Applicable to any triplet of variables of the caller
- Constraint: all the variables corresponding to `base`, `exponent` and `power` must be of integer type

**Explanation:**
The flow is: `main` prepares the inputs in the globals `base` and `exponent`; `raise_power` computes `base^exponent` and writes the result into the global `power`; `main`, on return, copies `power` into the corresponding local variable (for example `Y_to_n`). This mechanism is simple but ties the code to the presence of globals and their type.

**Example:**
For three calls, `main` uses (X, n) → `X_to_n`, then (Y, n) → `Y_to_n`, finally (Z, n) → `Z_to_n`. Each time it sets `base` = the base variable (X/Y/Z), `exponent = n`, calls `raise_power` and on return copies `power` into the respective local variable.

**Considerations:**
- Ensure that `base`, `exponent` and `power` are of integer type
- Avoid state conflicts due to the use of shared global variables
- Correctly coordinate the order of assignments and calls so as not to overwrite `power` before it is read in `main`

**Special Circumstances:**
- If several functions use the same globals, how should interference be avoided? Serialize the calls and isolate access to the globals, or migrate to parameter passing

---

## Parameter Passing: Formal and Actual Parameters

Parameter passing allows direct communication between functions without globals: the function is defined with formal parameters (placeholders), which at the call are replaced with actual parameters. Input parameters and output parameters are distinguished, with attention to types and correspondence.

**Key Points:**
- Interface in the definition of the function: list of input and output parameters
- Formal parameters as placeholders: `base`, `exponent` (input), `power` (output)
- Actual parameters associated in the call: example `base ← y`, `exponent ← n`; `power → Y_to_n`
- Type correspondence: actual parameters must be of the same type as, or compatible with, the formal ones
- The parameters are part of the local environment of the called function
- Distinction between input/output indicated by the suffixes mentioned; each parameter has an explicit type
- The call includes the semantics of copy to the function and return of the result, eliminating the need to manipulate globals

**Explanation:**
By defining `raise_power` with formal parameters (`base`, `exponent` as input; `power` as output), `main` calls the function passing the corresponding actual parameters (for example `y` and `n`). On output, the result computed in `power` is transferred to the actual parameter `Y_to_n`. The call creates the local environment of the function with the return information (pointer to `main` and next statement). Before the execution of the body, the binding between formal and actual parameters is done, guaranteeing type compatibility.

**Example:**
The previous sequence: copy y and n into the globals `base` and `exponent`, call `raise_power`, copy the result of the global `power` into `Y_to_n`, becomes a single call: `raise_power(base = y, exponent = n, power → Y_to_n)`.

**Calculation Steps:**
- Definition of the function with formal parameters `base`, `exponent`, `power`
- Call with actual parameters `y`, `n` and `Y_to_n`
- Binding of the parameters before the execution of the function
- Computation of `base^exponent` and transfer of the result into the output parameter

**Considerations:**
- Clearly define the types of all the parameters in the function
- Ensure a one-to-one correspondence between formal and actual parameters at the call
- Manage input and output parameters distinctly to avoid ambiguity
- Perform parameter passing before the execution of the body of the function

**Special Circumstances:**
- If the types are not compatible, how should it proceed? Perform explicit conversions or adapt the definition of the parameters to ensure compatibility

---

## Environment Model of the Program

The environment model distinguishes a global environment and local environments for `main` and the called functions. With parameter passing, the global environment can contain only common libraries (e.g. iostream), while the interface data are local to the function.

**Key Points:**
- Global environment allocated before execution: in this case it contains the objects of the iostream library
- Local environment of `main`: declaration of x, y, z, n, x_to_n, y_to_n, z_to_n
- Creation of the rectangle (copy) of the local environment of `raise_power` at each call
- Return information included in the copy: pointer to the environment of `main` and next statement
- Parameter passing carried out before the execution of the body of the function

**Explanation:**
It starts by allocating the global environment (I/O library). `main` creates its own local environment with the variables mentioned and, at the time of the calls, copies of the local environment of the function `raise_power` are created. Each copy contains the information needed to return correctly to `main`. Before executing the statements of the function, the formal parameters are instantiated with the actual ones.

**Example:**
During a call, the stored restart statement is not a comment, but the next significant statement, which may be another call to `raise_power`.

**Calculation Steps:**
- The definition of the return information includes the next statement
- Comments are not considered statements by the computer
- The restart can be directly a second call to the same function

**Considerations:**
- Clarify which objects reside in the global environment when local parameters are used
- Verify the restart sequence to avoid flow-control errors
- Always create the copy of the local environment before instantiating the parameters

---

## Parameter Passing by Value

Mode in which the value of the actual parameter at the time of the call is copied into the formal parameter of the called function. It is a one-way transmission: the called function receives a copy and cannot modify the caller's environment through that parameter.

**Key Points:**
- The current value of the actual parameter in the caller is copied into the formal parameter
- Applies to input parameters such as `base` and `exponent`
- Example: NN is 3, so 3 becomes the initial value of the exponent
- It does not allow changes to be reflected in the caller's environment

**Explanation:**
When the function is called, boxes are created in the environment of `main` for the input formal parameters. For `base` and `exponent`, the corresponding actual parameter is evaluated and the value is copied into the formal parameter. This mechanism is called passing by value because it transfers only the value, not the location, and any modification remains confined to the called function.

**Example:**
In the case of the second parameter `exponent`, the actual parameter NN, which is 3, is evaluated. The value 3 is copied as the initial value of the formal parameter `exponent` before the execution of the function.

**Calculation Steps:**
- NN is located in the caller
- Its value is read: 3
- 3 is copied into the formal parameter `exponent`

**Considerations:**
- Always verify the current value of the actual parameter at the time of the call

---

## Parameter Passing by Address (for Output)

Mode in which the called function is given not the value but the position (address) of the actual parameter. By operating on the formal parameter, one operates directly on the corresponding actual parameter, allowing the modification of the caller's environment during execution.

**Key Points:**
- The address/position of the actual parameter is passed
- Every operation on the formal parameter acts on the actual parameter
- Allows transmission of information from the called function to the calling function
- The association between formal and actual parameter happens only once at the time of the call
- Allows incremental changes during execution, not only at the end

**Explanation:**
For the parameter `power`, in addition to the type, the direction is specified: it is an output parameter. Instead of computing an internal value and transferring it at the end (pass by result), the language adopts passing by address. At the time of the call to `raise_power`, together with the passing by value of the other parameters, the address of the actual parameter corresponding to `power` is passed. Thus, the assignment of 1 to `power` directly modifies the actual parameter in the caller.

**Example:**
The first statement in the function assigns the value 1 to the formal parameter `power`. Since `power` is passed by address, the value 1 is written directly into the corresponding actual parameter in the caller.

**Calculation Steps:**
- At the time of the call, the address of the actual parameter of `power` is passed
- The assignment `power = 1` in the function writes into the caller
- The effect is immediately visible in the environment of `main`

**Considerations:**
- Correctly pass the address of the actual parameter for output parameters
- Do the association between formal and actual only once at the time of the call

**Special Circumstances:**
- If the actual parameter is not allocated or is not addressable, how should it be handled? Verify the existence and validity of the address before passing

---

## Comparison Between Passing by Value and Passing by Result

Passing by value transfers only the initial value and does not allow changes in the caller. Passing by result consists in transferring the value of the formal parameter at the end of the execution to the position of the corresponding actual one; however, languages prefer passing by address, which allows continuous updates to the actual parameter during execution.

**Key Points:**
- **By value:** one-way transfer, no change in the caller
- **By result:** transfer of the final value at the end
- **By address:** transfer of the address and continuous updates

**Explanation:**
The lesson considers the idea of "passing by result" as the inverse process of passing by value for output parameters. In practice, instead of waiting for the end, passing by address allows every modification of the formal parameter to be reflected immediately on the actual parameter.

**Considerations:**
- Choose the passing mechanism according to the need to modify the caller's environment

---

## Execution Environment and Phases of the Function Call

Before the execution of the called function, all the preparations are done in `main`: creation of the boxes for the formal parameters, initializations by value and associations by address. Only after parameter passing are the statements of the called function executed.

**Key Points:**
- Preparation operations in `main`
- Simultaneous passing of parameters by value and by address
- Creation of local variables in the called function (e.g. `products_left`)

**Explanation:**
The setup phase takes place entirely in the environment of `main`: boxes are created for the formal parameters, the input parameters are initialized by value and the address is associated for the output parameters. Once the passing is finished, the statements of the function `raise_power` are executed, including the declaration of local variables.

**Example:**
At the start of the execution of the called function, the local variable `products_left` is declared and its box is created. Subsequently, in the `for` loop, `products_left` is assigned the value of `exponent`, which is 3.

**Calculation Steps:**
- Declaration of `products_left` in the function
- Assignment: `products_left = exponent` with exponent = 3
- Check of the condition: `products_left > 0?`

**Considerations:**
- Clearly distinguish between the environment of `main` and the environment of the called function

---

## Parameter Passing (by Value and by Address) in the Function Example

In C++ parameters can be passed by value (the value is copied into the formal parameter) or by address/reference (one operates directly on the actual parameter). In the case described, `power` is passed by address, while `base` and `exponent` are passed by value.

**Key Points:**
- **By value:** `base` receives the current value of X, `exponent` receives the value of n
- **By address:** `power` refers directly to the actual variable (e.g. x_to_n or y_to_n)
- **Side effect:** operating on `power` directly modifies the corresponding actual parameter
- Clear distinction between input parameters (X, n; Y, n) and output parameters (x_to_n, y_to_n)

**Explanation:**
The function `raise_power`, in the first version, uses `power` as an output parameter passed by address. During the loop, the computed value is assigned to `power`, which is bound directly to the actual variable (x_to_n, y_to_n). Passing `base` and `exponent` by value ensures that internal changes do not affect the caller's variables.

**Example:**
Call: `raise_power(base = X, exponent = n, power = &(x_to_n))`. The loop repeatedly multiplies `power` by `base` (base equal to three is mentioned as an example) until `products_left` is decremented, directly updating `x_to_n`.

**Calculation Steps:**
- Setting: `power = 1`
- `for` loop: successive multiplications by `base`
- Decrement of the counter (`products_left`)
- End of the loop: `x_to_n` updated with the final value of `power`

**Considerations:**
- Always clarify which parameters are input and which are output
- Avoid ambiguity in names (e.g. `power`, `x_to_n`) for readability
- Pay attention to the side effects of passing by address

**Special Circumstances:**
- If the actual parameter must not be modified, how should it be passed? Pass it by value or as a `const` reference

---

## Execution Environment: Caller and Function

Each function call creates a local environment with variables and return metadata. At the end of the function the local environment is deleted and execution resumes at the return point of the caller.

**Key Points:**
- Creation of a copy of the local environment at each call of `raise_power`
- Return information: who the caller is (`main`) and which statement to return to (e.g. alpha, beta)
- After the conclusion, the local environment is deleted and execution resumes in the caller
- At the end of `main`, the local environment of `main` is also deleted, ending the program

**Explanation:**
When `raise_power` is called several times, each call has a distinct local environment. The return point differs depending on the position of the call in the expression. The labeling (alpha, beta) serves to illustrate where to resume execution.

**Example:**
After the first call with X and n, the second calls `raise_power(Y, n)` with `power` bound to `y_to_n`, with a new return point (beta).

**Calculation Steps:**
- Creation of a new local environment
- Parameter passing: `base = Y`, `exponent = n`
- Execution of the loop, computation of `power`
- Return to point beta

**Considerations:**
- Highlight the difference between return points when the call occurs in different contexts
- Ensure that each call destroys its own environment to avoid confusion or conceptual memory leaks

**Special Circumstances:**
- If a function is called inside an expression with several functions, how is the order handled? Define return points and the handling of temporary spaces for intermediate evaluations

---

## Return Value and the `return` Keyword

A function can return a value associated with its name. The return type prefixes the function (e.g. `int` instead of `void`). The `return` statement expresses the value to be returned to the caller and interrupts the execution of the function.

**Key Points:**
- Change of signature: from `void` to `int` for `raise_power`
- Removal of the output parameter `power` when the return value is used
- Use of `return power` to return the result (e.g. 27)
- The caller can directly use the result in the evaluation of expressions

**Explanation:**
To avoid introducing intermediate variables (e.g. K) and splitting expressions, a version with a return value is preferred. The statement `return power` transfers the value to the context of the caller, which can assign it or use it in a complex expression.

**Example 1:**
`x_to_n = raise_power(x, n);` without using an output actual parameter.

**Calculation Steps:**
- Internal computation of `power`
- `return power`
- Assignment of the return value to `x_to_n`

**Example 2:**
`if (raise_power(x, n) + raise_power(y, n) == raise_power(z, n)) { ... }`

**Calculation Steps:**
- Evaluation of the first call and temporary storage (ESP)
- Evaluation of the second call and sum with the first result
- Evaluation of the third call
- Comparison (`==`) and branching of the `if`

**Considerations:**
- Choose the return type consistent with the expected result (here `int`)
- When using `return` with an expression, make sure the variable is correctly computed before the `return`

**Special Circumstances:**
- If the function must signal errors, how should it return them? Error codes or exceptions could be used; not described here but to be planned

---

## Evaluation of Expressions and Temporary Memory (ESP)

The evaluation of expressions with multiple function calls requires temporary memory cells to store partial results. The model uses an ESP box to represent these spaces globally.

**Key Points:**
- The C++ code is translated into machine language before execution
- The calls to `raise_power` appear three times and the intermediate values are kept temporarily
- ESP represents the space for partial and final values during the evaluation
- The order of evaluation is illustrated with return points (alpha, beta)

**Explanation:**
During the `if`, the following is executed: 1) call to `raise_power(x, n)`, a value is obtained (e.g. 27) and saved in ESP; 2) call to `raise_power(y, n)`, a second value is obtained, and it is added; 3) call to `raise_power(z, n)`, the result of the sum is compared with this last value. Each call creates and destroys its own environment.

**Example:**
After the first call, `return power` transfers 27 into ESP; the local environment is destroyed and execution resumes at point alpha.

**Calculation Steps:**
- Creation of the environment
- Computation of `power = 27`
- `return power`
- Destruction of the environment and resumption at point alpha

**Considerations:**
- Do not go into excessive detail of machine language when not necessary, but understand the use of temporary spaces
- Clarify the return points to follow the evaluation flow

**Special Circumstances:**
- If the order of evaluation of the operands is not defined, how should it be handled? Rely on the rules of the language and do not assume an unspecified order

---

## Direct Communication Between Functions Without a Global Environment

Functions can communicate directly through parameter passing, avoiding the use of the global environment. This makes functions autonomous and reusable with different inputs/outputs without changing their description.

**Key Points:**
- Preference for parameter passing over the use of global variables
- Better modularity and code reusability
- Fewer side effects and a clearer data flow

**Explanation:**
In the rest of the course this mode will be used almost exclusively: functions defined autonomously that receive input and provide output by value or by return, without depending on global state.

**Considerations:**
- Limit global variables to avoid implicit dependencies

---

## Introduction to Recursion

Recursion is an approach in which a function is defined in terms of itself, making it possible in certain situations to translate the specification of the problem directly into code, without explicitly choosing an imperative solution strategy.

**Key Points:**
- Powerful conceptual tool in modern languages like C++
- Intensive use is expected in the final part of the course
- Allows elegant descriptions that adhere to the specification of the problem

**Considerations:**
- Understand well the base cases and progress towards them when recursion is adopted

**Special Circumstances:**
- If recursion may cause a stack overflow, how should it proceed? Introduce clear base cases and consider iterative versions or tail recursion if possible

---

## Recursion: Concept and Structure

Recursion is a technique in which a definition or a function uses itself to solve a problem on a smaller data domain. It requires at least one non-recursive base case that guarantees termination and a reduction rule that brings the data closer to the base case.

**Key Points:**
- Definition that uses itself
- Non-recursive base case (termination)
- Recursive step with reduction of the problem
- Decrease of the size of the domain (typically by 1)
- Equivalence with iterative solutions in many cases

**Explanation:**
In the context of the power and the factorial, the recursive function calls itself with parameters that decrease (`exponent-1`, `n-1`) until a base case is reached in which the result is known without further calls. This makes it possible to express the mathematical definition directly as code, delegating to the runtime the management of the chain of calls.

**Example:**
Definition: if `exponent = 1`, then `base^exponent = base`. If `exponent > 1`, then `base^exponent = base * base^(exponent-1)`. The repeated expansion produces `base * base^(exponent-1) = base * base * base^(exponent-2) = ...` until `exponent = 1` is reached.

**Calculation Steps:**
- Identify the base case: `exponent = 1` returns `base`
- Define the recursive step: return `base * raise_power(base, exponent-1)`
- Ensure that `exponent` is positive so that the reduction leads to the base case
- Observe that the size of the problem decreases by 1 at each call

**Considerations:**
- Always define a clear base case to avoid infinite recursion
- Make sure the parameters get closer to the base case at each call
- Handle only positive exponents in the proposed definition
- Assess the stack depth for large inputs in languages like C++
- Keep the interface (`main`) unchanged when replacing the iterative solution with the recursive one

---

## Recursive vs. Iterative Power (Exponentiation)

Computation of `base^exponent` using two approaches: iterative (repeated multiplications starting from 1, the neutral element of the product) and recursive (application of the definition `base^n = base * base^(n-1)` with base case `exponent = 1`).

**Key Points:**
- **Iterative:** initialization to 1 and a `for` loop for n multiplications of the base
- **Recursive:** base case `exponent = 1`, recursive step with `exponent-1`
- Logical equivalence of the two formulations
- Constraint: positive exponent in the model presented
- `main` can remain identical; the implementation of the function changes

**Explanation:**
It starts from the mathematical definition: for `exponent = 1`, the result is `base`; for `exponent > 1`, `base` multiplied by the result of the same function with `exponent-1` is returned. Expanding repeatedly, a chain is obtained that ends when `exponent` reaches 1. The iterative version translates the same logic into a `for` loop starting from 1.

**Example:**
Logical scheme: `if (exponent == 1) return base; else return base * raise_power(base, exponent-1);` `main` does not change; only the function that solves the sub-problem of the power changes.

**Calculation Steps:**
- Define formal parameters: `base`, `exponent`
- Base case: `exponent == 1` → `return base`
- Recursive step: `return base * raise_power(base, exponent-1)`
- Prerequisite: `exponent > 1` to enter the recursive branch

**Considerations:**
- Correctly initialize to 1 in the iterative case (neutral element)
- Check that `exponent` is not 0 in the given specification; otherwise extend the base cases
- Beware of duplicated code/typos in the text; keep the logic consistent

---

## Factorial as an Example of a Recursive Definition

The factorial of a positive integer n is defined recursively: if n = 0 or 1, n! = 1; if n > 1, n! = n * (n-1)!. The sequence of calls decreases n by 1 until the base case.

**Key Points:**
- **Base cases:** n = 0 or 1 → n! = 1
- **Recursive step:** n! = n * (n-1)! for n > 1
- Equivalent product: n * (n-1) * (n-2) * ... * 2 * 1
- Termination guaranteed by the reduction of n
- Classic example to introduce recursion

**Explanation:**
Applying the definition, each recursive call reduces n by 1. When n reaches 1, the function returns 1 without further calls, ending the chain. The corresponding iterative form is the product from 1 to n.

**Example:**
For n > 1: n! = n * (n-1)! = n * (n-1) * (n-2)! = ... down to 1! = 1. If n = 0, 0! = 1 by definition.

**Calculation Steps:**
- Establish the base cases: n = 0 or 1
- Apply the reduction n → n−1
- Verify termination
- Compare with the iterative version as a correctness check

**Considerations:**
- Verify input n >= 0 to respect the base cases n = 0 or 1
- Avoid overflow for large n in practical implementations

---

## Execution Semantics of Recursive Calls (Environment Model)

The execution of a recursive function involves the creation of a chain of calls, each with its own execution environment/context, up to the base case; then it returns going back up the chain, combining the results.

**Key Points:**
- Each call has its own parameters and local variables
- The chain grows until the base case is reached
- The return of the values happens in reverse (unwinding of the stack)
- In C++ the implementation exploits the call stack
- `main` remains unchanged; the implementation of the function is replaced

**Explanation:**
For `raise_power(base, exponent)`, the successive calls `raise_power(base, exponent-1)`, `raise_power(base, exponent-2)`, ... are allocated on the stack with their respective parameter values. When `exponent = 1` is reached, `base` is returned, and each previous activation multiplies by `base`, up to the initial call.

**Example:**
The initial call with `exponent = n` (> 1) generates a call with n−1, then n−2, ... down to 1. The base case returns `base`; each previous activation computes `base * partial_result`.

**Calculation Steps:**
- Creation of an activation frame for each call
- Evaluation of the base case and return
- Unwinding with successive multiplications
- Comparison with the iterative approach that uses a single frame and a loop

**Considerations:**
- Avoid excessive recursion depth, which can cause a stack overflow
- Make sure every execution path reaches a base case

---

## Environment Semantics in C++: Global, `main` and Function Locals

In the execution model described, every function called in C++ activates a new copy of the local environment. The local environments are created in the global environment and keep formal parameters and local variables distinct for each activation. In recursive calls several copies can coexist simultaneously, but execution operates on the most recent copy (top of the stack). The resume points (Alpha, Delta) indicate where control returns in the caller.

**Key Points:**
- The global environment contains the definitions and creates the functions at the time of the call
- The environment of `main` governs the overall flow and receives the returns from the functions
- Every function call dynamically creates a new copy of the local environment
- In recursive calls several copies coexist; only the last one is operated on
- Labeled return points (Alpha, Delta) to restore execution in the caller
- The ESP box represents the space for evaluating expressions (partial and final values)

**Explanation:**
At startup from `main`, an `if` condition governs the execution. At the call to `raise_power`, a copy of the local environment is created with formal parameters `base` and `exponent`, initialized with the actual values passed. Any `return` expression requires evaluation inside an ESP box. In a recursive call, new copies are created in parallel in the global environment and each has the same names, but they belong to different environments, so they do not interfere. When an inner call ends, control returns to point Delta of the previous call, making it possible to complete the suspended expression and propagate the result towards the caller. At the end, `main` resumes from point Alpha with the returned result and continues the overall evaluation.

**Example:**
`main` invokes `raise_power` with `base = 3` and `exponent = 3`. First activation: `exponent = 3`, condition `exponent == 1`? no; `exponent > 1`? yes, executes `return` with the expression `base * raise_power(base, exponent-1)`. A second copy is created: `base = 3`, `exponent = 2`. Again `exponent == 1`? no; `exponent > 1`? yes, `return base * raise_power(base, exponent-1)`. A third copy is created: `base = 3`, `exponent = 1`. Base case: `exponent == 1`? yes; `return` the value of `base`. The third call returns 3 to the second: ESP becomes 3 × 3 = 9, the second returns 9 to the first: ESP becomes 3 × 9 = 27. The first returns 27 to `main` at point Alpha.

**Calculation Steps:**
- First call: parameters `base = 3`, `exponent = 3`; evaluation of the expression in ESP
- Second call: parameters `base = 3`, `exponent = 2`; new ESP; another recursive call
- Third call: parameters `base = 3`, `exponent = 1`; base case, `return base = 3`
- Unwinding: third → second (3); the second computes 3 × 3 = 9; second → first (9); the first computes 3 × 9 = 27
- `main` resumes from point Alpha with the value 27

**Considerations:**
- Make the different copies of the local environments visible in the demonstrations by changing stroke/name (stroke one, stroke two, stroke three) for readability
- Ensure that each activation records the correct return point (Alpha, Delta) to resume execution
- Use an ESP box to keep track of the partial values in the `return` expressions
- Always operate on the most recent copy in the presence of recursion; the previous ones remain suspended
- Understand the memory/time cost when the local environment is rich and the activations are numerous

**Special Circumstances:**
- If the exponent is large (e.g. 27), how should memory and time usage be handled? Use iterative implementations or optimizations (e.g. exponentiation by squaring) to reduce recursive activations
- If state must be kept between calls, how should it be handled? Use `static` or external structures, aware of the semantic change (persistence of values) and of the risks of interference between calls

---

## Dynamic vs. Static Allocation of Local Environments

Dynamic allocation in C++ creates and destroys the local environment at every function call, guaranteeing independence from the history of previous calls. Static allocation would preserve the values of the local objects between calls, altering the semantics and making it impossible to correctly handle recursion when several copies must coexist.

**Key Points:**
- **Dynamic:** a new copy for each call; destruction at the end; independence from the past
- **Static:** a single copy per function; persistence of the values of the last call; interference between calls
- Recursion requires dynamic allocation to support the coexistence of several copies
- The number of copies depends on the input data (exponent)

**Explanation:**
In languages that allow recursive functions, dynamic activation is necessary. With static allocation, the local values would persist and be reused, preventing the correct evaluation of nested calls, because there would be a single instance that would be overwritten. Dynamic allocation makes it possible to have as many copies as the problem requires (exponent 3 → 3 copies; exponent 27 → 27 copies), which cannot be known in advance by static analysis of the program.

**Example:**
For `exponent = 3`, 3 copies of the local environment are activated; for `exponent = 27`, 27 copies are activated. The system cannot determine statically how many copies will be needed before execution.

**Calculation Steps:**
- The structure of the stack grows with the calls until the base case
- Each return frees the copy and returns the result to the previous one

**Considerations:**
- Verify that the platform handles the stack correctly for many activations
- Avoid expensive local allocations in repeated recursive functions
- Clearly document the base cases to limit the recursion depth

**Special Circumstances:**
- If the stack is insufficient for deep recursion, how should it be handled? Apply iterative transformations or tail recursion techniques (when applicable), or increase the stack limits with caution

---

## Evaluating Expressions and Managing the ESP Box

Every `return` with an expression requires progressive evaluation in an area (ESP) that accumulates partial values and produces the final value to return. When the evaluation includes a function call, execution is suspended, the function is called and the result is reinserted into ESP to complete the expression.

**Key Points:**
- ESP contains partial and final values of the expressions
- The function call suspends the evaluation and stores the resume point (Delta)
- The result of the called function is inserted into ESP to complete the computation
- The chain of recursive returns completes the expressions in reverse

**Explanation:**
In the example, the first ESP prepares `base = 3` for `raise_power(...)`. The third call returns 3, the second ESP becomes 3 × 3 = 9, the first ESP becomes 3 × 9 = 27. `main` resumes from point Alpha with 27 and continues with a further sum and comparison.

**Example:**
After the return of 27 to `main`, the expression continues with a `+` operator. `raise_power` is called with y and n. With n = 3, in the end 4 × 4 × 4 is obtained, which is added to 27. The evaluation then continues from point Beta with a comparison operator on z raised to n (n = 3).

**Calculation Steps:**
- The ESP in `main` goes from 0 to 27 + ...
- New recursive chain with `base = 4` and `exponent = 3`, result 64
- Sum: 27 + 64
- Evaluation of the next comparison with z^3

**Considerations:**
- Clearly annotate points Alpha and Beta in the overall evaluation of the expressions
- Avoid ambiguity in the handling of several simultaneous ESPs: one for each context

**Special Circumstances:**
- If the expression includes several operators with different precedence, how should it be handled? Establish the order of evaluation and correctly suspend/resume for each function call

---

## Efficiency and Design Choices Between Recursion and Iteration

Recursion can be less efficient in terms of memory and time, especially when the number of activations is high or the local environments are complex. However, in a teaching context, recursion is often preferred for its clarity and adherence to the specification. In real programs, for simple problems like the power and the factorial, the iterative solution is preferred.

**Key Points:**
- Example: computing 2 to the eighteenth power requires 18 activations of `raise_power`
- Repeated allocations of complex environments can be expensive
- Teaching goal: favor correct and clear solutions, often recursive ones
- In practice, choose iteration for simple cases; use recursion when the non-recursive version is conceptually difficult

**Explanation:**
In the first course of computer science fundamentals, the focus is on correctness and clarity: inserting the recursive definition into the program is almost the specification of the problem. However, for operations like exponentiation or the factorial, an iterative version is more efficient and common in real programs. When the transformation from the recursive specification to an iterative solution is complicated, recursion considerably simplifies development.

**Example:**
For 2^18, 18 copies of the local environment are activated, with higher allocation and memory costs compared with an iterative solution that uses a loop.

**Calculation Steps:**
- Recursion: depth 18, the stack grows and each call allocates local variables
- Iteration: a single environment, updates in a loop

**Considerations:**
- Assess the maximum expected depth and the allocation cost
- Prefer iteration when available and simple
- Use recursion for problems with a naturally recursive definition or hard to iterate

---

## Tasks and Suggestions

- Read the requirements of the problem very carefully before seeing the solution, to understand what the problem consists of
- Independently analyze the passage from pseudocode to C++ code
