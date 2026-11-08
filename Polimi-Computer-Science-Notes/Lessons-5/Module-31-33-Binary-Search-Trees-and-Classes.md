# Modules 31-33: Binary Search Trees and Classes in C++

## Topic Overview

The lesson of 2025-11-04 explores both the data structures used to represent tables of students (a "warehouse" array, pointer-based lists, binary search trees) and the introduction of classes in C++ as a tool for encapsulation and access control. Sequential and binary search on sorted arrays are compared, and the BST (Binary Search Tree) is presented as a compromise that combines efficient lookups with local insertions/deletions. The object-oriented part shows how to model the table as a tree through two classes, `TreeNode` (node) and `Tree` (overall structure), highlighting constructors, member functions, friend classes, scope (`::`) and a recursive approach to "insert if not exists". Search, insertion and deletion procedures in the BST are discussed (leaf, one child, two children with replacement by the maximum of the smaller values or the minimum of the larger ones), as well as the problems of unbalancing and strategies for maintaining/rebalancing, in-order printing functions and graphical representations. Classes guarantee consistency of state, code reuse and cost reduction, preventing direct manipulation of the internal representation.

---

## 1. Representations of Tables: "Warehouse" Array vs. Pointer Lists

### Pre-sized array (warehouse)

- **Structure:** array with maximum capacity, with the "full" part at the low indices and an "empty" part for future insertions; a field indicates the boundary between full and empty
- **Pros/Cons:** quick lookup (especially if sorted); requires sizing in advance and has insertion/deletion costs due to physical shifts (on average about half the array)

### Pointer lists (dynamic creation)

- **Structure:** dynamic nodes linked through pointers; each node points to the next one
- **Pros/Cons:** local and efficient insertions/deletions; search is typically sequential and slower

---

## 2. Sequential Search vs. Binary Search in Sorted Arrays

- **Sequential search:** linear scan; does not exploit the ordering
- **Binary search:** on a sorted array, it consults the median element and iteratively halves the search space; logarithmic complexity; not applicable to pointer lists because of the lack of random access

---

## 3. Binary Search Trees (BST) as a Combination of Advantages

### Concept and structure

- The binary tree materializes the logic of binary search: the root is pointed to by the table variable; each node has up to two children (left/right); nodes without children are leaves

### Search in the BST

- Start from the root comparing the key; go down to the left if smaller, to the right if greater, until the key is found or an empty subtree is reached

### Insertion in the BST

- It takes place as a leaf in the appropriate subtree after verifying the absence of the key

### Deletion in the BST

- **Leaf:** it is detached from the parent
- **Only one child:** short-circuit, linking the parent to the child
- **Two children:** the value is replaced with the maximum of the smaller ones or the minimum of the larger ones, then the moved node is deleted, preserving the ordering

---

## 4. Tree Balancing and Impact on Performance

- **Problem:** ordered insertions can generate a degenerate tree similar to a list, degrading the search to sequential
- **Management:** maintain a reasonable balance in insertion/deletion or perform periodic rebalancing depending on the operating load

---

## 5. Fundamental Concepts of Classes in C++

### Classes and OOP

- The class allows defining new types with data and functions; it enables reuse and cost reduction

### Encapsulation and access

- Private data (`private`); operations through public methods (`public`); it prevents corruption of the state

### Stability and consistency

- Operations are correct only if the structure remains consistent; avoid direct modifications of the internal data

### Differences from struct/record

- The class extends the record by also including the operating functions

---

## 6. Modeling the Table as a Binary Tree with Classes

### Class `Tree` (table)

- **Representation:** private `rootPTR` (pointer to the root)
- **Constructor:** initializes `rootPTR = 0` (empty tree)
- **Functions:** public `insertIfNotExists`, which invokes the private `insertWithRecursion` with a reference to a pointer to modify the root/subtrees; traversals and printing (in-order, rotated graphical view)

### Class `TreeNode` (node)

- **Private members:** `studData` (Student), `leftPTR`, `rightPTR` (pointers to `TreeNode`)
- **Constructor:** takes `newStudent`, sets `studData` and zeroes the pointers
- **Scope and resolution:** definitions outside the class with the `::` operator (e.g. `TreeNode::getData`)
- **Friend class:** declare `friend class Tree` in `TreeNode` for direct access by `Tree` to the private members

---

## 7. Recursive "Insert If Not Exists"

### Strategy

- **Base case:** root/subtree null → create a new `TreeNode` and link it
- **Recursion:** comparison on student ID; descent to the left or right; if duplicate, do not insert and report it

### Parameterization

- The private function accepts `TreeNode*&` (reference to a pointer to the root of the subtree) and a `Student` object; this allows the pointers to be updated in place

### Continuity with the version without classes

- The recursive logic remains equivalent; what changes is the construction of the nodes through the class constructor

---

## 8. Related Operations with Recursion

- **Ordered printing:** in-order visit (left, root, right) produces increasing student IDs
- **Graphical representations:** rotated view (tree lying on its side) and optionally by levels

---

## 9. Use and Operational Safety with Classes

- Classes impose controlled access and protect the internal representation, avoiding fragile dependencies on self-discipline and facilitating reuse in different projects

---

## Tasks

1. Implement the node structure `TreeNode` with private members: `studData` (Student), `leftPTR` and `rightPTR`; define the constructor that initializes data and pointers to 0
2. Declare `friend class Tree` inside `TreeNode` to allow access to the private members from the class `Tree`
3. Define the class `Tree` with private `rootPTR` and the constructor that initializes `rootPTR = 0`
4. Implement the public function `Tree::insertIfNotExists(Student)` that invokes the private service function `insertWithRecursion(TreeNode*&, Student)`
5. Write `insertWithRecursion` with logic: base case (null root → `new TreeNode(newStudent)`), descent left/right based on the student ID, handling of duplicates with a message to the user
6. Implement the search in the BST: comparison from the root and descent left/right; return existence and, if useful, a trace of the path
7. Implement printing in increasing order (in-order visit) and a graphical representation rotated by 90°; optionally printing by levels
8. Implement the deletion procedures: leaf, one child (short-circuit), two children (replacement with the maximum of the smaller ones or the minimum of the larger ones and deletion of the moved node)
9. Prepare a `main` that declares a `Tree` object `class`, inserts several students and verifies the ordering and the correct behavior of the methods
10. Document the impact of unbalancing (e.g. increasing insertions) and choose a strategy: maintaining the balance during insertion/deletion or periodic rebalancing
