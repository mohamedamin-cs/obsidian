`#!/bin/bash`: $shebang$
___
### Think of `awk` as:
- A **mini programming language** for working with text, especially in columns.
- Often used to **print specific fields**, **filter lines**, or even do math.
- awk 'pattern { action }' file
- `some_command | awk 'pattern { action }'`
- `awk '$2 == "192.168.1.12"' MySQLscan`
___

| Command  | Function                                                               |
| -------- | ---------------------------------------------------------------------- |
| :        | Returns 0 or true                                                      |
| .        | Executes a shell script                                                |
| [[       | Performs a conditional test                                            |
| bg       | Puts a job in the background                                           |
| break    | Exits the current loop                                                 |
| cd       | Changes directory                                                      |
| continue | Resumes the current loop                                               |
| echo     | Displays the command arguments                                         |
| eval     | Evaluates the following expression                                     |
| exec     | Executes the following command without creating a new process          |
| exit     | Quits the shell                                                        |
| export   | Makes a variable or function available to other programs               |
| fg       | Brings a job to the foreground                                         |
| getopts  | Parses arguments to the shell script                                   |
| jobs     | Lists background (bg) jobs                                             |
| pwd      | Displays the current directory                                         |
| read     | Reads a line from standard input                                       |
| readonly | Declares a variable as read-only                                       |
| set      | Lists all variables                                                    |
| shift    | Moves the script’s input parameters left, dropping the first parameter |
| test     | Evaluates arguments                                                    |
| times    | Prints the user and system times                                       |
| trap     | Traps a signal so the script can handle it                             |
| type     | Displays how each argument is interpreted as a command                 |
| umask    | Changes the default permissions for a new file                         |
| unset    | Deletes values from a variable or function                             |
| wait     | Waits for a background process to complete                             |
