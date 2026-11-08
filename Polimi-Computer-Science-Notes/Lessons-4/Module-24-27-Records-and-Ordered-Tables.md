# Modules 24-27: Records, Arrays of Records and Ordered Tables

## Topic Overview

Data structures, arrays of records and table management. The lessons go in depth into the management of large masses of data through structures and arrays of records in the C and COBOL languages. Key concepts are illustrated, such as the definition of a record, the management of ordered tables, the insertion and deletion of elements, parameter passing by value and by reference, and naming conventions. Strategies for handling non-significant elements and the importance of efficiency in the manipulation of structured data are also analyzed.

---

## Key Points Summary

1. Introduction of the COBOL language and comparison with Fortran
2. Need to manage large masses of data organized in tables
3. Concept of record/structure to aggregate data of different types
4. Definition of a structure in C through the keyword `struct`
5. Example of a student structure with fields: student ID, surname, first name, sex, date of birth
6. Definition of the date-of-birth structure as a structure made of day, month, year
7. Importance of the order of definition of structure types
8. Naming conventions for types, variables and constants
9. Arrays of structures: representation of a table of students as an array of `struct Student`
10. Selection of fields through dot notation

**Key Quotes:**
> "With these two structures, these two modes of aggregation, we are now able to represent sufficiently complex structures."

> "The field with respect to which a table is sorted is generally called the key field."

> "In this case efficiency considerations prevail over ours."

> "Whenever we have a structured situation to which we want to give an overall value, we use curly brackets."

---

## The COBOL Language and Comparison with Fortran

COBOL (Common Business Oriented Language) was designed to handle commercial applications that require the management of large masses of data organized in tables, unlike Fortran, which was oriented towards scientific and technical computation.

**Key Points:**
- COBOL is an acronym for Common Business Oriented Language
- COBOL was designed for commercial applications, not for complex scientific calculations
- Fortran was the first high-level language, oriented towards scientific computation
- COBOL introduces the management of heterogeneous data through records

**Explanation:**
The instructor explains that the birth of COBOL answered the need to handle commercial data, often organized in tables and stored on permanent media such as tapes and disks, while Fortran was better suited to scientific computation.

---

## The Concept of Record/Structure in Programming Languages

The record (or structure) is a construct that allows aggregating data of different types under a single name, unlike the array, which aggregates data of the same type.

**Key Points:**
- The record allows giving a single name to information of different types
- In C the keyword `struct` is used to define a structure
- A record can contain other records as fields (example: date of birth made of day, month, year)
- The definition of a structure type must precede its use in other types

**Explanation:**
The instructor shows how a student structure is defined in C, with fields of different types, and stresses the importance of the order of definition of the types.

**Example:**

```cpp
struct DateOfBirth {
    int day;
    int month;
    int year;
};

struct Student {
    int id;
    char surname[...];
    char name[...];
    char sex;
    struct DateOfBirth dateOfBirth;
};
```

**Calculation Steps:**
- The structure `DateOfBirth` is defined first
- Then the structure `Student`, which uses `DateOfBirth` as a field, is defined

**Considerations:**
- Give meaningful names to types and fields
- Follow the naming conventions: capital initial for types, lowercase for variables, all uppercase for constants

---

## Arrays of Structures and Table Management

A table of data can be represented as an array of structures, where each element of the array is a record that represents an individual (e.g. a student).

**Key Points:**
- The table is an array of `Student` structures
- To select a field of an element, dot notation is used: `arrayName[index].field`
- It is possible to represent large archives (e.g. 1,000 or 10,000 inhabitants of a municipality)

**Explanation:**
The instructor explains how to access the fields of a structure inside an array and how to represent complex archives through arrays of records.

**Example:**
`class[i].surname`

**Calculation Steps:**
- `class` is the array of `Student`
- `i` is the index of the element
- `surname` is the field of the structure `Student`

**Considerations:**
- Size the array according to the maximum expected capacity
- Correctly handle access to the fields through dot notation

---

## Swapping Records and Manipulating Arrays of Structures

To swap two records in an array of structures, a temporary variable of structure type is used. The manipulation operations (insertion, deletion) require attention to the management of the size and of the significance of the elements.

**Key Points:**
- To swap two elements, a temporary variable of type `Student` is used
- It is not necessary to assign field by field, it is enough to assign the whole record
- The size of the array must be fixed in advance
- To delete an element, the array can be compacted or the element can be marked as non-significant

**Explanation:**
The instructor shows how to swap two students in the array and discusses the strategies to delete an element: compaction or marking through a special field.

**Example:**

```cpp
Student temp = class[i];
class[i] = class[j];
class[j] = temp;
```

**Calculation Steps:**
- A temporary variable `temp` of type `Student` is created
- `class[i]` is copied into `temp`
- `class[j]` is copied into `class[i]`
- `temp` is copied into `class[j]`

**Considerations:**
- Verify that the size of the array is sufficient
- Correctly handle the temporary variable for the swap

**Special Circumstances:**
- If an element is deleted, one can choose between compacting the array (moving all the following elements) or marking the element as non-significant (e.g. student ID zero)

---

## Handling Non-Significant Elements in an Array of Structures

To handle deleted or non-significant elements in an array of records, different strategies can be adopted: use a special value in a field (e.g. student ID zero), add a significance field, or define a new type that includes the significance field.

**Key Points:**
- Use an impossible value (e.g. student ID zero) to mark an element as non-significant
- Add a significance field (e.g. an integer that is 1 if significant, 0 if not)
- Define a new type `StudentInTable` with a field `student` and a field `significant`
- Handle the selection of fields with one extra step if `StudentInTable` is used

**Explanation:**
The instructor illustrates the various solutions to handle the presence of empty elements in the array, highlighting the advantages and disadvantages of each.

**Example:**

```cpp
struct StudentInTable {
    Student stud;
    int significant;
};
```

**Calculation Steps:**
- The field `significant` indicates whether the element is valid (1) or not (0)
- To access the surname: `class[i].stud.surname`

**Considerations:**
- Choose the solution best suited to the needs of the application
- Correctly handle the logic of access to the fields if an extra structure level is introduced

**Special Circumstances:**
- If every possible value can be assumed by a field, it is not possible to use a special value to mark the element as non-significant: in that case, add a significance field

---

## Handling the Full and Empty Part of the Array Through the `num` Field

To know which elements of an array of structures are significant, a field `num` that indicates the number of valid elements can be used. The elements from 0 to `num − 1` are significant, the following ones are available.

**Key Points:**
- The field `num` indicates the number of significant elements
- The index of the first free element coincides with the value of `num`
- It is necessary to know `num` to avoid accessing invalid elements

**Explanation:**
The instructor explains that, to avoid having to mark every element, one can simply keep track of the number of significant elements and consider only those.

**Example:**

```cpp
struct StudentSet {
    Student class[MAX];
    int num;
};
```

**Calculation Steps:**
- `class` is the array of `Student`
- `num` is the number of significant elements

**Considerations:**
- Always update the field `num` when an element is inserted or deleted
- Never access elements beyond `num`

---

## Managing an Ordered Table Through Insertion and Deletion Functions

The lesson focuses on the management of a table ordered with respect to a key field (student ID), implementing the insertion and deletion operations on records, and deliberately leaving out the search for teaching reasons. The importance of keeping the table ordered and correctly updating the number of elements, avoiding duplicates and holes in the structure, is highlighted.

**Key Points:**
- The table is sorted with respect to the key field, in this case the student ID
- Insertion requires determining the correct position and shifting the following elements
- Deletion involves compacting the table to avoid holes
- The number of actual elements must be updated after each operation
- Insertion happens only if the student ID is not already present
- The main functions are: `initialize_table`, `insert_if_not_exists`, `delete_if_exists`, `print_table`
- Data persistence requires saving to a file
- For very large tables, management through matrices can be inefficient and the need for pointers and dynamic management is introduced

**Explanation:**
During the lesson, it is explained how to manage an ordered table of students, where each student is identified by a unique student ID. It starts from the initialization of the table, and the insertion functions are implemented (which checks the absence of duplicates and inserts in the correct position) and deletion (which deletes the record and compacts the table). The need to update the number of elements and to use meaningful function names for clarity is stressed. It is also mentioned that, for reasons of efficiency, pointers will be introduced in the future for more dynamic management.

**Example:**
Suppose an ordered table of students with student IDs 1001, 1003, 1005. If a student with ID 1002 is to be inserted, the correct position must be found (between 1001 and 1003), the following elements (1003 and 1005) shifted by one position and the new record inserted. If instead the student with ID 1003 is to be deleted, the record is deleted and the table is compacted by moving 1005 into the position of 1003.

**Calculation Steps:**
- Check whether the student ID to insert is already present
- Determine the correct position for the insertion
- Shift the following elements by one position
- Insert the new record
- Update the number of elements
- For deletion, search for the student ID
- Delete the record and compact the table
- Update the number of elements

**Considerations:**
- Avoid duplicates by checking for the presence of the student ID before insertion
- Compact the table after each deletion to avoid holes
- Always update the number of actual elements
- Use clear and meaningful function names for teaching purposes
- Handle data persistence by saving the table to a file

**Special Circumstances:**
- If the table contains several students with the same surname, use a composite key (for example, surname and first name) to guarantee uniqueness
- If the table is very large and the operations are inefficient, consider the use of pointers and dynamic data structures

---

## Defining the Interfaces of the Table Management Functions

The lesson illustrates how to define the interfaces of the main functions for managing the table, specifying the input and output parameters, and the use of parameters passed by address or as return values.

**Key Points:**
- The function `initialize_table` can directly return an initialized table or modify it through a parameter passed by address
- The function `insert_if_not_exists` receives the table and the record to insert, and returns the new version of the table
- The function `delete_if_exists` receives the table and the student ID to delete, and returns the new version of the table
- The function `print_table` allows displaying the current state of the table

**Explanation:**
It is explained how to design the interfaces of the functions for managing the table, choosing between parameters passed by address or return values, and how these functions interact with one another in `main`.

**Considerations:**
- Choose the most suitable parameter passing mode (address or return value) according to the language and the needs
- Define function names that clearly reflect their functionality

---

## Parameter Passing in Functions (by Value vs. by Address)

Parameter passing in functions can take place by value or by address. If the parameter is only an input and of simple type, it is passed by value. If the parameter is an output or of complex type (such as arrays or large structures), it is passed by address for reasons of efficiency and to allow the modification of the original value.

**Key Points:**
- Formal parameter both input and output: passing by address is mandatory if the original value is to be modified
- Parameter only input and of simple type: passing by value
- Parameter only input but of complex type (arrays, structures): often passed by address for reasons of efficiency
- In the case of large arrays, passing by value would involve copying the entire structure, with a negative impact on performance

**Explanation:**
During the lesson it is explained that, for example, the function `print_table` receives as a parameter a table of students. Even if logically it would only be an input and therefore passable by value, for reasons of efficiency passing by address is preferred, avoiding the copy of potentially very large structures. This principle also applies to other functions that modify or use complex data structures.

**Example:**
The function `print_table` receives as a parameter a table of type `StudentSet`. Even though the function does not modify the table, the parameter is passed by address to avoid copying the whole structure.

**Calculation Steps:**
- The function is declared with a parameter by address
- When it is called, the address of the variable `class` is passed
- The function accesses the data without modifying them, but without creating useless copies

**Considerations:**
- Always assess the size of the data structure before deciding the type of parameter passing
- If the function must modify the parameter, passing by address is mandatory
- For large structures, passing by value can be inefficient

**Special Circumstances:**
- If very small structures are handled and logical clarity is a priority, passing by value can be considered

---

## Structure and Management of a Table of Students in C++

The table of students is managed through a structure made of an array of student records and a field that indicates the actual number of students present. The main operations are: initialization, insertion, deletion and printing of the table.

**Key Points:**
- The structure `StudentSet` contains an array `list` and a field `num`
- The initialization of the table assigns initial values to both fields
- The insertion requires reading all the fields of the new student
- The deletion is based on the student ID of the student
- The printing shows only the student ID field for brevity
- The operations are handled through characters ("i", "e", "f") and a `while` loop

**Explanation:**
The program is structured to handle a sequence of insertion and deletion operations on a table of students. The table is represented by a structure with two fields: `list` (array of students) and `num` (number of students present). The main functions operate on this structure, passing the parameters by address when needed. The initialization assigns starting values, insertion and deletion modify the table, printing shows the current state.

**Example:**
The function `initialize_table` creates a variable of type `StudentSet`, assigns the initial value to `num` (for example 4) and initializes the array `list`.

**Calculation Steps:**
- A variable `tab` of type `StudentSet` is declared
- The initial value is assigned to `num`
- The array `list` is initialized
- The variable `tab` is returned via `return`

**Considerations:**
- Always declare the global types and constants before the `main` function
- Use constants to improve the readability of the code
- Handle the date-of-birth fields separately as a record

**Special Circumstances:**
- If the table must handle a very large number of students, consider the use of dynamic data structures

---

## Managing Operations Through a Loop and Command Characters

The insertion, deletion and end operations are handled through characters ("i", "e", "f") entered by the user. A `while` loop controls the sequence of operations until the user decides to terminate.

**Key Points:**
- The character variable `operation` determines the action to execute
- The `while` loop continues as long as `operation` is different from "f"
- Before entering the loop, the first operation is read
- Inside the loop, insertion or deletion is handled according to the value of `operation`
- After each operation, the table is printed and the next operation is requested

**Explanation:**
The program asks the user to enter a character to select the desired operation. Depending on the character ("i", "e", "f"), the program performs the insertion of a new student, the deletion of a student by student ID, or ends the execution. The loop ensures that the user can perform several operations in sequence.

**Example:**
The user enters "i" to insert a student, "e" to delete one, "f" to end. The `while` loop checks the value of `operation` and calls the corresponding function.

**Calculation Steps:**
- The first operation is read
- The `while` loop is entered if `operation` is different from "f"
- It is checked whether `operation` is "i" or "e" and the corresponding function is executed
- The table is printed after each operation
- The next operation is requested from the user

**Considerations:**
- Make sure the user enters only valid characters ("i", "e", "f")
- Correctly handle the reading of the first operation before the loop

**Special Circumstances:**
- If the user enters an invalid character, the program should handle the error and request the input again

---

## Initializing Records and Arrays of Structures

When initializing a record made of several fields, the values must be separated by commas. If one of the fields is an array, the values of the array are also separated by commas. Complex structures, such as nested records, are initialized using curly brackets. For example, the student type is made of 5 elements: student ID, surname, first name, sex, date of birth, where date of birth is in turn a record with day, month and year.

**Key Points:**
- The values of the fields of a record are separated by commas
- For array fields, the values are separated by commas
- Nested structures are initialized with curly brackets
- Example of a student type with 5 fields, one of which (date of birth) is a record

**Explanation:**
During the lesson it is explained how to assign values to records and arrays of structures, stressing the importance of the syntax (commas and curly brackets) and showing how a student type is composed. It is also illustrated how several students are inserted in a table and how the table is returned through a function.

**Example:**
A variable `Tab` that represents a table of students is created. Each student has a student ID (for example 7), a surname (for example Rossi), a first name (for example Marco), a sex (for example "M"), and a date of birth made of day, month and year. Four students are inserted in the table, each initialized with its own values.

**Calculation Steps:**
- The student structure is defined with the required fields
- Each student is initialized using curly brackets and separating the values with commas
- Several students are inserted in the array `list` of the table
- The table is returned through the function with `return Tab`

**Considerations:**
- Always separate the values with commas
- Use curly brackets for complex structures
- Pay attention to the order of the fields during initialization

**Special Circumstances:**
- If a new element must be inserted in first position, move all the existing elements by one position
- If an element is inserted at the end, make sure the position is correct and that the maximum number of elements is not exceeded

---

## Table Management Functions: Print, Insert, Delete

The management of a table of students provides specific functions for printing, inserting and deleting elements. The function `print_table` uses a loop to scan all the significant elements, determined by the field `num`. The insertion and deletion functions require searching for the correct position, keeping the table sorted by increasing student ID.

**Key Points:**
- The function `print_table` scans all the elements from the first (index zero) up to `num`
- The parameter of the function `print_table` is passed by reference or address
- The insertion and deletion functions keep the table sorted
- During insertion, the following elements must be shifted by one position
- During deletion, the position of the previous element is identified

**Explanation:**
It is explained how the function `print_table` shows the student IDs of the students present, how the insertion of a new student is handled (search for the position, shifting of the elements) and how an element is deleted by identifying the position of the previous element. The importance of keeping the table sorted is stressed.

**Example 1:**
A student with student ID 91 is to be inserted. The table is scanned (…, 84) and it is verified that 91 must be inserted after the last element (84).

**Calculation Steps:**
- The table is scanned until the correct position is found
- It is verified that 91 is greater than the last element
- 91 is inserted at the bottom of the table

**Example 2:**
A student with student ID 50 is to be inserted. The table is scanned and it is found that it must be inserted after the element with student ID 48 and before 63.

**Calculation Steps:**
- The position of the previous element is kept during the scan
- 50 is inserted in the correct position, shifting the following elements

**Considerations:**
- Keep the table sorted after each insertion or deletion
- Correctly handle the shifting of the elements
- Use the field `num` to determine the number of significant elements

**Special Circumstances:**
- If an element is inserted in first position, shift all the elements by one position
- If an element is deleted, correctly update the field `num` and shift the following elements

---

## Sequential Search and the Service Function `search_if_exists_and_position`

To insert or delete an element in an ordered table, the correct position must be found. Sequential search is used, even though the table is sorted, for teaching reasons and for compatibility with other storage mechanisms. The function `search_if_exists_and_position` returns both the existence of the element (0 or 1) and the position of the previous element.

**Key Points:**
- Sequential search starts from the first element and scans the table
- The function returns two pieces of information: existence (0 or 1) and the position of the previous element
- The position of the previous element is useful both for insertion and for deletion
- The function is a service to the insertion and deletion functions

**Explanation:**
During the lesson it is illustrated how the function `search_if_exists_and_position` is fundamental for handling both insertion and deletion. It is explained that the function must be able to return both whether the element exists and the position of the previous element, in order to then insert or delete correctly.

**Example:**
A student with student ID 5 is to be inserted. The function `search_if_exists_and_position` scans the table and determines that 5 must be inserted in first position (after a fictitious element of index −1).

**Calculation Steps:**
- The table is scanned from the beginning
- It is determined that no element has a student ID lower than 5
- The position −1 is returned for the insertion at the head

**Considerations:**
- Always return both the existence and the position of the previous element
- Correctly handle the boundary cases (beginning and end of the table)

**Special Circumstances:**
- If the table is empty, the function must return that the element does not exist and that the position for insertion is −1
- If the element to insert is smaller than all the others, the previous position is −1

---

## Parameter Passing by Reference and by Value

In the context of managing a table of students, passing parameters by reference is used to avoid the inefficiency of copying entire data structures. The parameters that represent results (such as `exists` and `pos`) are passed by reference, while the input data can be passed by value or by reference depending on the need.

**Key Points:**
- The datum parameter (student ID) can be passed by value
- The table of students is passed by reference to avoid useless copies
- The results of the function (`exists` and `pos`) are passed by reference to be able to modify them directly
- Indirect addressing makes it possible to operate directly on the original variable in `main`

**Explanation:**
During the call of functions such as `search_if_exists_and_position`, the parameters are passed so that the changes made inside the function are also reflected outside, especially for the results and for the main data structure.

**Example:**
When `search_if_exists_and_position` is called with `datum = 91`, `Tab` (the table of students), `exists` and `pos`, the value 91 is copied, while `Tab`, `exists` and `pos` are passed by reference. Thus, any change to `exists` and `pos` in the function directly updates the local variables of the calling function.

**Calculation Steps:**
- The local environment of the function is created
- The parameter `datum` receives the value 91
- `Tab` receives the reference to the table of students
- The variables `exists` and `pos` are referenced directly
- The changes to `exists` and `pos` are also visible in the calling function

**Considerations:**
- Avoid copying large data structures by passing by reference
- Make sure the parameters passed by reference are correctly initialized

**Special Circumstances:**
- If a data structure shared among several functions must be modified, always pass by reference

---

## Handling Insertion and Deletion in an Ordered Table

The insertion and deletion functions in an ordered table of students require careful handling of the positions and the shifting of the elements to maintain the ordering and consistency of the data.

**Key Points:**
- To insert a new element, it is first verified whether it already exists through `search_if_exists_and_position`
- If it does not exist and there is space (`num <= dim`), the elements are shifted to the right to make room
- The insertion position is `pos + 1`
- After the insertion, the field `num` is incremented
- To delete, it is verified whether it exists through `search_if_exists_and_position`
- If it exists, the elements are shifted to the left to cover the deleted position
- After the deletion, the field `num` is decremented
- Handling of special cases: insertion or deletion in first position (`pos = -1`)

**Explanation:**
Maintaining the ordering requires that, during insertion, all the elements following the insertion position be shifted by one position to the right. Similarly, during deletion, the following elements are shifted to the left.

**Example:**
Assume a table with students with student IDs in increasing order and a student with student ID 91 is to be inserted. The function `search_if_exists_and_position` determines that it does not exist and that it must be inserted at the end. The elements are not shifted and the new student is inserted in position 4. The field `num` is updated to 5.

**Calculation Steps:**
- Call of `search_if_exists_and_position` with `datum = 91`
- Result: `exists = 0`, `pos = 3`
- Check that `num <= dim`
- Insertion in position `pos + 1 = 4`
- Update of `num` to 5

**Considerations:**
- Always verify that there is space in the table before inserting
- Correctly handle the cases of insertion or deletion in first position
- Always update the field `num` after each operation

**Special Circumstances:**
- If the table is full (`num > dim`), a new element cannot be inserted
- If the element in first position is deleted, `pos` must be −1 to correctly handle the shifting

---

## Managing the Local Environment and the Execution Flow Between Functions

During the execution of a structured C++ program, each function has its own local environment, with its own variables and parameters. The passage of control between functions involves the suspension of the calling function and the creation of a new environment for the called function.

**Key Points:**
- Each function has local variables and formal parameters
- `main` contains variables such as `operation`, `id`, `new_student`, `class`
- When a function is called, a new local environment is created
- Parameter passing can take place by value or by reference
- At the end of the called function, control returns to the calling function

**Explanation:**
The local environment of each function guarantees the isolation of the variables and the correct management of the data flow between functions. Parameter passing and the handling of the results are fundamental for the consistency of the program.

**Example:**
In `main`, after reading the data of the new student, `insert_if_not_exists` is called. This function creates its own local environment, passes the parameters, and in turn calls `search_if_exists_and_position`, which creates a further local environment. The parameters are passed and the results returned through local variables and references.

**Calculation Steps:**
- `main` reads the data and calls `insert_if_not_exists`
- `insert_if_not_exists` creates local variables and calls `search_if_exists_and_position`
- `search_if_exists_and_position` operates on the parameters and updates the results
- Control returns to `insert_if_not_exists`, which completes the insertion
- Finally, control returns to `main`

**Considerations:**
- Make sure the local variables are correctly initialized
- Correctly handle the passing of parameters between functions

**Special Circumstances:**
- If a function modifies a variable passed by reference, the change is also visible in the calling function
