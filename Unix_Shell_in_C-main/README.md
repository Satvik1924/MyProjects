# SimpleShell - README

## Project Overview
**SimpleShell** is a minimalistic UNIX shell implemented in C. It allows users to execute shell commands, handle piped commands, and manage a command history. The shell also provides additional features such as signal handling for graceful termination (via `Ctrl+C`) and logging command execution time.

---

## Features
1. **Basic Command Execution**  
   Execute single UNIX commands with arguments, such as `ls -l`, `echo "Hello, World!"`, etc.

2. **Piped Commands**  
   Supports multiple piped commands, such as `ls -l | grep "test" | wc -l`.

3. **Command History**  
   - Maintains a persistent command history saved to a `history.txt` file.  
   - Allows viewing the history with the `history` command.

4. **Timing and Logging**  
   - Logs execution time, start and end timestamps, and process ID (PID) for each command in `history.txt`.

5. **Graceful Termination**  
   - Handles `Ctrl+C` to terminate the shell and display the command history.

---

## How It Works
1. **Input Parsing**  
   - User inputs are tokenized to identify commands and arguments.
   - The shell detects pipes (`|`) to execute piped commands.

2. **Command Execution**  
   - Commands are executed using `fork()` and `execvp()`.
   - For piped commands, pipes (`pipe()`) connect the output of one process to the input of the next.

3. **History Management**  
   - Commands are appended to `history.txt` after execution.
   - Viewing the history reads and displays the contents of the `history.txt` file.

4. **Signal Handling**  
   - `SIGINT` (`Ctrl+C`) is caught, triggering the display of the command history before exiting.

---

## Usage Instructions
### Running the Shell
Compile the code and run the shell as follows:
```bash
gcc -o SimpleShell shell.c
./SimpleShell
```

### Commands
- **Executing a command**:  
  Example:  
  ```bash
  group50@SimpleShell $ ls -l
  ```
- **Executing piped commands**:  
  Example:  
  ```bash
  group50@SimpleShell $ ls -l | grep ".c" | wc -l
  ```
- **Viewing command history**:  
  ```bash
  group50@SimpleShell $ history
  ```
- **Exiting the shell**:  
  ```bash
  group50@SimpleShell $ exit
  ```
- **Terminating with Ctrl+C**:  
  Displays command history and exits.

---

## Files
- **`shell.c`**: Source code for the shell.
- **`history.txt`**: File used to log the command history, timestamps, and execution times.

---

## Limitations
1. Supports up to 10 piped commands in a single input.
2. Limited error handling for invalid or malformed commands.
3. Does not handle advanced shell features like background processes (`&`) or redirection (`>`, `<`).

---

## Future Enhancements
1. Add support for redirection (`>`, `<`) and background execution (`&`).
2. Improve error handling and provide descriptive error messages.
3. Include built-in commands for directory management (`cd`, `pwd`).
4. Optimize logging and remove redundant execution calls.

---
