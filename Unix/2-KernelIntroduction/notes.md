# Introduction to the Kernel

## Architecture of the UNIX Operating System

* files and processes are the two central concepts of UNIX
* system call and library interface represent border between user programs and
  the kernel
* interrupts NOT serviced by special processes, but by special functions in the
  kernel within the context of the current process 
  
## Introduction to System Concepts

* every file has one inode (index node)
* a file may have several names (links) pointing to the same inode
* separate user and kernel stacks for process
* the kernel services interrupts in the context of the interrupted process, even
  if it didn't cause the interrupt; kernel saves enough information to resume
  process, then services interrupt in kernel mode
* kernel protects its consistency by prohibiting arbitrary context switches and
  controlling occurrences of interrupts (disallowed during execution of critical
  code in kernel mode)
* context can only be switched when process is in "asleep"[in memory] state
* processes running in kernel mode cannot be preempted by other processes; the
  process needs to be transitioned into "asleep" state before context switching
* non-preemptive nature of kernel ensures critical sections of code are executed
  by only one process at a time
* code is considered "critical" if execution of arbitrary interruption handlers
  could cause inconsistency; critical regions are small and infrequent, so
  throughput largely unaffected
* NOTE: multiprocessor systems handle things differently 
* one process cannot change the state of another
* sleeping processes do not consume CPU resources; kernel only awakens sleeping
  process when event occurs
