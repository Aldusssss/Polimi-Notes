# Modules 16-19: Character Parsing, Arrays and Output Formatting

## Topic Overview

Character parsing, C/C++ arrays and I/O formatting. The lessons cover data-driven design to transform free-form input of first name and surname into a structured output, handling spaces and terminators. They cover do-while loops, auxiliary functions, properties of the `cin` stream and `iomanip`, the use of one- and two-dimensional arrays, and tabular formatting. The second part introduces a price analysis program with fixed-size arrays, averages, deviations and a split by zone (center/suburbs).

---

## Key Points Summary

1. Transformation of a sequence of characters: from "first name surname." to "surname initial."
2. Importance of designing the program to reflect the structure of the input and output data
3. Free input data format: handling one or more spaces between first name and surname and leading spaces
4. Use of a terminator (a "stopper") to indicate the end of the sequence of characters: choice of "." as a value of type character
5. Acquisition of the data in a single entry by the user: first name, surname and period
6. Strategy: store only the initial of the first name, then output the surname, then the initial
7. Character-by-character scanning with a variable `character` and reading from `cin`
8. Skipping the leading spaces up to the first significant character of the name
9. Storing the initial of the first name in a separate variable `initial`
10. Scanning and skipping the rest of the name up to the first space

**Key Quotes:**
> "We are completely free to change the input terminator, but the rules by which we indicate the initial of the first name always require a period at the end."

> "The trick is therefore to manage, through the concept of the array, to use the same notation for all these elements, and this allows me to use the loop."

> "With a clear and complete definition of the function headers it will be possible to divide the development work of the whole program among several people in a working group."

---

## Data-Driven Design: Mapping the Structure of the Input Data onto the Output

The design of the program starts from the comparison between the structure of the input data (a sequence of characters containing first name, spaces, surname and terminator) and the structure of the output results (surname, space, initial, period). The organization of the code directly reflects the way the data must be interpreted and transformed.

**Key Points:**
- Input as a sequence of characters, not as already separated tokens
- Output as a structured sequence: "surname initial."
- Modular design: sub-problems for skipping spaces, storing the initial, scanning the surname
- Adoption of final-condition loops to guarantee at least one read
- Separation of responsibilities between acquisition, processing and formatting

**Explanation:**
The instructor stresses that the program arises from comparing the structure of the starting data with the structure of the results. The steps are: 1) acquire all the characters typed by the user (first name, spaces, surname, period), 2) isolate the first significant character of the first name (skipping the leading spaces), 3) store that character as `initial`, 4) skip the rest of the first name up to the space, 5) skip all the spaces between first name and surname, 6) read and write the surname up to the terminator, 7) add a space and the initial followed by a period.

**Example:**
Data typed: "  Luigi   Rossi." with multiple leading spaces and between first name and surname. The program: skips the leading spaces, reads "L" and stores it in `initial`; scans "u", "i", "g", "i" up to the first space; skips all the spaces between first name and surname; outputs "R", then acquires the following characters "o", "s", "s", "i" and writes them; when it reads the ".", it ends the writing of the surname; writes " " and then "L" and then ".". Output: "Rossi L."

**Calculation Steps:**
- Character-by-character acquisition with the variable `character`
- First do-while loop: as long as `character == ' '`, extract a character from `cin`
- Storage `initial` = first non-space character ("L")
- Second do-while loop: extract the characters of the first name until `character != ' '`
- Third do-while loop: skip the spaces between first name and surname while `character == ' '`
- Fourth loop: write `character` (already the first of the surname), then extract and write the following ones until `character != '.'`
- Write " " + `initial` + "." as the final output

**Considerations:**
- Make the input data format as free as possible (one or more spaces, leading spaces)
- Clearly define and document the terminator of the sequence ("." by default)
- Store only the initial of the first name to minimize the state needed
- Use final-condition loops (do-while) to guarantee at least one read of the character
- Explicitly handle the spaces and prevent `cin` from skipping them automatically when needed
- Factor the repeated code into a function `skipSpaces`
- Assess the use of global variables vs. parameter passing for auxiliary functions
- Provide for the possibility of configuring the stopper/terminator at runtime
- Inform the user of the exact format required with an input message (`cout`)

**Special Circumstances:**
- If the first name or surname contains internal spaces (compound names), how should it be handled? Clearly define the rules or limit the input to cases without internal spaces in the tokens
- If the user does not enter the terminator ".", how should it be handled? Insert an error check and ask for re-entry, or consider the end of line as an alternative terminator only if specified
- If the first significant character is not alphabetic (e.g. symbols), how should it be handled? Validate the characters and request correction if out of domain
- If there are only spaces and then the terminator (no first name/surname), how should it be handled? Report invalid input and repeat the acquisition
- If the user wants a different terminator, how should it be handled? Allow reading the terminator at the start of the program as a variable and use it in place of "."

---

## Handling Spaces and Terminators in Character Scanning

Spaces can be multiple and present at various points. A terminator (period) is used to mark the end of the surname. The scanning is done with variables of type character, preventing the standard input from treating spaces as implicit separators.

**Key Points:**
- **Leading spaces:** skipped up to the first character of the first name
- **Spaces between first name and surname:** skipped as a block, any number
- **Terminator as a constant of type `char`:** enclosed between single quotes, "." by default
- Strings enclosed between double quotes; distinction between `char` and `string`
- Possibility of replacing the terminator with other characters ("-", "/", etc.) by changing the constant or reading it from input

**Explanation:**
The program must treat spaces as ordinary characters. For this reason the input stream is instructed not to skip them automatically. The terminator is handled as a `char` with single quotes, clearly distinguishing it from the use of strings. The choice of a configurable "stopper" allows flexibility: it can be promoted to a variable and its value read at startup.

**Example:**
At the start of the program the user enters the terminator character (example: "/"). The code uses the variable `stopper` instead of a constant. During the scanning of the surname, the loop continues while `character != stopper`. If the user chose "/", the string "Rossi/" will produce "Rossi L." with "/" not included in the output.

**Calculation Steps:**
- Define `stopper` as a variable of type `char`
- Read `stopper` from input before the first name/surname acquisition phase
- In the surname-writing loop, continuation condition: `character != stopper`
- Unchanged output formatting: surname + space + initial + "."

**Considerations:**
- Make sure the input does not treat spaces as implicit separators
- Validate that the terminator is a single character
- Document for the user the expected format and the chosen terminator
- Correctly handle the end of the surname when the terminator is detected

**Special Circumstances:**
- If the user enters several characters as the terminator, how should it be handled? Accept only a single `char` and reject invalid input
- If the terminator also appears inside the surname, how should it be handled? Define rules: either forbid it or consider the first occurrence as the end of the surname

---

## Final-Condition Loops (do-while) in Input Scanning

Final-condition loops guarantee the execution of the body at least once, a useful characteristic when at least one character must be extracted in order to position correctly. They are applied to skipping the leading spaces, skipping the rest of the first name and skipping the spaces between first name and surname.

**Key Points:**
- The body of the loop is executed at least once
- **Applications:** skipping leading spaces, skipping the rest of the first name, skipping spaces between first name and surname
- **Typical conditions:** `character == space` to keep skipping, `character != space` to identify the end of the token
- Semantic advantage: clarity that at least one extraction happens
- Reuse of the same loop scheme for several sub-problems

**Explanation:**
To skip the leading spaces, the loop will extract at least one character; if there were no spaces, it will read the first character of the first name. To skip the rest of the first name, at least the following space will be read (even if the first name had only one character). To handle the spaces between first name and surname, at least one read is performed, then it continues until a non-space character is met.

**Example:**
Variable `character` fed from `cin`. Body: read a new character. Condition: repeat while `character == ' '`. Output: `character` is the first significant (non-space) character.

**Calculation Steps:**
- Initialization: read the first character
- Repetition: continue if it is a space
- Exit from the loop: condition false when `character != ' '`
- Positioning: ready to store or write depending on the phase

**Considerations:**
- Clarity of the control flow and of the exit conditions
- Uniformity of use of the same loop pattern in several phases of the program

**Special Circumstances:**
- If the input ends before a non-space character is found, how should it be handled? Detect EOF and issue an error or request re-entry

---

## Factorization with the `skipSpaces` Function

The code that skips spaces can be encapsulated in a function `skipSpaces`. Two modes: without parameters (global variables) or with parameters/return (more modular).

**Key Points:**
- **Mode without parameters:** uses global variables such as `character` and the constant `space`
- **Mode with parameters:** receives `space` and returns the first significant character
- **Pros and cons:** globals make things easier, but reduce modularity and increase coupling
- **Calls from `main`:** positioning on the first character of the first name and on the first of the surname

**Explanation:**
The function without parameters relies on the global `character` and `space`; it runs the do-while loop and leaves `character` positioned on the first significant character. The version with parameters accepts the value of `space` (if a shared constant name is not used) and returns the non-space character, integrating with `main`, which updates the state.

**Example:**
First call: skip the leading spaces before the first name. Second call: skip the spaces between first name and surname. In both cases, on exit the first significant character is ready for the next phase.

**Calculation Steps:**
- Call 1: position on the first character of the first name
- Call 2: position on the first character of the surname

**Considerations:**
- Reduction of code duplication
- Better maintainability and testability
- Pay attention to the handling of state between the function and `main`

**Special Circumstances:**
- If the use of globals is avoided, how should state be handled? Pass and return the necessary data through parameters and return values

---

## Handling White Space in Input Streams (`cin`) and the "skip white spaces" Property

The property that controls the treatment of white space makes it possible to decide whether spaces are skipped or treated as normal characters. It is normally set to true (spaces are skipped). By disabling it (unset), spaces are read as part of the stream and become significant for the logic of the program. This property does not belong to the standard input/output library, but is made available by the stream manipulation library (IO manipulation), which must be included with `#include`.

**Key Points:**
- "set" sets a property, "unset" removes it
- With "skip white spaces" active, `cin` ignores spaces, tabs and newlines; with "unset" it considers them characters
- Disabling it is useful when the logic must distinguish spaces as separators or content
- The property is not in `iostream` but in the IO manipulation library
- The correct library must be included with `#include` to use advanced manipulators/properties

**Explanation:**
In the context of parsing first names and surnames, one wants to control whether spaces are treated as automatic separators or as characters. Under standard conditions, `cin` skips spaces, which makes it easy to read tokens separated by spaces. However, if one wants to store in full a string that may contain spaces (or have fine control over delimiters), the property that skips spaces must be disabled. This is done through manipulators available in IO manipulation (not in `iostream`). Once disabled, every space is read and can be handled by the application logic, making it possible, for example, to distinguish between first name and surname explicitly or to build strings with preserved spaces.

**Example:**
The goal is to output "Rossi Luigi", placing the full first name after the surname. The logic requires not skipping spaces automatically. By disabling "skip white spaces", the space between "Luigi" and any other tokens is read as a character. It is then possible to iterate over the characters of the first name until the chosen delimiter or a manually controlled space is met.

**Calculation Steps:**
- Determine the initial positioning on the first character of the first name/surname (unchanged from the initial case)
- Disable "skip white spaces" to treat the space as a character
- Read character by character and store in a structure that supports several elements (array or string)
- Rebuild the output as "Surname First name" preserving the characters read

**Considerations:**
- Verify that the correct library (`iomanip`) is included when using manipulators not present in `iostream`
- Test the behavior of `cin` after removing the property: without the declaration on `cin` things might not work correctly
- Explicitly decide the input delimiters (stopper) and do not confuse them with the typographic conventions of the output (the period after the initial)
- Carefully handle irregular input cases (multiple spaces, commas, hyphens as possible terminators)

**Special Circumstances:**
- If the input terminator (stopper) is changed to a hyphen or a comma, how should it proceed? The output convention that requires a period after the initial must stay unchanged; so the period must be inserted explicitly and not deduced from the stopper
- If the input contains multiple spaces or tabs, how should it proceed? By disabling "skip white spaces" all the spacing characters must be handled manually, clearly defining the criteria for separating first name and surname

---

## Why an Explicit Period in the Output Instead of the Input "Stopper"

The "stopper" is a freely chosen value to indicate the end of the sequence of input data (it can be a hyphen, a comma, etc.). The typographic rules for indicating the initial of the first name require that there always be a period at the end. Therefore, in the output the period constant is inserted explicitly, regardless of the value of the input terminator.

**Key Points:**
- The "stopper" is an input convention and can change
- The period after the initial is an output format convention that must not depend on the "stopper"
- Separate the responsibilities: parsing (input) vs. formatting (output)

**Explanation:**
In the design of the I/O flow, the input markers are distinguished from the symbols required by the output format. Even if a different character is chosen to terminate the input, the output formatting must follow established rules. For the initial of the first name, the period must always be present: a constant for the period is therefore used in printing instead of reusing variables tied to the parsing.

**Example:**
One moves from a stopper based on the period to a stopper based on the comma. The output "Rossi L." must still contain the period after the initial. A constant "." is kept in printing and "," is used only to delimit the end of the input data.

**Calculation Steps:**
- Define the input terminator as ","
- In parsing, stop at the comma to close the token
- In printing, always add "." after the initial of the first name

**Considerations:**
- Do not tie the output format to contingent parsing choices
- Clearly define the formatting constants (e.g. ".") in the code

**Special Circumstances:**
- If the stopper coincides with a character that appears in the name (e.g. a hyphen in "Maria-Teresa"), how should it proceed? Choose a stopper that does not conflict with real data or handle escaping/quoting of the data

---

## Introduction to Arrays for Storing Several Elements of the Same Type

To treat different elements in a similar way (e.g. storing the whole first name character by character), it is essential to introduce aggregate variables that contain several elements of the same type: arrays. Moving from scalar variables (a single value) to arrays makes it possible to iterate and store sequences without defining a variable for each character (charOne, charTwo, charThree, ...).

**Key Points:**
- Scalar variables are not suitable for holding complete sequences of characters
- Arrays make it possible to store and access multiple positions with an index
- Iterative structures (loops) operate naturally on arrays
- They avoid the non-scalability of defining charOne, charTwo, charThree, etc.

**Explanation:**
If one wants to place the full first name after the surname, every character of the first name must be read and kept up to the delimiter. Using separate scalar variables for each character, the code becomes unmanageable and non-generalizable. Arrays make it possible to store a sequence of characters in contiguous positions, allowing a loop that reads each character and places it at the current index. This solves the "small problem" highlighted: the second, third, fourth, fifth character cannot be handled elegantly with the same variable; arrays and a progress index are needed.

**Example:**
The first name "Luigi" is read character by character and stored in an array of `char` of adequate size. An index is incremented for each character read up to the delimiter (space or stopper), then the content of the array is placed after the surname to obtain "Rossi Luigi".

**Calculation Steps:**
- Initialize an array of `char` and an index at 0
- Cyclically read characters from `cin`
- Insert each character in the array and increment the index
- End at the delimiter; add a string terminator if necessary
- Print "Surname" followed by the space and the content of the array

**Considerations:**
- Correctly size the array for the maximum number of characters expected
- Handle array overflow and the string terminator if C-strings are used
- Clearly define the stop condition of the loop (delimiter)

**Special Circumstances:**
- If the first name exceeds the size of the array, how should it proceed? Implement an overflow check and allocate dynamically or truncate with a warning

---

## Distinction Between Initial Positioning and Subsequent Handling of Characters

In the passage from the initial alone to the whole first name, the positioning on the first character does not change. What changes is the strategy for storing and handling the following characters: the rest can no longer be skipped up to the space, but must be kept in full.

**Key Points:**
- Initial positioning unchanged from the case of the initial
- The handling changes: every character is kept instead of skipping up to the space
- A data structure and an appropriate loop are needed

**Explanation:**
The parser that previously read one character and then skipped the following ones up to the space must be rewritten to store everything. This implies preparing a buffer (array) and a clear termination logic.

**Example:**
The same logic for locating the first character of the first name is kept, but the phase of collecting the characters changes: instead of ignoring them up to the space, they are all stored and printed after the surname.

**Calculation Steps:**
- Locate the first character of the first name
- Acquire all the following characters up to the delimiter
- Print the full surname and first name

**Considerations:**
- Do not confuse the entry point of the parsing with the storage policy
- Verify cases with compound names or multiple spaces

---

## Arrays in C/C++ for Handling Sequences of Characters

Arrays are complex variables that aggregate simple values of the same type. In C/C++ the elements are indexed by an integer that starts from 0. To store sequences of characters (e.g. names), an array of `char` of a predetermined size is defined through a constant, and access is managed with a variable index.

**Key Points:**
- The elements of an array must all be of the same type
- In C/C++ indexing starts from 0: the first element has index 0, the last has index size−1
- The definition of an array includes the type of the elements and the size between square brackets
- Use of a constant (e.g. `long Max`) to fix the size; in the case in question `long Max = 20`
- Replacement of many simple variables with one array variable and an index to select the position
- The index can be an expression, typically a variable (i, j)

**Explanation:**
The instructor highlights that with simple variables only, a reusable loop body for storing successive characters cannot be created: one ends up with a sequence of statements (car1, car2, car3...) that does not scale. The array-type variable (e.g. `name[]`) is introduced, representing an aggregate of homogeneous elements (`char`). The size is defined with a constant `long Max = 20` (integer), which indicates that up to 20 characters can be stored for the name. Arrays in C/C++ are indexed from 0: `name[0]` is the first character, `name[19]` the last if the size is 20. An index variable `i`, initialized to 0, is used, and the characters are stored via `name[i] = character;` after each insertion `i` is incremented to move to the next position. Reading and storing continue as long as the character read is different from a space (end of the name).

**Example:**
An integer constant `long Max` with value 20 is declared. The array `name` is defined with type `char` and size `Max`. The elements are `name[0] .. name[19]`.

Initialize `i = 0`, assign `name[i] = character`, increment `i` with `i++`. Repeat until the character is different from a space to store the whole name.

**Considerations:**
- Make sure the size of the array (`Max`) is sufficient for the expected names; if not, change the constant
- Arrays must have homogeneous elements; for strings of characters, use `char`
- Correctly handle indexing from 0 to avoid off-by-one errors
- Keep `i` as both the count of the characters stored and the first free position
- Provide for the case of names longer than the size of the array: define a strategy (truncation or error)

**Special Circumstances:**
- If names longer than 20 characters are encountered, how should it be handled? Increase `Max` or implement a check that interrupts reading and signals overflow

---

## Using Loops to Read and Write Sequences: while, do-while, for

Loops make it possible to repeatedly handle operations on array elements and on input/output streams. The `for` loop is suited to scanning an array with a known index; `while`/`do-while` handle sequential reading based on conditions (e.g. up to a space or terminator).

**Key Points:**
- The `for` loop with index `j` from 0 to `i − 1` prints the characters stored in the name
- The semantics of `for`: initialization, condition, body, update
- Loop for reading the first name: repeat storing and incrementing the index until a character different from a space
- Loop to skip spaces between first name and surname: repeat while spaces are met
- Loop to read the surname: read and write characters up to the terminator (stopper/period)

**Explanation:**
The instructor shows how to make the code uniform using a variable index. To print the name, a `for` is used with `j` initially 0, condition `j < i`, and update `j++`. The output for "Luigi" with `i = 5` is illustrated: `name[0] = L`, `name[1] = U`, `name[2] = I`, `name[3] = G`, `name[4] = I`. For the surname, a loop is used that reads and writes until the terminator (period/stopper) is met. Between first name and surname, the spaces are handled with a loop that skips them.

**Example:**
Index `j = 0`; condition `j < i`; increment `j++`. Print `cout << name[j]` for `j = 0..i-1`. With `i = 5`, l, u, i, g, i are obtained in sequence.

After reading the first name, a loop reads the space characters and discards them until it finds a non-space character, positioning the input on the first character of the surname.

**Considerations:**
- Verify the exit condition of the loops to avoid infinite loops
- Make the output formatting uniform (a fixed single space between surname and first name)

**Special Circumstances:**
- If the input has multiple spaces between parts, how should it be handled? Implement a loop that compresses multiple spaces into one in the printing

---

## Output Format and Handling Surnames Made of Several Parts

Surnames can often be made of several parts separated by spaces. The initial program prints all the parts separating them as in the input, leading to multiple spaces. An outer loop is needed that handles each part of the surname and guarantees a single space between the parts and between surname and first name.

**Key Points:**
- A surname made of several parts must be handled by repeating the read/write logic for the single part
- At least one part is present: an outer do-while loop is proposed
- The internal parts of the surname end with a space; the last part ends with the stopper (period)
- Termination condition of the outer surname loop: when the character read at the end of the part is the stopper
- Problem detected: non-uniform separations (e.g. three spaces); compacting to one space is needed

**Explanation:**
The instructor analyzes the case of the surname "Della Vigna" and shows that the program, as it is, can produce three spaces between the parts. He suggests turning the section that handles the surname into a reusable component within an outer do-while loop that repeats the handling of each part. The exit condition of the outer loop is that the character read at the end of the part is the terminator (stopper/period). The other parts are terminated by a space. To avoid multiple spaces, the output must be normalized by imposing a single space as separator.

**Example:**
Each part is read and printed up to the space (for the first part) or up to the stopper (for the last). Between the parts and between surname and first name a single space is emitted as a separator.

**Considerations:**
- Normalize the separators in the output to a single space
- Clearly distinguish the terminators: space between internal parts, stopper for the end of the surname

**Special Circumstances:**
- If the input has three or more spaces between parts of the surname, how should it be handled? Replace sequences of spaces with a single space when printing

---

## Logical Conditions and De Morgan's Theorem Applied to Parsing Loops

To handle the exit from the loops that read a part (first name or surname), it is useful to formulate conditions with logical operators and apply De Morgan to obtain the exit condition. The loop continues while `character` is different from stopper AND different from space; it exits when NOT(...) = (`character == stopper`) OR (`character == space`).

**Key Points:**
- **Condition for staying:** `character != stopper AND character != space`
- **Exit condition:** `character == stopper OR character == space`
- Direct application of De Morgan's theorem: NOT(A AND B) = (NOT A) OR (NOT B)

**Explanation:**
The instructor formalizes the control logic for handling multiple parts. The single part (of the surname or of the first name) continues until neither the final terminator (stopper/period) nor a separator space appears. When one of the two appears, the current part ends and control passes to the handling of the separator (space) or of the end of the sequence (stopper).

**Example:**
If the current character is a space, the part ends and the next is prepared; if it is the stopper, the whole surname/first name ends. The exit condition is `character == stopper OR character == space`.

**Considerations:**
- Make the terminators and separators in the input explicit to reduce ambiguity
- Test the boundary cases: absence of a final space, presence of multiple spaces

**Special Circumstances:**
- If non-alphabetic characters appear as separators, how should it be handled? Extend the exit condition to include such characters as additional separators, after specification

---

## Ambiguity Between First Names and Surnames with Several Parts and the Need for an Explicit End-of-Name Terminator

When both the first name and the surname can have several parts, it becomes impossible to determine with certainty where the first name ends and the surname begins without an external rule. An explicit terminator for the end of the first name is needed (e.g. the same stopper used for the whole sequence), or an unambiguous convention.

**Key Points:**
- Impossibility of distinguishing "Pier Luigi" as a first name from "Pierluigi" with surname "Vigna" without rules
- Need to explicitly signal the end of the first name in the input
- Possible reuse of the terminator of the whole sequence as the terminator of the sequence of parts of the first name

**Explanation:**
The instructor presents the case "Pierluigi Della Vigna" and discusses the ambiguity: without metadata or dictionaries, the segmentation cannot be established with certainty. He proposes introducing an explicit terminator for the end of the first name, analogous to the one used for the end of the surname (stopper/period), to make the parsing deterministic.

**Example:**
Use the stopper to indicate the end of the compound first name. The outer loop for the first name is symmetric to the one for the surname: do-while with exit when `character == stopper`.

**Considerations:**
- Define an input protocol that includes end-of-field markers (first name/surname)
- Document the fixed output format to guarantee uniformity

**Special Circumstances:**
- If the input has no end-of-first-name terminator, how should it be handled? Request the specification or assume a predefined convention, flagging the ambiguity

---

## Handling Compound Names with One-Dimensional Arrays

When several parts of the name are stored in a single array of characters, the write index `i` must be initialized outside the inner loop and kept across iterations to avoid overwriting the previous parts. The parts must be separated by a space and the input ends with a "stopper" (sentinel).

**Key Points:**
- Typical error: `i` initialized inside the outer loop causes a restart from index 0 and overwriting (example: Pierre skipped and only "Luigi" or "Filippo" remains)
- Solution: initialize `i` outside the loop handling the whole compound name (one-dimensional array)
- Insert a space after each part of the name, except the last
- User guide: enter first name and surname in succession, each followed by the "stopper", parts separated by one or more spaces
- Use of do-while with a condition for staying that includes the check of the character being different from the "stopper"

**Explanation:**
The program reads part by part, skips the leading spaces (`skipSpaces`), copies the part into the same array `name`, keeping an index `i` that keeps growing. After each part, a space is added to separate the parts. Staying in the do-while loop depends both on the end of input and on the check that the character is different from the "stopper". By initializing `i` outside, the following parts do not overwrite the previous ones. The output of the compound surname includes a trailing space, so there is no need to add it before writing the first name.

**Example:**
In execution, the program prints "della vigna Luigi" skipping "Pierre". The reason is that the index `i` is re-initialized to 0 inside the outermost loop, so with each new part of the name the previously stored part in the array `name` is overwritten. If the user were called "Pierluigi Filippo", the final result would be only "Filippo".

**Calculation Steps:**
- Cause: `i` re-initialized inside the outer loop
- Effect: overwriting starting from index 0
- Fix: initialization of `i` outside the loop that handles the compound name
- Add spaces between the parts of the name for visual separation

**Considerations:**
- Clarify to the user how to enter the data: parts of the first name/surname each followed by the "stopper", parts separated by one or more spaces
- The "stopper" is a modifiable constant that defines the end of the input
- Correctly handle the condition for staying in the do-while loop, including the check against the "stopper"

---

## Handling Compound Names with Two-Dimensional Arrays

The parts of the name can be stored in different rows of a two-dimensional array, where each row is an array of characters (one part of the name) and each column a character. The maximum sizes are defined through constants and the current row is selected with an index `POS`.

**Key Points:**
- Two-dimensional array: first dimension number of parts, second dimension maximum length of the part
- Example: `parts_n = 10`, `lumax = 20`; `char name[parts_n][lumax]`
- Each row represents a part: "Pier", "Luigi", "Filippo" stored in distinct rows
- `POS` initialized to 0 at the entry of the loop handling the compound name; incremented after each part
- The index `i` becomes local to the current row (`name[POS]`), initialized to 0 for each new part

**Explanation:**
The constants `parts_n = 10` and `lumax = 20` are defined for the dimensions of the array. The variable `POS` identifies the row of the array of arrays where the current part is stored. For each part, `i = 0` is initialized and the characters are written to `name[POS][i]`, then the part is ended. At the end of each part `POS` is incremented to move to the next row.

**Example:**
`const int parts_n = 10; const int lumax = 20; char name[parts_n][lumax];` Each row (0..9) is a part of the name, with a maximum of 20 characters. It is filled from row 0 onwards. The index `i` manages the position in the current row `name[POS]`.

**Calculation Steps:**
- `POS = 0` initially
- For each part: `i = 0` and the characters are stored in `name[POS][i]`
- After the part: `POS++` for the next row

**Considerations:**
- Array indices in C/C++ start from 0, fill from the row with the lowest index
- Define reasonable maximum sizes: up to 10 parts, up to 20 characters per part

---

## Tracking the End of the Parts and the First Free Position

To know where the parts end or where the first free index is on each row, two approaches can be used: an auxiliary array of indices for each row or a special "stopper" character such as "$" placed at the end of each part.

**Key Points:**
- **Auxiliary array:** stores for each row the index of the first free position
- **Special character "$"** as an end-of-part sentinel on each row
- **Printing:** iterate K from 0 to `POS − 1` and for each row print up to the character "$"
- **Separation between parts:** emit a space " " between parts in the output

**Explanation:**
Solution 1: use an array of 10 elements (if `parts_n = 10`) that stores for each row the index of the first free character. Solution 2: place "$" at the end of the sequence of characters of the part in `name[POS]`. In printing, it is known that there are `POS` parts, so a `for` on `K = 0..POS−1` and an inner loop on `J` starting from 0 until "$" is met are used. A space is printed between parts. This reproduces the separation seen in the one-dimensional solution.

**Example:**
Since `POS` indicates the first free element (the number of parts stored), the following is used: `for (K = 0; K <= POS - 1; K++) { for J from 0 while name[K][J] != '$' print name[K][J]; then print a space }`

**Calculation Steps:**
- The inner loop ends on "$"
- The space separates the parts for readable output

**Considerations:**
- Choose a sentinel that does not appear in real names (example "$")
- Align `POS` and the number of actual parts to avoid out-of-bounds access

---

## Constraints on Array Sizes in C/C++ and Pascal

In C and C++, as in Pascal, the size of arrays is static and must be defined before the execution of the program, with constant values. Constant identifiers can be used to improve readability and maintainability.

**Key Points:**
- The sizes must be known at compile time
- Example: `lumax = 20`; `char name[lumax]` or `char name[parts_n][lumax]` is declared
- Use of `const int` to define constants (`const int lumax = 20`)

**Explanation:**
Constants are defined with `const int`, for example `const int lumax = 20`, and then used in array declarations. This makes it possible to change the value in a single point and keep consistency. The size must be finite and constant at compile time.

**Example:**
`const int lumax = 20; char name[lumax];` or `const int parts_n = 10; char name[parts_n][lumax];`

**Calculation Steps:**
- Constants guarantee the static sizes required by the language
- They make future changes to the maximum sizes easier

**Considerations:**
- Avoid excessive sizes; choose reasonable limits such as 10 parts and 20 characters per part

---

## Functions and Parameter Passing: Teaching Plan of the Lessons

The first four lessons (on the first CD) cover functions, exchange of information via the global environment and parameter passing, and the use of arrays. The next four lessons introduce a program to analyze the distribution of the price of a product in different shops of an urban area, evolving from an undifferentiated area to two zones and then to several zones, with input of the number and name of the zones. Passing by value and by address, software reuse and division of work through function headers are explored.

**Key Points:**
- First four lessons: functions, global environment, parameter passing, use of arrays
- Next four lessons: price analysis program for a city, from an undifferentiated area to two zones, then several zones with number and names provided by the user
- Introduction of functions with ARRAY-type parameters and the environment model with successive versions of the program
- Third lesson: comparison between passing by value and by address
- Fourth lesson: decomposition into sub-problems, definition of function names and of input/output formal parameters
- Goal: software reuse and improved identifiability of errors
- Division of work made possible by clear headers

**Explanation:**
The teaching path proceeds by successive versions of the price analysis program: initially an undifferentiated area; then two zones handled separately; finally an extension to n zones with user input. In each version new data structures and functions are introduced, including ARRAY-type parameters and the implications of passing by value and by address. In the final phase the sub-problems are identified and the interfaces (headers) of the functions are defined with accurate formal parameters, allowing parallel work among the members of the group.

**Example:**
The program acquires information on the prices of a product in different shops of an area. Version 1: undifferentiated area. Version 2: split into two zones. Version 3: extension to several zones, with the user able to provide the number and names of the zones.

**Calculation Steps:**
- Progressive increase in complexity to motivate the use of functions and parameters
- ARRAY-type parameters introduced with specific considerations

**Considerations:**
- Clear function headers and definition of formal parameters for collaboration
- Highlight when to use passing by address for efficiency or for multiple outputs

---

## Acquiring and Storing Data in C++ with Fixed-Size Arrays

In C++ arrays require a size defined at compile time. To handle a maximum number of readings, a constant (for example `MaxDim`) with value 100 is introduced. The data (prices) entered by the user are stored sequentially in the array `prices` and the counter `num` identifies the first free index, as well as the number of elements acquired.

**Key Points:**
- Definition of `MaxDim = 100`
- Array indices from 0 to `MaxDim − 1`
- Variable `num` used as a counter and insertion index
- **Overflow handling:** when `num` reaches `MaxDim`, subsequent elements are not accepted

**Explanation:**
The program starts with an acquisition loop that reads the prices in euros (integers) from the user. Each price is inserted in `prices[num]` and `num` is incremented. In parallel the total sum of the prices is updated for the later computation of the average. The loop is potentially infinite and ends when the user signals the end with Control-Z (end of file) or when `num` reaches `MaxDim`, a condition that indicates the exhaustion of the space in the array. The specification of the program establishes that more than 100 elements are not accepted, but those already acquired remain valid and will be processed.

**Example:**
The user enters three prices: 80, 90 and 70. The program stores these three values in `prices[0]`, `prices[1]`, `prices[2]`. The variable `num` becomes 3. Since `num = 3 < 100`, there is residual space in the array. The accumulated sum is used for the average. If the user had entered 101 values, the 101st would not have been accepted.

**Considerations:**
- Clearly establish `MaxDim` before compilation
- Inform the user that more than 100 entries will not be accepted
- Correctly update `num` and the total sum during acquisition
- Correctly handle the Control-Z input terminator
- Validate that `num > 0` before proceeding to the output

---

## Computing the Average and the Deviation from the Average

The average of the prices is computed by dividing the sum of the prices by the number of readings (`num`). The deviation for each reading is the difference between the specific price and the average. To appreciate even small deviations, both the average and the deviation are of type `float` with a fractional part.

**Key Points:**
- The average requires all the data acquired
- Deviation for each element: `deviation[i] = prices[i] - average`
- Floating types to represent the fractional part

**Explanation:**
Once the acquisition is finished, it is checked that `num` is different from 0. The average is computed as sum/num, promoting the computation to type `float`. For each `i` from 0 to `num−1`, the deviation is computed as the difference between `prices[i]` and the average. These values are then printed in the table, ensuring a readable format.

**Example:**
Average = (80 + 90 + 70) / 3 = 240 / 3 = 80.0 (float). Deviations: 80 − 80.0 = 0.0; 90 − 80.0 = 10.0; 70 − 80.0 = −10.0. With `showpoint` and `setprecision(2)`, they can be printed as 0.00, 10.00, −10.00.

**Considerations:**
- Make sure the sum is computed correctly and promoted to `float`
- Use sufficient precision to highlight small deviations (e.g. 2 decimals)

---

## Tabular Output Formatting with `iomanip`

The `iomanip` library provides tools to format the output: `setw` (set width) for the width of fields, `setprecision` for the precision of floats, `setf` to set flags such as fixed-point notation and `showpoint`. The table must have a clear header and aligned columns.

**Key Points:**
- Use of `setw` to define field widths: 20 for "prices recorded", 40 for "deviation from the average price"
- Right justification within the field of fixed width
- Use of `setprecision(2)` for two decimal digits
- Setting of fixed-point notation and `showpoint` through `setf`

**Explanation:**
The header is printed with the same field widths used for the data, ensuring alignment of the columns. For each reading, the price (integer) is printed with `setw(20)` and the deviation (float) with `setw(40)`, after setting `setprecision(2)`, `fixed` and `showpoint`. Even when the number has no fractional part, `showpoint` forces the presence of the decimal point and of the decimal digits.

**Example:**
Header: "Prices recorded" with width 20 and "Deviation from the average price" with width 40. Rows: 80 and 0.00; 90 and 10.00; 70 and −10.00. With `setw(20)` for the price and `setw(40)` for the deviation, the columns are right-aligned.

**Considerations:**
- Include the `iomanip` library in the source to use `setw`, `setprecision`, `setf`
- Maintain consistency between the widths of the headers and the data
- Verify the effect of `showpoint` for always displaying the decimal point

---

## Input Flow Control and End-of-File Handling (Control-Z)

Acquisition happens in an infinite loop that ends when the user enters Control-Z, marking the end of the file, or when the array is full (`num == MaxDim`).

**Key Points:**
- Infinite reading loop with well-defined exit conditions
- Control-Z as the end-of-input signal
- Check of `num == MaxDim` to interrupt the insertion

**Explanation:**
During reading, the state of the stream is checked. On receiving Control-Z, the stream indicates end of file and the loop is exited. If `num` reaches 100, no further insertions are accepted. The specification must inform the user of this behavior.

**Example:**
The user enters prices until they decide to end with Control-Z. If they instead continue beyond 100, at `num == 100` the program stops accepting new values, keeping the previous ones.

**Considerations:**
- Provide clear messages for the user on how to end the input
- Correctly handle the state of the stream in case of end of file

---

## Extending the Problem: Splitting the Area into Center and Suburbs

To make the exercise more complex, it is proposed to split the city into two zones (center and suburbs) and to repeat or adapt the analysis for each part.

**Key Points:**
- Geographic segmentation of the data: center and suburbs
- Possible separate analysis of averages and deviations for each zone

**Explanation:**
Once the flow of acquisition, storage and output formatting is understood, a classification of the data by zone can be introduced, making it possible to compute separate averages and deviations for "center" and "suburbs". This requires additional data structures or labeling the prices with the zone they belong to.

**Example:**
Prices are acquired indicating whether they belong to the center or the suburbs. Two averages are computed and two tables with the related deviations are printed. The field widths and the precision remain consistent with the main setup.

**Considerations:**
- Ensure the correct association between price and zone
- Maintain consistent tabular formatting for both tables

---

## Numeric Output Formatting with Flags

The lesson introduces the logic of flags to control the representation of float numbers in the output. Two key concepts: the choice between decimal notation with a point and mantissa+exponent notation; use of the flag to always show the decimal point (`showpoint`) even when there are no decimal digits. This affects the length of the decimal part displayed, which can be filled, for example, with 000000. The discussion refers to the syntax of stream-oriented libraries (hinting at classes and objects to be covered at the end of the course), with examples of settings that determine how 0, 10 and −10 are shown.

**Key Points:**
- Flags can be raised/lowered to configure the formatting
- Choice between decimal point and mantissa+exponent for floats
- `showpoint` flag to always show the decimal point
- With `showpoint` the decimal part appears even if zero (e.g. 000000)
- Without `showpoint` the output is more concise: e.g. 0, 10 and −10 without fraction
- Reference to the syntax of streams and to classes/objects (covered later in the course)

**Explanation:**
It is illustrated that, just as on sailboats one signals by raising/lowering flags, in output streams "flags" are set that govern the format. One flag decides the notation (decimal vs. mantissa/exponent); another imposes the presence of the decimal point. If the flag to show the point is active, decimals are seen even when the data have a null fractional part, producing a string with zeros. If the flag is not active, whole numbers are printed without the fractional part, such as 0, 10, −10.

**Example:**
With `showpoint` active: 10.000000 (or similar with a fixed number of decimal digits). Without `showpoint`: 10.

**Calculation Steps:**
- Set the `showpoint` flag
- Print a float 10
- Observe the difference in the output

---

## Data Design for Zone Analysis (Center/Suburbs)

A specification is defined to analyze prices split into two zones, center and suburbs, computing distinct averages and deviations from the average for each area. The input data arrive in random order. A coding of the zone through the characters "C" and "P" (periferia) is proposed.

**Key Points:**
- **Zone coding:** "C" for center, "P" for suburbs
- Objective: deviations from the averages by zone
- Random input order, no assumption of grouping
- Two presentation modes: grouped by zone vs. in insertion order
- Need for `sumC`, `sumP`, `numC`, `numP` for separate averages

**Explanation:**
The specification requires separating the readings by geographic area. To avoid verbose input, single codes "C"/"P" are adopted. Independent averages and deviations are computed for each zone: separate sums and counts are accumulated. In the output one can choose between grouping by zone or keeping the insertion order.

**Example:**
With three readings: 1st center (C), 2nd suburbs (P), 3rd center (C).

**Calculation Steps:**
- Update `sumC` and `numC` for the 1st and 3rd
- Update `sumP` and `numP` for the 2nd
- Choose the desired presentation mode

---

## Data Structures: Two Separate Arrays vs. a Prices Array + a Zones Array

Two solutions are compared: (1) two separate arrays, `pricesC` and `pricesP`; (2) a single array `prices` and a parallel array `zones` with codes "C"/"P". Sizing, maintaining the order, costs and adaptation to the output specification are analyzed.

**Key Points:**
- Two separate arrays: `pricesC` and `pricesP`; `numC` and `numP` are needed for the significant elements
- Sizing to 100 for both if `MaxDim` is 100, to handle extreme cases
- Cost: possible memory occupation double that of the readings that can be handled
- With two arrays the total ordering between the zones is lost (only the one internal to each zone is kept)
- The prices+zones solution keeps the total ordering and associates a zone to each price
- For grouped printing with prices+zones: double scan filtering by zone
- Variant with 0 as a placeholder in the two arrays to preserve the global order (with complications)

**Explanation:**
If the data must be grouped by zone, two separate arrays work well and allow scanning each group with dedicated loops. However, they do not maintain the order relation between C and P at the global level. The alternative prices+zones preserves the insertion order and allows any presentation, but requires filtered scans to group. The choice depends on the output specification.

**Example:**
If all the readings are from the center, `pricesP` remains unused; if all are from the suburbs, `pricesC` remains unused. Both arrays must nonetheless be sized to 100 to handle the extremes.

**Calculation Steps:**
- Allocate `pricesC[100]` and `pricesP[100]`
- Check overflow for each array during acquisition
- Accept the memory cost as a specification trade-off

**Variant with placeholders:**
Insert 0 in the positions of the array that do not correspond to the zone to preserve the global order; print by alternating reads from `pricesC` and `pricesP` skipping the 0s.

**Calculation Steps:**
- Populate `pricesC` and `pricesP` with 0 as a placeholder
- Scan in parallel, checking for 0 to skip elements
- Print according to the original order

---

## Acquisition, Control and Computation Flow for Output Grouped by Zone

The first solution (two arrays) is adopted. The program provides: initialization of sums and counts, acquisition loop with a request for the zone, handling of end-of-file, capacity check for each array, acquisition of the price, update of the sum and insertion into the appropriate array, then analysis and printing phase for each zone with headers, computation of the average and the deviation.

**Key Points:**
- Character constants: `center='C'`, `suburbs='P'` (single quotes); strings between double quotes
- **Variables:** `zone`, `price`, `pricesC`, `pricesP`, `numC`, `numP`, `sumC`, `sumP`, `i`, `average`, `deviation`
- Infinite acquisition loop, with exit on EOF
- Check: if `zone` is C and `numC` has reached capacity, exit from the loop; similarly for P and `numP`
- If `zone` is valid (C/P), the price is read and `sumC`/`sumP` is updated, it is inserted in `pricesC`/`pricesP` at position `numC`/`numP` and `numC`/`numP` is incremented
- If `zone` is not valid, it is reported to the user and the price is not requested
- Output phase: for each zone with `num > 0`, print the table header with the indication of the zone ("center" or "suburbs"), computation of the average and for each element computation of the deviation and printing
- Reuse of the variable `average`: computed first for the center, then for the suburbs; alternative: use two variables (`averageC`, `averageP`) if one prefers to compute both before printing
- Use of the index `i` to scan both `pricesC` and `pricesP`

**Explanation:**
The program starts the acquisition by asking for the zone of the new reading. If the user signals the end of the data (EOF), the loop ends. For valid C/P inputs, the availability of space in the corresponding array is checked; if full, the loop is exited. Otherwise the price is acquired, the sum is updated and it is inserted in the respective array incrementing the counter. In the output two tables are generated: one for the center and one for the suburbs, with adequate headers, computation of the average and of the deviation from the average for each element. The variable `average` is reused: it is computed and used for the center, then recomputed and used for the suburbs. The index `i` scans the arrays from 0 to `num−1`. The character constants are defined between single quotes; the header strings between double quotes.

**Example:**
During acquisition: if the user enters EOF, the end-of-file function detects it and the program exits from the loop. If `zone='C'` and `numC` reaches `MaxDim`, the program exits from the loop; similarly for `zone='P'` and `numP`.

**Calculation Steps:**
- Ask for the zone
- Check EOF
- Check the capacity of the corresponding array
- Acquire the price and update the structure

---

## Tasks and Suggestions

- Design and implement in C++ a program that reads integer prices entered by the user, stores them in an array `prices` with maximum size 100 (`MaxDim = 100`), computes the average (float) and prints a table with: header, prices recorded (`setw(20)`), deviation from the average (`setw(40)`, `fixed`, `showpoint`, `setprecision(2)`). Handle the input with an infinite loop interrupted by Control-Z or by `num == MaxDim`.
- Extend the program to split the data between "center" and "suburbs", computing and printing two separate tables with their own averages and deviations, keeping the same formatting settings.
