# Modules 37-39: Operating Systems, Processes and File Handling

## Topic Overview

This lesson introduces the fundamental concepts of operating systems and system programming, with a focus on multi-user and multiprogrammed environments. The role of the operating system is explained as an arbiter of resources (CPU, memory), provider of services (I/O) and creator of a "virtual machine" for the user. The concept of "process" is introduced as a program in execution, describing its internal and external state and its management by the scheduler with a Round Robin policy. The importance of "supervisor" mode (kernel mode) and of "system calls" as the interface between user programs and OS services is stressed. The lesson then focuses on file management, illustrating attributes, naming conventions and permissions in systems such as UNIX/Linux and Windows. The differences between text and binary files and the interaction between programs (in C) and files through streams and descriptors (handles) are described. Finally, the basic file operations (opening, closing, deleting, renaming), the access modes (read, write, append), the techniques for direct access (positioning) and the C functions for reading/writing characters, strings and complex data structures are presented in detail, highlighting the importance of error handling.

---

## 1. Introduction to Operating Systems

### Definition and functions of the operating system

- The operating system (OS) is a set of software modules that makes services available to the programmer through system calls
- The reference environment is a multi-user, multiprogrammed machine
- **Role of arbiter:** it ensures the correct functioning of the system, preventing a program from invading the memory of another or monopolizing resources such as the CPU or the total memory
- **Provision of services:** it spares the user from having to implement low-level functions such as I/O (input/output), for example `cin` and `cout` in C++
- **Hardware abstraction:** it masks the peculiarities of peripherals (e.g. mass storage disks), preventing the programmer from having to manage details such as tracks, sectors and cylinders

### The "onion skin" model

- It is a layered representation of how a computer works
- **Layers:**
  1. **Hardware (real machine):** the base, made of CPU, RAM, disks, network card, etc.
  2. **Operating system:** a set of software modules that manages the hardware and provides a more powerful "virtual machine" to the user
  3. **Command interpreter:** a program that receives the user's commands and passes them to the operating system for execution

### Supervisor mode (kernel mode)

- The operating system runs in a privileged mode (kernel mode) to control the users' processes, which run in user mode
- This distinction reserves the execution of special instructions (e.g. process management, I/O) to the OS only, guaranteeing stability and security
- When a user process needs a privileged instruction, it must invoke the supervisor through a system call
- **Motivations:** control of I/O, access to memory, fair sharing of resources (CPU, disks) and management of conflicts

---

## 2. Process Management

### Definition of process

- A process is a sequential activity, described as a "program in execution". Two copies of the same program in execution constitute two distinct processes

### State of a process

- **Internal state:** indicates the next instruction to execute and includes the values of variables and registers
- **External state:** describes the situation of the process with respect to the CPU. It is managed by the OS and can be:
  - **Waiting:** suspended, waiting for an event (e.g. I/O)
  - **Running:** its instructions are executed by the CPU
  - **Ready for execution:** ready to be run, waiting for the CPU to become free

### Multiprogramming and virtual machines

- In a multiprogrammed machine, the OS makes a dedicated "virtual machine" visible to each process, managing the sharing of the real resources (CPU, memory, disk)

### The scheduler and the Round Robin policy

- The scheduler is a component of the OS that selects the processes in the "ready" state and assigns the CPU to them in turn for a "time quantum". This policy is called **Round Robin**

### Parallelism and process creation

- In a multi-user system (e.g. UNIX), the connection of a new user requires generating a new process to manage the session, running several copies of the same program in parallel

---

## 3. System Programming and System Calls

### Definition of system programming

- Techniques used to write programs (in user mode) that interact closely with the OS through system calls. The reference language will be C

### Main categories of system calls

- Management of processes, files, directories and file system, protection mechanisms, management of time and date

### Operations on processes

- The primitives make it possible to: generate a new process, wait for its termination, terminate it and replace its executable code

---

## 4. File Management

### Characteristics and attributes of files

- A file is a "Long Lived Object" identified by a name (unique in its directory) and optionally an extension
- **Naming conventions:** they vary between systems (DOS: 8+3 characters; Linux: up to 32). It is good practice to avoid special characters
- **Metadata:** they include length (in bytes), dates (creation, last modification), owner and access permissions (read, write, execute)

### File management in a UNIX/Linux environment

- **`ls` command:** used to display information on files (e.g. `ls -lpa` shows permissions, owner, length, dates)
- **Access rights (permissions):** specified for three categories (owner, group, others) with the permissions `r` (read), `w` (write), `x` (execute)
- **`chmod` command:** used to modify the access rights

### Program-file interaction and standard streams

- A program opens a file by invoking the OS, which returns a "file descriptor" (handle or file pointer). This handle stores the current position in the file
- Closing the file guarantees the physical saving of the changes and releases the descriptor
- **Standard streams:** three streams are predefined for each process:
  - **Standard In (stdin):** input (typically the keyboard)
  - **Standard Out (stdout):** output (typically the screen)
  - **Standard Error (stderr):** output for error messages

### Types of files

- **Text files (ASCII):** sequences of characters divided into lines. They can be displayed and printed with standard commands (`cat`, `type`, `lpr`, `print`)
- **Binary files:** sequences of bytes. They require a specific program that knows their structure in order to be interpreted correctly

---

## 5. File Operations in C

### File access modes

- **`r` (READ):** read only
- **`w` (WRITE):** writing from the beginning of the file
- **`a` (APPEND):** writing at the end of the file
- **Modifiers:**
  - `b` (binary): binary access (e.g. `rb`, `wb`)
  - `+` (read/write): read and write access (e.g. `r+`, `w+`)
- The modes are subject to the permissions of the file system

### Basic system calls

- **`fopen(name, mode)`:** opens a file. It returns a file pointer (`FILE*`). If it returns `NULL`, an error occurred
- **`fclose(fp)`:** closes a file. It returns a non-zero value in case of error
- **`remove(name)`:** deletes a file
- **`rename(old_name, new_name)`:** renames or moves a file

### Error handling

- **`feof(fp)`:** checks whether the end of the file has been reached
- **`ferror(fp)`:** checks whether generic access errors have occurred
- **`clearerr(fp)`:** resets the error and end-of-file indicators

### Direct access (positioning)

- **`fseek(fp, offset, refpoint)`:** changes the current position. `refpoint` can be `SEEK_SET` (beginning), `SEEK_CUR` (current), `SEEK_END` (end)
- **`ftell(fp)`:** returns the current position in bytes
- **`rewind(fp)`:** brings the position back to the beginning of the file (equivalent to `fseek(fp, 0, SEEK_SET)`)

### Reading and writing data

- **Characters:** `fgetc(fp)` (reads), `fputc(c, fp)` (writes)
- **Strings:** `fgets(s, n, fp)` (reads), `fputs(s, fp)` (writes)
- **Blocks of data (struct):**
  - `fread(&var, elem_size, num_elem, fp)`: reads one or more elements (e.g. `struct`) from a file
  - `fwrite(&var, elem_size, num_elem, fp)`: writes one or more elements to a file

---

## Tasks

1. Go deeper into the categories of system calls mentioned using the text by Tanenbaum and Woodhull
2. Become familiar with the `ls` command and its options (e.g. `ls -lpa`) in a UNIX/Linux environment to inspect the metadata and permissions of files
3. Practice with the `chmod` command to modify the permissions of a test file in a UNIX/Linux system
4. Experiment with the use of the commands `cat`/`type` and `lpr`/`print` on text and binary files to observe the differences in the output
5. Implement a C program that opens a file, verifying that the opening operation was successful by checking the return value of `fopen`
6. Write a program that uses `fseek` to position at specific points of a file and read/write data
7. Create a program that defines a `struct` (e.g. `STUDENT`) and uses `fwrite` to write several instances of the `struct` to a binary file, and `fread` to read them afterwards
8. Practice error handling, using `feof` and `ferror` to check the state during read operations from a file
