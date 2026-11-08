# Modules 34-36: The Tree Class, Traversals and Operator Overloading

## Topic Overview

The lessons of 2025-11-10 present, progressively and conclusively, the adoption of a class `Tree` to represent a table as a binary search tree, replacing the earlier representations (the "warehouse" array and the linear pointer list). They clarify the automatic initialization of the object through the constructor (`rootPTR = 0`, empty tree), the call semantics of methods with the implicit variable `this`, and the insertion flow starting from a `main` that declares a local object `class` of type `Tree` and invokes the member insertion function passing `newStudent`.

The central part details insertion in a BST through the member functions `insertIfNotExists` and `insertWithRecursion`, with passing by reference of the pointers to the fields of the tree (`rootPTR`/`leftPTR`/`rightPTR`) and allocation of new `TreeNode` nodes that initialize the fields `studData` and the left/right pointers. It introduces traversal and in-order printing (increasing order), the comparison between an iterative solution with an explicit stack and recursion (`recursiveInOrder`), as well as other traversals (pre-order, post-order) and the printing of the "overturned" tree (rotated by 90°) with indentation handling.

The concluding lesson extends the concepts of classes in C++: encapsulation (`private`/`public`), abstract data types, overloading of functions and constructors (including the copy constructor), operator overloading (`+`, `=`) as member functions, and I/O operators (`<<`, `>>`) implemented as non-member friend functions to enable chaining on `ostream`/`istream`. It is shown how classes allow creating domain-oriented libraries (e.g. matrices with sum, product, determinant) and students are encouraged to continue their studies.

---

## 1. Program Structure and Data Representations

### Previous and current representations

- From the "warehouse" array and the linear pointer list to the representation as a `Tree` object that encapsulates the logic of the tree

### `Tree` object in `main`

- Declaration of a local variable `class` of type `Tree` in `main`
- The object has a field `rootPTR` (pointer to `TreeNode`) initialized by the constructor

### Declaration dependencies

- `TreeNode` must be declared before `Tree`; the class `Tree` must precede `main` in the file

---

## 2. Execution Flow and Initialization of the `Tree` Object

### Automatic activation of the constructor

- When the object is created, the `Tree` constructor activates automatically on the specific instance

### Implicit variable `this`

- Every method has an implicit pointer to the object, to access its internal state

### Initialization of `rootPTR`

- The constructor assigns `rootPTR = 0`, making the object an empty tree; once the activation is finished, the environment of the function is removed

---

## 3. Managing Operations in `main` (Insertion and Loop)

### Available operations and loop

- Only the operations "insert" and "end" are handled; exit from the loop on "end"

### Acquisition and passing of data

- `main` collects `newStudent` (focus on the key "student ID") and calls the member insertion function on the object `class`

### Printing and simplifications

- The prints are initially omitted to focus on the insertion

### Removal of an unused constant

- The constant "delete" is removed because it is not used in the current flow

---

## 4. Insertion in a Binary Search Tree Through Member Functions

### `insertIfNotExists`: flow and parameters

- Call on `class` with actual parameter `newStudent`; in the environment of the method: `this` → `class`, `newStudent` by value

### Delegation to `insertWithRecursion`

- Recursive method with two parameters: `PTR` by reference (pointer field of the tree/subtree) and `newStudent` by value
- Passing by reference allows `rootPTR`/`leftPTR`/`rightPTR` to be updated directly

### Base case: empty tree

- If `PTR` is null, `new TreeNode(newStudent)` is allocated; the constructor copies `studData` and sets `leftPTR`/`rightPTR = 0`; the pointer is assigned to the field passed by reference

### Recursive case: comparison and descent

- Comparison on `studData.id`; descent to the left/right passing by reference `&node->leftPTR` or `&node->rightPTR`; creation of the node if the subtree is null

---

## 5. Printing and Traversals of the Tree

### In-order (increasing order)

- Recursive function: visit left, print root, visit right; the recursion creates an implicit LIFO stack of environments
- Comparison with the iterative solution that uses an explicit stack to go back up and continue in the right subtree

### Pre-order and post-order

- **Pre-order:** root, left, right
- **Post-order:** left, right, root

### "Overturned" printing (rotated by 90°)

- Visit right, print root, visit left with an indentation parameter; choice of starting column and increment (e.g. initial indent = 10, `incr_indent` = 3) and fixed width of 3 characters for alignment

---

## 6. Environment Model and Semantics of Functions/Methods

### Execution environments and objects

- Objects can be declared as variables or created dynamically; upon activation of the methods a local environment is created with `this` pointing to the instance

### Automatic initialization

- The initialization of the table is no longer an explicit call: the constructor of `Tree` handles it

---

## 7. C++ Classes: Encapsulation, ADT and Overloading

### Encapsulation and ADT

- Public interfaces and private internal representation; the user uses member functions without accessing the implementation, favoring consistency and maintainability

### Overloading of functions and constructors

- Overloading based on the signature; multiple constructors including the copy constructor and custom constructors (e.g. from an array of `Student`)

### Operator overloading as member functions

- `operator+` to merge two `Tree`: call `class1.operator+(class2)`; `operator=` for consistent assignment

### `operator<<` and `operator>>` as friend functions

- Non-member "friend" functions to access private parts and enable `cout << object`; signature with `ostream&`/`istream&` and return of a reference for chaining

---

## 8. Libraries and Language Extension Through Classes

### Application view

- Classes enable domain-oriented libraries (e.g. matrices with sum, product, determinant)
- Expressive syntax through overloaded operators, improving clarity and reuse

---

## Tasks

- Update `main` to use the object of type `Tree`, handling the operations "insert" and "end"
- Implement/link `insertIfNotExists` and `insertWithRecursion` in the class `Tree` with passing by reference of the pointers and creation of `TreeNode` that initializes `studData` and left/right = 0
- Correctly declare and include `TreeNode` and `Tree` before `main` in the program file
- Verify the automatic initialization of the object `class` through the constructor: `rootPTR` must be 0 (empty tree)
- Write `recursiveInOrder(PTR)` and the member function `inOrderTraversal` that calls it on `rootPTR`; test the output (e.g. "10 13 18 28 30 40")
- Implement an iterative (non-recursive) version of the in-order with an explicit stack (array or dynamic list)
- Define `printOverturnedTree` and `printOverturnedRecursive(PTR, indent)`: visit right, print root, visit left; initial indent (e.g. 10), `incr_indent` (e.g. 3), fixed width 3 characters
- Design the class `Tree` with encapsulation, public functions and private representation; define multiple constructors (including copy)
- Overload `operator+` and `operator=` in `Tree`; define `operator<<` as a friend function that returns `ostream&` and consider `operator>>` for reading
- Integrate any print operations after the insertion, once the basic flow has been tested
- Remove the constant "delete" from the code since it is not used
- Design a class library for matrices with sum, product and determinant operations, using operator overloading for a natural syntax
