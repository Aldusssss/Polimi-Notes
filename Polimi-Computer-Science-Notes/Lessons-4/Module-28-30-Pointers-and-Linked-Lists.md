# Modules 28-30: Pointers, Linked Lists and Dynamic Allocation

## Topic Overview

Pointers, linked lists and dynamic allocation. The lessons show how to move from a table managed with static arrays to a dynamic representation based on pointers: creation of elements with `new`, the dereferencing operator, nodes and linked lists, insertion and deletion with the release of memory through `delete`, scanning of a list, a test strategy and the execution model with heap allocation.

---

## Key Points Summary

1. Management of a table with static arrays and its limits
2. Problem of the predefined maximum size and inefficiency of insertion/deletion
3. Introduction to the dynamic representation of a table through pointers
4. Dynamic creation of elements in memory with the `new` operator
5. Concept of pointer as a reference to an object in memory
6. Declaration of pointer-type variables in C++
7. Dereferencing operator `*` to access the pointed object
8. Structure of a linked list made of nodes
9. Definition of a node with a data field and a pointer to the next one (`next_ptr`)
10. Access to the fields of a pointed object through `(*pointer).field`

**Key Quote:**
> "To be sufficiently confident that the program is correct, remember that certainty could come only from a formal proof of correctness, into which we do not want to venture for the moment."

---

## Managing a Table with Dynamic Data Structures (Linked Lists)

A way of representing a table that overcomes the limits of static data structures such as arrays is presented. Unlike arrays, whose maximum size must be defined before execution, this new mode allows the structure to grow dynamically during execution, allocating new elements only when needed. This approach solves both the problem of the fixed size and that of the inefficiency in inserting and deleting elements, which in arrays require moving a considerable part of the data.

**Key Points:**
- Dynamic data structures, such as linked lists, allow memory to be allocated during the execution of the program, overcoming the fixed-size limit of arrays
- The insertion and deletion of elements in a linked list are more efficient because they do not require moving other elements, only modifying some pointers
- The creation of new elements takes place through the `new` operator followed by the type of object, which allocates the space in memory and returns a pointer to it
- A pointer is a variable that does not contain a direct value, but the memory address of another object
- To access the object a pointer refers to, the dereferencing operator `*` is used (e.g. `*pointer`)
- A list is a chain of nodes, where each node contains the information (e.g. the data of a student) and a pointer to the next node of the chain
- To access a field of a pointed object, the syntax `(*pointer).field` is used. The parentheses are essential because of operator precedence
- C++ offers the arrow operator `->` as a syntactic shortcut to access the fields of a pointed object (e.g. `pointer->field`), which is equivalent to `(*pointer).field`

**Explanation:**
To create a table dynamically, pointers and dynamic memory allocation are used. Instead of a preallocated array, the table is represented by a chain of "nodes". Each node is a record made of two main fields: one to hold the actual data (e.g. the information on a student, called `stud_data`) and another field, which is a pointer, to store the address of the next node in the sequence (called `next_ptr`).

The table itself is identified by a pointer to its first element (the "head" of the list). To add a new element, the `new` operator is used to create a new node in memory. This new node is then "linked" to the list by modifying the `next_ptr` pointer of the previous element so that it points to the new node. Navigation through the table takes place starting from the head and following the chain of `next_ptr` pointers from one node to the next.

**Example:**
A table of students organized as a linked list, sorted by increasing student ID, is considered. The list contains students with IDs 7, 48, 63, 84, etc. The variable `class` is a pointer that points to the first element of the list (the one with ID 7).

**Calculation Steps:**
- To locate the object (the node) pointed to by `class`, the dereferencing operator is used: `*class`
- To select the field `id` of the first student, `class` must first be dereferenced to obtain the node, then the field `stud_data` is selected and finally the field `id`. The complete notation is `(*class).stud_data.id`. The parentheses are mandatory because the operator `.` has precedence over `*`
- Using the arrow operator `->`, the same operation becomes more readable: `class->stud_data.id`
- To access the second student (ID 48), the pointer to the second node must first be obtained, which is stored in the field `next_ptr` of the first node. The expression for this pointer is `class->next_ptr`
- To obtain the ID of the second student, the same logic is applied starting from the pointer to the second node: `(class->next_ptr)->stud_data.id`

---

## Transforming a Program from Array Management to Pointer Management

The lesson focuses on transforming a table-management program (e.g. a student registry) from a version that uses an array as a store to one that uses a pointer-based structure for dynamic, non-sequential management. The goal is to modify the bare minimum of the code, keeping the same program logic and the same function interfaces.

**Key Points:**
- The general logic of the program and the definition of the record with the student information do not change
- The way the table is created and managed changes
- A new type of record, the "node", is introduced, which contains two fields: one for the student data (`stud_data`) and a pointer to the next element (`SPTR` or `next_ptr`)
- The table is no longer an array, but a single pointer to the first node of the list. If this pointer is null (it is 0 or NULL), the table is empty

---

## Modifying the Functions for Pointer-Based Management

The main functions of the original program are analyzed and it is shown how to adapt them to the new pointer-based data structure.

**Key Points:**
- The functions keep the same names: `initialize_table`, `insert_if_not_exists`, `delete_if_exists`, `search_if_exists_and_position`, `print_table`
- The parameters that represent the table, previously of type "array of students", become of type "pointer to node"
- The variable that represents the table in `main` (e.g. `class`) changes type, becoming "pointer to node", but the rest of `main` remains identical

**Example 1 (`initialize_table`):**
- In the array version, the initialization could consist in setting an element counter to 0
- In the pointer version, initializing the table means setting the pointer to the head of the list to a null value
- The function therefore simply returns the value 0 (or NULL), meaning that the table is empty and does not point to any element

**Example 2 (`search_if_exists_and_position`):**
- This function, which identifies the position for insertions or deletions, undergoes the most significant changes
- The return value that indicates the "position" is no longer an integer index, but a pointer to the node that precedes the one of interest
- **Empty-table check:** the pointer to the table is checked for being null (`Tab == 0`) instead of checking a counter (`Tab.num == 0`)
- **Access to the first element:** the arrow operator is used (`Tab->stud_data.id`) instead of the array index (`Tab.list[0].id`)
- **Scanning the list:** to move to the next element, the position pointer is updated with the value of the pointer field of the current node (`pos = pos->next_ptr`) instead of incrementing an index (`pos++`)
- **Checking the end of the list:** it is checked whether the pointer to the next element is null (`pos->next_ptr == 0`)
- **Access to the next element:** to read a datum (e.g. student ID) of the element following the one pointed to by `pos`, a double dereference is used: `pos->next_ptr->stud_data.id`

**Example 3 (`insert_if_not_exists`):**
- The local variable `position` becomes of type "pointer to node"
- **Creation of the new element:** space is no longer looked for in a preallocated array. A new node is created dynamically in memory using the statement `new node`. The pointer to this new memory space is saved in a temporary variable (e.g. `temp`)
- The insertion operation no longer requires moving elements in the array, making it much more efficient
- **Insertion at the head (if `position` is 0/NULL):** 1. The `next` pointer of the new node (`temp->next_ptr`) is made to point to the old first element of the list (`Tab`). 2. The pointer of the table (`Tab`) is updated to point to the new node (`temp`)
- **Insertion in the middle or at the end:** (the logic is only hinted at) the `next` pointer of the previous node (`position`) is modified to point to the new node, and the `next` pointer of the new node to point to the following one

---

## Insertion in a Linked List with Dynamic Allocation

Explanation of how to insert a new element (student) in a table implemented as a linked list, handling the dynamic allocation of memory and distinguishing the cases of insertion at the head or at an intermediate position.

**Key Points:**
- The function `insert_if_not_exists` handles the addition of new nodes
- It is essential to distinguish between insertion in first position and insertion in an intermediate position
- When inserting in an intermediate position, it is crucial to first update the pointer of the new element and then that of the previous element, so as not to lose the link with the rest of the list
- The data field of the new node (`temp->stud`) is populated with the information passed to the function (`new_student`)

**Explanation:**
The insertion of a new element requires two different procedures depending on the position. If the list is empty or the element must be inserted in first position (the result of the search is null), the newly generated element is linked to the head of the existing table. The `next_ptr` pointer of the new element will point to the old head of the list and the head of the list will point to the new element. If instead the element must be inserted in an intermediate position (defined by `position`), the new element (`temp`) must be inserted between the element `position` and its successor. To do so, the `next_ptr` pointer of the new element is first set to point to the successor of `position` (`temp->next_ptr = position->next_ptr`). This step is crucial so as not to lose the reference to the rest of the list. Then, the `next_ptr` pointer of the element `position` is updated to point to the new element (`position->next_ptr = temp`).

---

## Deletion from a Linked List with Memory Deallocation

Description of the process of deleting an element from a linked list, distinguishing between the deletion of the element at the head and of an element in an intermediate position, and illustrating the importance of deallocating memory with the `delete` operator.

**Key Points:**
- The function `delete_if_exists` handles the removal of nodes
- The cases of deletion at the head and in an intermediate position must be handled separately
- The concept of "short-circuiting" an element consists in modifying the pointers to exclude it from the chain of the list
- The `delete` operator is fundamental to free the dynamically allocated memory and prevent memory leaks, returning the space to the system

**Explanation:**
For deletion too two cases are distinguished. If the element to delete is in first position (`position` is zero), a temporary variable `temp` is used to point to the head of the list (`Tab`). Then, the head of the list (`Tab`) is updated to point to the next element (`Tab->next_ptr`), effectively "short-circuiting" the first element. If the element to delete is in an intermediate position, `position` identifies the element preceding the one to delete. `temp` is used to point to the element to delete (`temp = position->next_ptr`). Then, the element `temp` is "short-circuited" by updating the pointer of the previous element (`position->next_ptr = temp->next_ptr`) so that it points to the successor of the deleted element. Finally, to recover the memory, the statement `delete temp` is used, which returns the memory space of the element pointed to by `temp` to the system, making it reusable.

---

## Scanning and Printing a Linked List

Illustration of how to traverse (scan) a linked list to access the data of each node, in particular to print the key field of all the elements present.

**Key Points:**
- The scan of the list takes place through a loop that starts from the head
- A temporary pointer variable is used to iterate over the elements
- The termination condition of the loop is reaching a null pointer (end of the list)
- At each step, the pointer advances to the next node through the field `next_ptr`

**Explanation:**
The function `print_table` uses a `for` loop to scroll through the list. A local pointer variable (`stu_ptr`) is initialized with the value of the head of the list (`Tab`). The loop continues as long as `stu_ptr` is different from zero (that is, it is not a null pointer). Inside the loop, the desired information (e.g. the student ID) of the current element is accessed and printed (`stu_ptr->stud.id`). At the end of each iteration, the pointer `stu_ptr` is updated to the value of its field `next_ptr` (`stu_ptr = stu_ptr->next_ptr`), thus moving to the next element. The loop ends when the end of the list is reached (the pointer becomes null).

---

## Test Strategy for List Management

A complete test plan is outlined to verify the correctness of the list management program, covering all the significant logical cases of insertion and deletion.

**Key Points:**
- Testing the program in all the cases considered logically different is crucial to have confidence in its correctness
- The cases to cover include operations on an empty list, insertion/deletion at the head, at the tail and in intermediate positions
- It is also important to test boundary cases, such as the insertion of a duplicate or the deletion of a non-existent element

**Example:**
It starts from an empty list and insertion and deletion operations are executed in sequence to test all the functionalities of the program in different scenarios.

**Calculation Steps:**
- Start with an empty class
- Insertion of the student with ID 7 (test of insertion in an empty list)
- Insertion of the student with ID 5 (test of insertion at the head of a non-empty list)
- Insertion of the student with ID 84 (test of insertion at the tail)
- Insertion of the student with ID 63 (test of insertion in an intermediate position)
- Attempt to insert an already existing ID, 7 (the program must not insert the element)
- Deletion of ID 63 (test of deletion from an intermediate position)
- Deletion of ID 84 (test of deletion from the tail)
- Attempt to delete a non-existent ID, 28 (the table must not change)
- Deletion of ID 5 (test of deletion from the head)
- Deletion of the only remaining element, ID 7 (the table becomes empty again)
- Attempt to delete from the empty table, ID 43 (the program must do nothing)
- End of the operations

---

## Environment Model for Program Execution

Introduction to the use of the "environment model" to visualize and understand the semantics of program execution, with a focus on the dynamic allocation and deallocation of memory and on the handling of variables and pointers.

**Key Points:**
- Each function call creates a new local "environment" for its variables
- Pointer variables initialized to 0 (or null) indicate the absence of an object to point to
- The environment model helps to trace the execution flow, parameter passing and return values between functions
- This model is particularly useful to understand dynamic memory management with `new` and `delete`

**Explanation:**
The execution of the program starts with the allocation of the global environment. When `main` is called, its local environment is created with its variables (`operation`, `class`, etc.). The first statement is the initialization of the variable `class` through the call of the function `initialize_table`. This call creates a new environment for the function, which executes its single statement `return 0`. The value 0 is returned to the environment of `main` and assigned to `class`, which now represents an empty list (null pointer). Subsequently, `print_table` is called, creating another environment in which the parameter `Tab` refers to `class`. Since `Tab` is 0, the print loop is not executed, which is the correct behavior for an empty table.

---

## Dynamic Memory Allocation and the Global Environment

The objects created dynamically with `new` (e.g. `temp = new node`) must be allocated in the global environment (heap). This is essential because the data in the local environment of a function are deallocated at the end of its execution. If the nodes of the list were local, they would be destroyed on return from the insertion function, losing the changes to the table.

**Key Points:**
- The objects created with `new` are allocated in the heap (global environment)
- Local variables are allocated in the stack (local environment) and are temporary
- The persistence of dynamic objects is crucial to modify data structures such as linked lists across different function calls
- Access to dynamic objects happens exclusively through pointers

**Explanation:**
When a function is called, its local environment is created. Local variables are created and destroyed with the function. The objects created with `new`, instead, persist until they are explicitly destroyed. They are referred to only through pointers. This mechanism allows insertion and deletion operations to have permanent effects on the main data structure (the list `class` in `main`).

---

## Insertion Logic in an Ordered List

The insertion of a new student in a list ordered by student ID requires first finding the correct position. The function `search_if_exists_and_position` determines whether the student ID already exists and, if not, returns the position of the node that must precede the new one. The insertion handles several cases: empty list, insertion at the head, at the tail or in an intermediate position.

**Explanation:**
1. `search_if_exists_and_position` is called passing the student ID of the new student
2. The function scans the list comparing the student IDs
3. It returns `exists = false` and the position (pointer to the previous node) if the element is not there
4. The function `insert_if_not_exists` checks the flag `exists`. If it is false:
   - a. It creates a new node (`temp = new node`)
   - b. It links the new node by updating the `next_ptr` pointers: `temp->next_ptr` points to the successor of the node in `position`, and `position->next_ptr` points to `temp`
   - c. It handles the special cases in which `position` is 0 (insertion at the head) or points to the last element (insertion at the tail)

**Example 1 (empty list):**
The program tries to insert the student with ID 7. The list `class` is initially empty (`Tab` is 0).

**Calculation Steps:**
- `search_if_exists_and_position` is called. Since `Tab` is 0, the function sets `exists` to false and `POS` to 0
- `insert_if_not_exists` verifies that `exists` is false
- It creates a new node (`temp = new node`)
- Since `position` is 0, `temp->next_ptr` is set to `Tab` (which is 0)
- `Tab` (that is, `class`) is set to `temp`, making the new node the first and only element of the list
- The student data (ID 7, surname, first name, etc.) are copied into the new node

**Example 2 (insertion at the head):**
The list already contains the student with ID 7. The student with ID 5 is to be inserted.

**Calculation Steps:**
- `search_if_exists_and_position` detects that 5 is less than 7 (the ID of the first element), so it returns `exists = false` and `position = 0`
- `insert_if_not_exists` creates a new node for ID 5
- `temp->next_ptr` is set to the current value of `Tab` (the pointer to node 7)
- `Tab` (that is, `class`) is updated to point to `temp` (the new node with ID 5)
- The list is now: 5 → 7

**Example 3 (insertion at the tail):**
The list contains students 5 and 7. The student with ID 84 is to be inserted.

**Calculation Steps:**
- `search_if_exists_and_position` scrolls the list. It passes 5, then reaches 7. It sees that 7 has no successors (`next_ptr` is null)
- The function concludes that 84 does not exist and must be inserted after 7. It returns `exists = false` and `position` pointing to node 7
- `insert_if_not_exists` creates a new node for ID 84
- `temp->next_ptr` is set to `position->next_ptr` (which is 0)
- `position->next_ptr` (that is, `node_7->next_ptr`) is set to `temp`
- The list is now: 5 → 7 → 84

**Example 4 (insertion in an intermediate position):**
The list contains 5, 7, 84. The student with ID 63 is to be inserted.

**Calculation Steps:**
- `search_if_exists_and_position` scrolls the list. It passes 5. It reaches 7 and sees that its successor (84) has an ID greater than 63
- It concludes that 63 goes after 7. It returns `exists = false` and `position` pointing to node 7
- `insert_if_not_exists` creates a new node for ID 63
- `temp->next_ptr` is set to `position->next_ptr` (the pointer to node 84)
- `position->next_ptr` (that is, `node_7->next_ptr`) is set to `temp`
- The list is now: 5 → 7 → 63 → 84

**Example 5 (duplicate):**
The list already contains a student with ID 7. The user tries to insert another with the same ID.

**Calculation Steps:**
- `search_if_exists_and_position` finds that the element with ID 7 already exists
- The function sets the flag `exists` to true and returns
- In the function `insert_if_not_exists`, the condition `if (exists == false)` is not satisfied
- The insertion is skipped and the function ends without modifying the list

---

## Handling User Input and Potential Errors

The program reads the user's operation (e.g. "i" for insertion) in a loop. Incorrect input can lead to unexpected behavior. For example, entering "63" instead of "i" makes the program read first "6" and then "3" as separate commands, neither of which is valid, requiring the user to re-enter the command.

**Special Circumstances:**
- If the user enters a string of several characters (e.g. "63") instead of a single command character ("i", "e", "f"), how should it be handled? The program, using `cin` on a `char`, reads one character at a time from the input buffer. It reads "6", processes it as an invalid command, then reads "3", processes it as an invalid command, and only then waits for new input from the user

---

## Tasks and Suggestions

- The next step will be to examine, with the usual environment model, what happens during the execution of a program in which spaces in memory are allocated dynamically
- Represent with pen and paper what happens during the execution of the last cases of insertion and deletion (deletion of IDs 63, 28, 7, 43) up to the end of the program
