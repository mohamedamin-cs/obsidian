- `ps aux`: viewing processes
### Changing Process Priority
- `nice` : suggest that a process should be elevated in priority.
- |------------|------------|
- -20(most)   0            +19(least)
- The [[nice]] command requires that you increment the nice value, whereas the [[renice]] command wants an absolute value for niceness.
- `sudo nice -n -10(or 10) /bin/slowprocess`
- `sudo renice 19 6996`
- top + R = renice
### Killing Processes
- `kill -signal PID`
- default = SIGTERM
- **[[SIGHUB]]** : 1 (Hangup) It stops the designated process and restarts it with the same [[PID]].
- **[[SIGINT]]** : 2 (Interrupt) It is a weak kill signal that isn’t guaranteed to work but does in most cases.
- **[[SIGQUIT]]** :  3 (core dump)It terminates the process and saves the process information in memory. Then it saves this information in the current working directory to a file named core
- **[[SIGTERM]]** : 9 (termination) This is the Termination (TERM) signal. It is the kill command’s default kill signal.
- **[[SIGKILL]]** : 15 This is the absolute kill signal. It forces the process to stop by sending the process’s resources to a special device, /dev/null.
- k + top = [[kill]] a process
- killall : kill all processes
### Scheduling Processes
- kali> `sudo at 7:20am`
	at> `/root/myscanningscript`
	
| Time Format            | Meaning                                               |
| ---------------------- | ----------------------------------------------------- |
| `at 7:20pm`            | Scheduled to run at 7:20 pm on the current day        |
| `at 7:20pm June 25`    | Scheduled to run at 7:20 pm on June 25                |
| `at noon`              | Scheduled to run at noon on the current day           |
| `at noon June 25`      | Scheduled to run at noon on June 25                   |
| `at tomorrow`          | Scheduled to run tomorrow                             |
| `at now + 20 minutes`  | Scheduled to run in 20 minutes from the current time  |
| `at now + 10 hours`    | Scheduled to run in 10 hours from the current time    |
| `at now + 5 days`      | Scheduled to run in five days from the current date   |
| `at now + 3 weeks`     | Scheduled to run in three weeks from the current date |
| `at 7:20pm 06/25/2024` | Scheduled to run at 7:20 pm on June 25, 2025          |
