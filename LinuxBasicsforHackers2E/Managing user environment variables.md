### [[Change default shell]] to bash
- sudo [[kali-tweaks]] --> shell & prompt --> set the default login shell --> bash
---
### Viewing and Modifying Environment Variables
- view all your default environment variables : `env`
### Viewing All Environment Variables
- =including shell variables, local variables, and shell functions, such as any user-defined variables and command aliases:`set | more`
### Changing Variable Values for a Session
- `VAR_NAME=VALUE`
### Making Variable Value Changes Permanent
- `export VARIABLE_NAME`
### Changing Your Shell Prompt
- `username@hostname:current_directory$`
- `$PATH` : which controls where on your system your shell will look for the commands you enter.
- `PATH=$PATH:/root/newhackingtool` add new
### Creating a User-Defined Variable 
- `MYNEWVARIABLE=″Hacking is the most valuable skill set in the 21st century″`
- **delete it** : `unset MYNEWVARIABLE`

