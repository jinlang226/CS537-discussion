## ADD A SYSCALL TO SET PRIORITY OF A PROCESS

The first part adds support for the priority-based scheduling. However, all the processes still have the same priority (50, the default priority). In the second part, you will add a new syscall (`setpriority`) for a process to change its priority. The syscall changes the current process’s priority and returns the old priority. If the new priority is lower than the old priority (i.e., the value of new priority is larger), the syscall will call `yield` to reschedule.

In this part, you will need to change `user.h`, `usys.S`, `syscall.h`, `syscall.c`, and `sysproc.c`. Review
Lab 1 to refresh the steps to add a new syscall. Here is a summary of what to do in each file:

-	`syscall.h`: add a new definition for `SYS_setpriority`.
-	`user.h`: declare the function for user-space applications to access the syscall by adding: `int setpriority(int);`
-	`usys.S`: implement the `setpriority` function by making a syscall to the kernel.
-	`syscall.c`: add the handler for `SYS_setpriority` to the syscalls table using this declaration:
`extern int sys_setpriority(void);`
-	`sysproc.c`: implement the syscall handler `sys_setpriority`. In this function, you need to check that the new priority is valid (in the range of \[0, 200\]), update the process’s priority, and, if the new priority is larger than the old priority, call `yield` to reschedule. You can use the `proc` pointer to access the process control block of the current process.


