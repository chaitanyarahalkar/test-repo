### Things to know about Linux 


An operating system is divided into three parts:

1. The Kernel 
2. Shell 
3. User Applications 

The kernel interfaces directly with the hardware. The kernel also has a sub layer within it which is architecture dependent.

Several shells have been introduced with Bash being the most popular amongst them.

User applications interact with the hardware with system calls. System calls were introduced to provide security and abstraction while accessing.

The diagram given below explains the layout: 

![OS Diagram](os.jpg "Operating System Diagram")

### Important Linux Commands 

Linux commands are a result of binary executables which are usually stored in your /bin,/usr/bin or /sbin folders. Commands can also be made from interpreter scripts like bash,Python,Perl etc.

```
which ls
```
The which command shows the location of the binary executable of ls.

