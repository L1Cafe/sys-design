# POSIX

Posix is divided in four sections.

## POSIX.1 - Core services

- Process creation and control
- Signals
  - Floating point exceptions
  - Memory violations
  - Illegal instructions
  - Bus errors
  - Timers
- File and directory operations
- Pipes
- C library
- I/O port interface and control
- Process triggers

## POSIX.1b - Real-time extensions

- Priority scheduling
- Real-time signals
- Clocks and timers
- Semaphores
- Message passing
- Shared memory
- Asynchronous and synchronous I/O
- Memory locking interface

## POSIX.1c - Threads extensions

- Thread creation, control, and cleanup
- Thread scheduling
- Thread synchronisation
- Signal handling

## POSIX.2 - shell and utilities

Defines command-line interpreter and utilities such as `cd`, `echo` or `ls`.

----

Taken together, these four sections define the POSIX standard, which provides a portable and standardized interface for developing and running applications on a wide range of operating systems. By adhering to the POSIX standard, developers can write code that is more portable and easier to maintain, while still being able to take advantage of the specific features and capabilities of the underlying operating system.