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

What is the $PATH environment variable? 


Every Linux & Unix System has several environment variables which are dynamic variables essential for running several processes in the system.
$HOME,$env being some of the well known environment variables.

The $PATH environment variable stores all the paths where one can find the binary executables for all the commands that we use.

Whenever a command is invoked from the terminal,all the paths in the $PATH environment variable are looked up and if the binary is found, the command is executed.

Trying this out on the terminal produces: 
```
echo $PATH

/home/linus/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

```
The path variable can be usually edited or updated from the .bash_profile hidden file(On Unix like OS) or directly by exporting the variable with the export command.


Creating your own command recipies

Linux or Unix commands can be usually built by shell scripts, Python or Perl scripts.
Let us create a simple Bash script that calculates the factorial of the number sent to it as an argument in the command.

```
#!/bin/bash
count=$1 
fact=1
while [ $count -gt 0 ] 
do
   fact=$(( $fact * $count ))
   count=$(( $count - 1 ))
done
echo $fact

```

Create a sample file with a  .sh extension and copy the factorial code as given above.
Add the directory which contains the given file to your $PATH variable. Edit the variable from your .bash_profile or .profile located in your root directory with your preferred text editor.


```
nano ~/.bash_profle

```

The file may contain several other aliases and variables but look out for the lines and update as shown below
(Make sure there are no spacings between PATH and =)
```
export PATH=/home/linus/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/directory_of_bash_script

```

Do not forget to source the .bash_profile or .profile file with the source command or . 

```
source .bash_profile
```
OR

```
. .bash_profile
```

Calling the script file name from the terminal with any number as the argument to the command will print the factorial to stdout.
The same thing can also be done by creating a symbolic link which will be discussed later.

### Dot Files

The beauty of Unix-like and Linux based systems is complete control & customisation of the system. 

Dot files are conventionally hidden files in Unix and Linux based systems which cannot be viewed neither from a regular file manager unless specified or by invoking ls.

However ls has a special flag -a which lists all the files in the directory. -l is also used with a to show the file permissions,size & modification information.

``` 
ls -a

``` 

If you list the hidden files in your root directory ('/') several well known dot files will be listed like the .bash_profile,.ssh folder etc.

Check out [here](https://dotfiles.github.io/) to get some really heavy customised dot files. Just clone the ones you like and replace the given dot files with your existing one or simply compile the code with make if a Makefile exists.


### File Permissions 

Unix & Linux provides Read(r),Write(w) and Execute(x) permissions to any file on the system. 
If you ``` ls -l ``` every file with its permissions will be shown.

The system is divided into three types - User,Group and others. The r,w,x permissions are assigned to each type. This is well explained by the diagram shown below: 

![Permissions](permissions.jpg "Permissions")


