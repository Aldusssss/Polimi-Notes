# Modules 40-42: C Input/Output, Process Management and Command-Line Parameters

## Topic Overview

The lesson introduces and details input/output operations in C through the functions `printf`, `scanf`, `puts` and `gets`, their extensions for files and strings (`fprintf`, `fscanf`, `sprintf`, `sscanf`), with particular attention to format controls and the operational differences compared with C++. It then addresses process management in a system environment (`fork`, `wait`, `waitpid`, `exec`, `exit`), illustrating the creation of child processes, synchronization and the replacement of running code, with explanatory examples on PIDs, process hierarchies and termination codes. Finally, it explains parameter passing through the command line with `argc` and `argv` in C/C++, including the use of conversion functions such as `atoi`. The lesson aims to provide practical foundations for input/output and system programming in C, with examples of formats, caveats and operating procedures. Creation date of the content: 2025-12-12.

---

## 1. Input/Output in C

### Main functions for terminal I/O

- **`printf`:** writes formatted text to the screen, analogous to `cout` in C++; it requires the specification of the format and of the variables, including control commands (new line, tab, etc.) and widths/precisions
- **`scanf`:** reads formatted text from the terminal, analogous to `cin` in C++; it needs formats to be specified and provides the values through pointers (the addresses of the variables are passed, e.g. `&myInt`)
- **`puts` and `gets`:** mentioned as functions analogous respectively to writing and reading strings; `gets` includes spaces in the reading, unlike `scanf` with `%s`

### Control commands in `printf`

- `\b`: backspace, moves the cursor (or head) back one position
- `\f`: form feed, jump to a new page
- `\n`: new line, positions at the beginning of the next line
- `\r`: carriage return, positions at the beginning of the current line
- `\t`: tab
- `\DDD`: inserts a character with the decimal ASCII code specified by DDD
- `\xYY`: inserts a character with the hexadecimal ASCII code specified by YY

### Format specifiers in `printf` (integer variables and strings)

- `%c`: prints a character; `%5c`: 5 characters (field of width 5)
- `%d`: signed decimal integer; `%i`: equivalent to `%d`
- `%8d`: signed decimal integer of 8 digits, including the sign
- `%u`: unsigned decimal integer; `%8u`: length of 8 digits unsigned
- `%s`: string (sequence of characters terminated by `\0`); `%40s`: first 40 characters of the string, reserving 40 positions even if the terminator comes earlier
- `%x`: unsigned hexadecimal integer in lowercase alphabet; `%X`: unsigned hexadecimal in uppercase alphabet
- `%o`: unsigned octal integer
- **Alignment:** use the minus sign to align to the left, e.g. `%-5d` for a field of 5 characters aligned to the left

### Specifiers for real numbers (float/double)

- `%f`: signed float/double
- `%8.3f`: 8 characters in total, with 3 decimals, 1 character for the point and 4 for the integer part
- `%e`: exponential notation with lowercase "e"; `%E`: identical but with uppercase "E"

### Examples of `printf` use

- Printing a string and an integer: `"A string: %s\n and an integer: %d\n"` with `myString = "my string"` and `myInt = 27` produces the string and the integer 27
- Integer of 8 characters and real: `%8d` for 27 (padding spaces); `%9.7f` for pi (9 characters in total: 1 for the integer part, 1 for the point and 7 decimals)

### Use of `scanf` and differences in reading strings

- `scanf` uses the same formats as `printf` for the types: `%c`, `%d`, `%i`, `%u`, `%x`, `%o`, `%f`, `%e`
- `%s` in `scanf` does not include spaces: the characters after a space are ignored. To read strings with spaces use `gets`
- The values read are returned through pointers: the address of the variables is passed, e.g. `&myInt`, and for strings a buffer is passed

### Extensions for files and strings

- **Files:** `fprintf` (writing to a file with a handle) and `fscanf` (reading from a file with a file pointer)
- **Strings:** `sprintf` (writing formatted into a string) and `sscanf` (reading from a string). They require a buffer/pointer to a string and formats analogous to `printf`/`scanf`
- Analogous behavior: `fprintf`/`fscanf` and `sprintf`/`sscanf` work like their terminal counterparts

---

## 2. Process Management in C (System Programming)

### Concepts and operations on processes

- **Main operations:** generate a new process, wait for the termination of an existing process, terminate the execution of the process (`exit`), modify the code of a running process to execute other code (`exec`)
- **Terminology:** "master" (parent) and "slave" (child) process. The child is a copy of the parent at the time of `fork` (variables, open files, state are duplicated)

### `fork`: creating a new process

- The primitive `fork` creates a child process identical to the parent at the time of the call; after the duplication the two evolve independently
- **Key difference:** the value of the return variable (`pid_t`) is different in the parent and in the child
- **Return values of `fork` (`pid_t`):**
  - 0 in the child process (slave)
  - −1 in the master in case of failure (e.g. lack of memory for the new process)
  - Any other positive value in the master: it is the PID of the child just created
- **Knowledge of the PID:** the parent knows the PID of the child (return of `fork`), the child does not know its own PID from `fork` (it gets 0)

### Process hierarchies

- Example: the master invokes `fork` twice generating f1 and f2; f2 can generate n2; f1 can generate n11 and n12. Hierarchy:
  - master is the parent of f1 and f2
  - f1 is the parent of n11 and n12
  - f2 is the parent of n2

### Code example with `fork` and flow

- `s_pid = fork();`
- In the master (`s_pid != 0`) the value of `s_pid` is the PID of the child (e.g. B). In the child (`s_pid == 0`) the dedicated branch is executed
- The master can wait for the termination of the child through `wait`; the child ends with `exit`

### `wait`: synchronization with the termination of children

- `wait` suspends the execution of the master until any one of its child processes terminates
- If a child terminates before the master executes `wait`, the execution of `wait` ends immediately (it does not block)
- **Syntax:** `pid_t my_pid = wait(int* status);`
  - `my_pid`: PID of the terminated child
  - `status`: termination code specified by the child (value passed to `exit`)
- **Example:** after `fork` and branch selection, in the master the PID of the child created is printed, `wait(&status)` is invoked, then "process PID has terminated with result STATUS" is printed

### `waitpid`: waiting for a specific child

- Similar to `wait` but waits for the termination of the child process with the specified PID
- **Syntax:** `pid_t my_pid = waitpid(pid_t pid, int* status, int options);`
  - `pid`: identifier of the child to wait for
  - `status`: termination code of the child
  - `options`: further options
- **Behavior:** if the child has already terminated, the execution of `waitpid` in the master ends immediately
- **Example:** the master waits for the termination of the specified PID; then prints "process my_pid has terminated with result status"

### `exec`: replacing the code of the current process

- It replaces the code of the running process with that of another program (name specified), keeping the same PID
- Parameters are passed to the new program through the command line (`argc`, `argv`)
- **Return:** status 0 if successful, −1 if there is an error and the replacement failed
- **Parameters:** name of the program and array of pointers `argv`
- **Example:** in the child created by `fork`, `exec` is executed to replace the code with the program "ls" and parameters "-lg", "/home", "null"; the master continues the execution normally while the child executes `ls`
- **Flow:** `s_pid = fork();` if `s_pid == 0` (in the child) execute MYPROG with `exec`; the new code ends with `exit(0)`; the master waits with `wait` and then proceeds

### `exit`: terminating the process and returning the code

- It terminates the current process and returns a status code to the parent (master)
- If there is no parent process, the code is returned to the command interpreter (shell), making it possible to know the termination result
- **Syntax:** `exit(int status);`
- **Example:** the child ends with `exit(1024)`; in the master suspended on `wait`, `pid` takes the identifier of the terminated child and "process PID has terminated with result STATUS" is printed, here 1024

---

## 3. Command-Line Parameters in C/C++

### Goal and portability

- Specifying parameters directly on the command line is practical and speeds things up; it must be a standard and portable method across compilers and operating systems
- The user must know the format and order of the parameters; the program must check the type and values

### The `argc` and `argv` mechanism

- **`argc`:** number of parameters specified (including the name of the program)
- **`argv`:** array of strings of the individual parameters
- **`argv[0]`:** full name of the program, possibly with the full path
- **Print example:** `cout` is used (in the C++ listing shown) to display `argc` and to iterate over the parameters `argv[0]`, `argv[1]`, …, indicating index and string

### Conversion of types from string

- Integers provided via `argv` are strings and must be converted, for example with `atoi` to obtain an integer value from `argv[i]`
- The program must validate the correctness of the type and values

---

## Tasks

1. Write a C program that prints a string and an integer using `printf` with the formats `%s`, `%d` and includes control commands (`\n`, `\t`), showing the alignment with `%-5d`
2. Implement the reading of an integer and a float from the terminal with `scanf`, using the respective pointers and validating the input
3. Demonstrate the difference between `scanf` with `%s` and `gets` in reading strings containing spaces, with practical examples
4. Create and read a file using `fprintf` and `fscanf`, printing and reading formatted values (integers, floats, strings)
5. Use `sprintf` to format a string with numeric variables and then parse the same string with `sscanf`
6. Write a program that creates a child process with `fork`; in the parent use `wait` to wait for the termination of the child and print PID and status
7. Modify the program to use `waitpid` and wait for a specific child, handling the case of termination already occurred
8. In the child created by `fork`, replace the code with `exec` to execute "ls" with parameters "-lg", "/home", "null", handling `exec` errors (return −1)
9. Implement the use of `exit` in the child to return a non-zero termination code (e.g. 1024) and show the reception of the status in the parent
10. Write a C/C++ program that prints `argc` and all the `argv` with their indices and that converts a numeric parameter with `atoi`, including a validity check
