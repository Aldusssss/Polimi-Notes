# Modules 20-23: Parameter Passing, Arrays and Table Management

## Topic Overview

C++, arrays and parameter passing. The modules cover the factorization of repetitive code into functions, the semantics of array parameters in C/C++, passing by value vs. by address, the `const` keyword, the decomposition of a problem into sub-problems and function prototypes, and an introduction to the management of tabular data.

---

## Key Points Summary

1. Factorization of repetitive code into functions
2. Identification of the parameters of a function based on the differences in the code
3. Semantics of passing array-type parameters in C/C++
4. The name of an array in C++ as a pointer to its first element
5. Passing the address of the array by value, which allows modifying the original array
6. Efficiency of passing arrays (saving of memory and time)
7. Declaration of array parameters in functions with empty square brackets `[]`
8. Flexibility of using a function with arrays of different sizes
9. Responsibility of the programmer to manage the sizes of the arrays
10. Need to pass the size of the array as a separate parameter to the function

**Key Quotes:**
> "The value of the name of an array in C is nothing more than the pointer to its first element."

> "It is very important that the sub-problems be solved using functions in such a way that in the expression of the solution of the problem, which is the whole program, the parts concerning different aspects, which are encapsulated in functions as we have seen, are clearly visible."

> "Two aspects: one is reusability, the other is limiting the user's ability to make mistakes."

---

## Passing Arrays as Parameters in C/C++

In C and C++, the name of an array represents the memory address of its first element. When an array is passed to a function as a parameter, what is really passed "by value" is the address of its first element. This means that the function receives a pointer to the first element of the original array, not a copy of the whole array.

**Key Points:**
- The value of the name of an array in C++ is the pointer to its first element
- Passing an array to a function involves copying the address of the first element into the formal parameter of the function
- The function operates directly on the original array in the caller's memory, not on a local copy
- This method is efficient in terms of memory and execution time, since it avoids copying the whole array
- In the declaration of the function, array-type parameters are indicated with empty square brackets (e.g. `int prices[]`), without specifying the size, to allow the function to operate on arrays of different sizes

**Explanation:**
When a function such as `show_deviations(prices, ...)` is called with an actual array `prices_c`, the value of `prices_c` (which is the address of its first element) is copied into the formal parameter `prices`. As a consequence, inside the function, `prices` points to the same memory area as `prices_c`. Any operation on `prices[i]` inside the function directly modifies the corresponding element in `prices_c`. This is the reason why it is not necessary to specify the size of the array in the signature of the function, offering the flexibility of using the same function with arrays of different sizes in different calls.

**Example:**
A program must analyze and print information (sum, number of elements, prices) for two zones of a city: "center" and "suburbs". The code to carry out these operations is identical for both zones, changing only the variables it operates on (`sum_ce` vs. `sum_p`, `prices_ce` vs. `prices_p`, etc.).

**Calculation Steps:**
- To avoid code duplication, the common operations are factored into a single procedure called `show_deviations`
- The variables that differ between the two zones (the name of the zone, the sum, the number of elements and the array of prices) are turned into input parameters of the function: `void show_deviations(char zone_name[], int sum, int num, int prices[])`
- The main program (`main`) calls this function twice, once for each zone, passing the specific data as actual parameters
- First call: `show_deviations("center", sum_ce, num_ce, prices_ce);`
- Second call: `show_deviations("suburbs", sum_p, num_p, prices_p);`
- In this way the analysis logic is written only once and reused, making the code cleaner and more maintainable

**Considerations:**
- It is essential, when functions operate on arrays passed as parameters, to also pass the information on how many significant elements the array has (its size), typically as another integer parameter
- Whoever writes the program must be careful not to go beyond the size of the arrays, using indices correctly and consistently with the defined size, to avoid memory access errors
- For strings (arrays of characters), the size is not passed explicitly, but the end of the string is indicated by a special character, the null terminator (`\0`)

**Special Circumstances:**
- If working with strings (arrays of characters), how is the end of the string determined without passing its length? The scanning of the array must end when the null terminator character (`'\0'`) is met
- If a string is built character by character and one forgets to insert the null terminator at the end, what happens? A print statement would keep reading and printing characters from consecutive memory until it randomly meets a byte with value zero, leading to undefined behavior

---

## Handling Strings as Arrays of Characters

In C++, strings are represented as arrays of characters. By convention, every string is terminated by a special character, the null character (represented as `\0`), which has ASCII numeric code zero. This allows functions to process the string without needing to know its length in advance.

**Key Points:**
- Constant strings such as "center" and "suburbs" are automatically terminated by the compiler with the null character `\0`
- Strings can be read and written as a whole (e.g. with `cin` and `cout`), unlike other types of arrays that require iterating element by element
- The statement `write zone_name` prints the characters of the array `zone_name` until it meets the null character
- The statement `cin >> string` reads characters from the input stream and inserts them in the array `string` until it meets a space or a newline, automatically adding the null character at the end

---

## Refactoring the Data Structure: From Single Variables to Arrays

The lesson illustrates how to modify a program to make it more scalable, moving from a system with distinct variables for each "zone" (e.g. `sum_CE`, `sum_p`) to an approach based on arrays. This avoids code duplication when the number of zones increases, for example from 2 to 20.

**Key Points:**
- The use of arrays makes the program easily expandable to a larger number of zones
- Handling the names of the zones requires a two-dimensional array of characters (array of strings), which by its nature must be "rectangular", imposing a fixed maximum length for all names (`MAX_NAME`)
- It is advisable to change the input of the zone from character to integer to align it with array indexing
- The initialization of arrays can be efficiently done with a loop
- Well-designed and decoupled functions (such as `show_deviation`) may not require changes even after a significant refactoring of the main data structure

**Explanation:**
The transformation process involves replacing individual variables with indexed array elements. For example, `sum_CE` and `sum_p` become `sum[0]` and `sum[1]`. This logic extends to all the zone-specific variables: prices, num, sum and zone_name. The input is also modified, using integer indices (0, 1, ...) to identify the zones, consistently with array access. The constants that define the zones are changed from characters to integers. The initialization of data is simplified through a loop that zeroes the elements of the arrays `num` and `sum`.

**Example:**
A program that initially used variables such as `price_c`, `price_p`, `num_c`, `num_p`, `sum_c`, `sum_p` is modified. Arrays are introduced: `prices[2][MAX_DIM]`, `num[2]`, `sum[2]` and `zone_name[2][MAX_NAME]`. The input for "center" becomes the integer 0 and for "suburbs" the integer 1.

**Calculation Steps:**
- Define the zone constants as integers: `const int center = 0;`, `const int suburbs = 1;`
- Declare the variables as arrays: `int prices[2][MAX_DIM];`, `int num[2];`, `float sum[2];`
- Introduce an array for the names: `char zone_name[2][MAX_NAME];`, with `MAX_NAME` defining the maximum length (e.g. 10)
- Replace the multiple initializations with a loop: `for (i=0; i<2; i++) { num[i] = 0; sum[i] = 0; }`

**Considerations:**
- When defining an array of strings (two-dimensional array of characters), a fixed maximum size (`MAX_NAME`) must be allocated for each string, which could cause a waste of memory if the names have very different lengths
- The order in which independent array elements are initialized is irrelevant for the result

---

## Using Arrays for Compactness and Extensibility of the Code

The transition from distinct variables for each "zone" (e.g. `sum_c`, `sum_p`) to an array-based system (e.g. `sum[zone]`, `prices[zone]`) makes the code more compact, efficient and easily extensible.

**Key Points:**
- A single block of statements can handle any number of zones by operating on `sum[zone]`, `prices[zone]` and `num[zone]`
- The exit condition of the data acquisition loop is generalized: the loop ends not only when there are no more readings, but also when there is no more space in the array for a specific zone (`num[zone] >= maximum_size`)
- This structure makes the program easily extensible to any number of zones, without having to rewrite the main logic

**Explanation:**
Instead of having separate blocks of code for each zone (center, suburbs, etc.), a single block of statements is used. The variable `zone` acts as an index to access the correct elements in the arrays `sum`, `prices` and `num`. This eliminates the need to duplicate the handling logic for each new zone added.

---

## Dynamic Management of Zones

The program is improved to allow the user to specify, at the start of execution, the number of zones to analyze and the name of each, within a predefined maximum limit.

**Key Points:**
- The use of a constant `MAX_ZONES` makes it easy to change the maximum capacity of the program
- A variable `num_zones` stores the actual number of zones chosen by the user for the current session
- The processing loops must iterate up to `num_zones`, not up to `MAX_ZONES`
- The user can assign specific names to the zones (e.g. "Porta Vigentina", "Duomo"), which will then be used in the output tables, improving the readability of the results

**Explanation:**
A constant `MAX_ZONES` is introduced to define the maximum size of the arrays. At startup, the program asks the user to enter the number of zones (`num_zones`) they intend to use. Then, with a `for` loop from 0 to `num_zones − 1`, the program asks the user to enter the name for each zone, storing it in a dedicated array `zone_names`.

**Considerations:**
- The user must remember which progressive number (0, 1, 2...) corresponds to each zone name entered, which represents a potential readability limit for the user

---

## Advantages of Using Functions and Parameter Passing

The lesson stresses the importance of using functions with parameter passing, even when a function is called only once, contrasting this approach with the use of global variables.

**Key Points:**
- **Reusability:** a function that receives data through parameters does not depend on the names of the variables of the calling program. It can be reused in different contexts, as shown by the function `show_deviations`, which remained unchanged despite the changes to the data structure (from separate variables to arrays)
- **Limiting errors:** parameter passing limits the visibility of the data. A function can operate only on the data that are explicitly passed to it, preventing accidental modifications of global variables (side effects) that can cause hard-to-find bugs
- **Structure and readability:** functions help to identify and encapsulate the solution to a "sub-problem" (e.g. the printing of the results table). This makes the main program clearer and more readable, highlighting its logical structure. Eliminating the function would remove this important aspect of code organization

**Explanation:**
Even if, after compacting the code with arrays, the function `show_deviations` is called in a single place, eliminating the parameters in favor of global variables would be a mistake. Global variables make the code less reusable and more prone to errors, since any function could modify them accidentally. Keeping the parameters guarantees that the function is an autonomous and reusable component, which interacts with the rest of the program only through a well-defined interface (its parameters).

**Special Circumstances:**
- If a function is called only once, why not eliminate the parameters and use global variables? Answer: it should not be done because the reusability and the protection from errors offered by parameters are lost
- If a function is called only once, why not eliminate it altogether and insert its code directly at the call point? Answer: it is not advisable because the important structural aspect of identifying and isolating the solution of a sub-problem is lost, worsening the readability and maintainability of the program

---

## Parameter Passing: Value vs. Address

In C++ there are two main ways of passing parameters to a function: by value and by address. Passing by address makes the position of the actual parameter available to the called function, allowing it to operate on it directly both for reading and writing. Passing by value, instead, creates a copy of the actual parameter, and any change inside the function is not reflected on the caller's original variable.

**Key Points:**
- **Passing by address:** the called function receives the memory location of the actual parameter and can modify it. Useful to transfer information computed by the function to the caller (output parameters)
- **Passing by value:** the called function receives a copy of the value of the actual parameter. The changes are local to the function. Used for information that is only used by the function and must not be altered
- **Advantage of passing by value:** helps the programmer to make fewer mistakes and to limit the propagation of bugs, since it prevents accidental changes to the caller's data

**Explanation:**
The lesson emphasizes that, although passing by address is sufficient for every type of communication between calling and called function, it is conceptually important to use passing by value for all the data that are only "input" to the function. This approach protects the data from unintended alterations. If a function tries to modify a parameter passed by value, it will modify only its local copy, and the error will not propagate to the rest of the program, making it easier to identify and fix.

---

## Handling Arrays as Parameters and the `const` Keyword

In C and C++, when an array is passed as a parameter to a function, what is actually passed is not the whole array but the address of its first element. As a consequence, even a formally "by value" passing of an array behaves in all respects like passing by address, giving the function the ability to modify the elements of the original array.

**Key Points:**
- The name of an array in C++ represents the pointer to its first element
- Passing an array to a function, even by value, allows its original content to be modified
- To protect an array from unwanted changes when it is meant only as an input parameter, the keyword `const` is used before its declaration in the formal parameters
- If an array is an output parameter (it must be filled or modified by the function), the keyword `const` must not be used

**Explanation:**
The problem is that the rule of using passing by value for input data seems to fail with arrays. To solve this inconsistency, C++ offers the keyword `const`. By placing `const` before the declaration of an array-type parameter (e.g. `const char zone_name[]`), the compiler is told that the array is read-only. Any attempt to write to an element of the array inside the function will generate a compilation error, thus ensuring data safety and respect for the principle of limiting access to only the strictly necessary information.

**Special Circumstances:**
- If an array is passed to a function and one wants to guarantee that it is not modified, how should it proceed? The keyword `const` must be placed before the declaration of the formal parameter in the signature of the function. E.g.: `void my_function(const int my_array[])`

---

## Decomposing a Problem into Sub-Problems and Functions

The lesson illustrates the software design process based on the decomposition of a complex problem into smaller, manageable sub-problems, each of which is encapsulated in a specific function. This approach improves readability, maintainability and code reuse.

**Key Points:**
- The general problem is the analysis of the price readings of a product in a geographic area divided into zones
- First sub-problem identified: acquisition of the number and name of the zones
- Second sub-problem identified: acquisition of all the data of each reading (zone and price)
- Third sub-problem identified: printing of the results in tables, one for each zone
- The third sub-problem is further broken down into three sub-tasks, each implemented by a function: 1. Printing of the table header. 2. Computation of the deviation of a reading from the average. 3. Printing of the row with price and deviation
- In total, 5 sub-problems to be turned into functions are identified

**Explanation:**
Starting from a problem already solved in a previous version, the decision is made to restart from scratch in the design in order to apply the principle of decomposition more rigorously. The goal is to break the problem down as much as possible into sub-problems, defining for each a function with a very precise task. This leads to identifying three macro-areas (acquisition of the configuration, acquisition of the data, printing of the results) and detailing the last one further, arriving at a total of five distinct functions, each responsible for a small part of the overall process.

---

## Designing a Function: the Case of `choose_zones`

The design of the first function, `choose_zones`, which has the task of acquiring from the user the number of zones and their names, is analyzed in detail.

**Key Points:**
- Name of the function: `choose_zones`
- Return value: `void`, since the results are returned through the parameters
- Input parameters: none, because the information is read directly from the user's input
- Output parameters: `num_zones` (an integer, to be passed by address with `&`) and `zone_names` (an array of strings, that is, a two-dimensional array of characters)
- Function header: `void choose_zones(int &num_zones, char zone_names[][ROW_SIZE])`
- For two-dimensional arrays passed as parameters, it is mandatory to specify the size of the second dimension (and of the following ones) in the header of the function

**Explanation:**
The design follows logical steps: 1. Choose a meaningful name. 2. Determine the input and output information. In this case, there are no inputs from the caller. The outputs are the number of zones and their names. 3. Choose the names and types for the parameters. `num_zones` is an `int`. `zone_names` is an array of arrays of characters. 4. Decide the passing mode: `num_zones` must be passed by address in order to be modified. `zone_names`, being an array, is modified even if passed by value, and `const` is not used because it must be written. 5. It is explained why the second dimension is needed for 2D arrays: the compiler uses it to compute the memory offset to reach the start of each row after the first, given that the matrix is stored linearly by rows.

---

## Designing a Function: the Case of `acquire_reading`

The design of the second function, `acquire_reading`, which handles the acquisition loop of the reading data (zone and price), is introduced.

**Key Points:**
- Name of the function: `acquire_reading`
- Return value: `void`
- Input parameters: `num_zones` (an integer)
- Purpose of the input parameter: the number of zones (`num_zones`) is needed to validate the user's input. When the user enters the code of a zone, the function must check that it is an allowed value (e.g. between 0 and `num_zones − 1`)

**Explanation:**
For this function too, inputs and outputs are analyzed. Unlike the previous one, this function needs an input from the caller: the total number of zones. This datum, computed by the function `choose_zones`, is indispensable here to verify the correctness of the data entered by the user during the acquisition loop. If the user enters an invalid zone number, the function can ask for it to be entered again.

---

## Handling Data Through Arrays

To be able to compute and print the deviations from the average, the number of readings, the sum of the prices and the prices themselves must be stored for each of the zones. These data are handled through arrays.

**Key Points:**
- The variables `num` (number of readings) and `sum` are arrays of integers
- The variable `prices` is a two-dimensional array of integers, since for each zone there is a sequence of prices
- When a two-dimensional array such as `prices` is a formal parameter of a function, its definition must include the size of the second dimension (e.g. `MAX_DIM`)
- `sum`, `num` and `prices` are output parameters, but being arrays, they are passed by value, which allows operating directly on the corresponding actual parameter

---

## The `compute_deviations` Function

This function is the heart of the printing operation and computes the deviation from the average of each reading for a specific zone. It is called iteratively for each zone. It prints nothing, it only computes.

**Key Points:**
- **Input parameters:** `sum` (sum of the elements of the zone), `num` (number of significant elements), `prices` (array of the elements). For safety, `prices` is declared `const` to avoid changes
- **Output parameter:** `deviations`, an array of floats where the results are accumulated
- The header of the function includes three input parameters (two integers and an array of integers) and one output parameter (an array of floats)

**Explanation:**
The function first computes the average of the prices for the zone. Then, it iterates through each price in the array `prices`, computes the deviation from the average and stores the result in the corresponding element of the array `deviations`.

---

## The `print_deviations` Function

This function takes care of printing the information relating to the readings of a single zone, organizing the values by rows.

**Key Points:**
- **Input parameters:** the array of prices (`prices`), the array of deviations (`deviations`) and the number of significant elements (`num`)
- The input parameters `prices` and `deviations` are locked with `const` to prevent changes
- The function has no output parameters, since its only purpose is to send data to printing (on `cout`)

---

## Program Structure and the `main` Function

The program is structured into several functions that are coordinated by the `main` function. The constants used in more than one function are defined at global level.

**Key Points:**
- The constants `MAX_NAME` and `MAX_TEAM` must be global because they are used in the headers of the subprograms
- `main` declares the variables needed, including `num_zones`, `zone_names`, `prices`, `num`, `sum` and the two-dimensional array `deviations`
- The main program consists of a series of function calls: `choose_zones`, `acquire_readings`, and then a loop for `print_header`, `compute_deviations` and `print_deviations` for each zone with at least one element

---

## Function Prototypes

C++ allows separating the header of a function (called "function prototype") from its complete implementation (the "body" or "block"). This allows a function to be used before its body has been defined in the code.

**Key Points:**
- The use of prototypes improves readability, allowing the `main` function to be placed at the beginning of the program, from which the general structure and the functions used can be understood
- To call a function, the compiler only cares about its header (name, return type, number and type of parameters) to verify that the call is correct
- The prototype is only the header of the function, which is placed at the beginning of the file to "declare" the function before its use

---

## Function Prototypes and Headers in C++

Analysis of the difference between the use of function prototypes and complete headers in C++. It is explained that, although the name of the formal parameter in the prototype is optional for the compiler (being treated as a comment), its inclusion is considered good practice to improve the readability and understanding of the code.

**Key Points:**
- The name of the formal parameter in a function prototype is inessential for compiling the program into machine language
- The name of the formal parameter is needed only inside the body of the function to express the operations to be performed on it
- It is advisable to include the parameter names in the prototypes, effectively turning them into function headers, to increase clarity
- Placing all the function headers before the `main` function helps to condense the frame of reference of the problem, making the program easier to understand by examining only a small part of the text

**Explanation:**
The proposed strategy consists of writing the complete headers of all the functions before the `main` function. This approach organizes the code so that all the sub-problems are clearly listed before the start of the main program. This facilitates both development (allowing the header to be copied and then the body of the function to be written) and maintenance, offering a localized and clear overview of the structure of the program.

---

## Managing Tabular Data

Introduction to table management, a crucial aspect of computer science that consists of organizing data in tables. Many practical problems, such as managing a registry, an inventory or a class, can be traced back to the management of tables. Initially the use of arrays for this purpose is explored, then the concept of "record" (or `struct` in C++) is introduced as a more advanced and satisfactory solution.

**Key Points:**
- Table management is an area of great importance in computer science
- A table organizes data in rows and columns, where each row represents an entity (e.g. a student) and each column a specific piece of information (field)
- The first data structures considered to represent tables are arrays
- The concept of "record" (or `struct` in C++) will be introduced as a more effective tool for managing aggregate data

**Example:**
Table management is applicable to numerous real-world contexts. Some examples include:

1. Managing a phone book
2. Managing the items in a warehouse of goods
3. Managing the students of a class
4. Recording the prices of a product in different shops, storing for each the business name, the address, the price, and other characteristics

---

## Representing the Data of a Table

Detailed analysis of how to represent in the computer the individual pieces of information (fields) that make up a row of a table, using a table of students as a case study. The choice of the appropriate data type for each field is the first fundamental step in building the data structure.

**Key Points:**
- **Surname and first name:** represented as arrays of characters (strings), defining a maximum length (e.g. 10 or 20 characters)
- **Sex:** can be represented with a single character (e.g. "M" for male, "F" for female)
- **Student ID number:** being a unique identifier, it can be represented as an integer value or, alternatively, as a string of characters
- **Date of birth:** a composite datum (day, month, year) that offers different representation options

**Explanation:**
For the practical example of the course, a specific representation is chosen: surname and first name as strings, sex as a single character, date of birth as three separate integers and student ID number as an integer value. Once the representations of the individual fields are defined, the next step is to aggregate them to represent the whole table.

**Example:**
The date of birth, made of day, month and year, can be represented in the computer in different ways.

**Calculation Steps:**
- As three separate integers: one integer for the day, one for the month and one for the year. This is the solution chosen for the example of the course
- As a string with fixed format: a single sequence of characters where the position determines the information (e.g. "DDMMYYYY", such as "05101995"). It requires 8 characters, using 4 digits for the year to avoid problems like the Millennium Bug
- As a string with separators: a sequence of characters of variable length that uses a special character (e.g. "/") to separate day, month and year (e.g. "5/10/1995"). It requires up to 10 characters

---

## Operations on Tables

Description of the fundamental operations that can be performed on a table of data: insertion of new elements, deletion of existing elements, search of elements according to specific criteria and sorting of the table.

**Key Points:**
- **Insertion:** adding a new row. If the table is sorted, the insertion must take place in the correct position to maintain the order
- **Deletion:** removal of a row. It requires a preliminary search to locate the element to delete
- **Search:** finding one or more elements that satisfy certain conditions. The search can return a single individual (e.g. search by student ID number) or a subset of individuals (e.g. search by sex)
- **Sorting:** reorganizing the rows of the table according to the values of a specific field (e.g. alphabetical sorting by surname)

**Explanation:**
Search is a central operation. A linear (or sequential) scan examines every element, but it is inefficient for large tables. If the table is sorted with respect to a field, a much faster search such as binary search can be used, which halves the search space at each step. Sorting therefore offers a great advantage in terms of search performance. A later challenge consists in reordering the table according to a field different from the current one.

---

## Representing Tabular Data with Heterogeneous Types

The lesson addresses the problem of how to store in a program a table of data, such as a list of students, where each row (individual) is made of fields with different data types (e.g. integer student ID number, string surname). The twofold need to treat the row as a unit (for moves) and to access the individual fields (for checks) is highlighted.

**Key Points:**
- Need to treat the data of an individual (the whole row) as a unit for operations such as moving
- Need to select and operate on individual fields of an individual, for example for specific checks (e.g. sex)
- Arrays, a potential tool for managing lists, require all their components to be of the same type
- This is a problem when the fields of a table are heterogeneous (e.g. the student ID is an integer, the surname is an array of characters)

**Explanation:**
Various solutions to represent the table are explored and criticized, trying to overcome the constraint of the homogeneous types of arrays:

1. **Parallel arrays:** an array is created for each column (field) of the table (e.g. one array for the student IDs, one for the surnames, etc.)
   - **Disadvantage:** if a whole individual (a row) has to be moved, as many swap instructions as there are fields must be executed, making the operation inefficient and cumbersome
2. **Unitary representation as strings:** all the fields are turned into sequences of characters so they can be stored in a single two-dimensional array (matrix of characters)
   - **Variant A (fixed format):** each field has a fixed length (e.g. student ID 6 characters, name 10). To access a field, its starting position and its exact length must be known
   - **Variant B (free format):** the fields are separated by a special character (e.g. "/"). To access a field, the string must be scanned and the separators counted
   - **Disadvantage:** both variants make the selection of a single field very complex
3. **Intermediate solution (array of arrays of strings):** the table is represented as an array of individuals, where each individual is in turn an array of strings (the fields). For example, `student[i][0]` for the student ID, `student[i][1]` for the surname. To improve readability, symbolic constants can be used (e.g. `student[i][ID_NUMBER]`)
   - **Disadvantage:** all the fields must be sized with the maximum number of characters required by the longest field (e.g. 10, for first name/surname), causing a significant waste of memory for the shorter fields (e.g. student ID, sex)

**Conclusion:** None of these solutions is considered fully satisfactory for the management of generic tables with heterogeneous data, since they introduce complexity, inefficiency or waste of resources.

**Example:**
A table containing information on students, with the following fields: Student ID (integer), Surname (string), First name (string), Sex (character, "M" or "F"), Day of birth (integer), Month of birth (integer), Year of birth (integer).

---

## Tasks and Suggestions

- Consider how to tackle the problem if it were necessary to split a city into more than two zones, for example into twenty districts, and what problems the current approach based on multiple calls to a function would involve
- Carry out step by step the transformation of the current program, taking into account the transformation of the data structure from single variables to arrays
- The listener is left the possibility of evaluating whether, for the variable `deviations`, a simple one-dimensional array can be used instead of a two-dimensional array, to be reused for each zone
- In lessons 23 and 24 the problem of table management will be addressed, a topic with considerable application potential. It will start by trying to represent tables with arrays, and then introduce the concept of record (`struct`)
