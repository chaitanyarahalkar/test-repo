### Dot Files

The beauty of Unix-like and Linux based systems is complete control & customisation of the system. 

Dot files are conventionally hidden files in Unix and Linux based systems which cannot be viewed neither from a regular file manager unless specified or by invoking ls.

However ls has a special flag -a which lists all the files in the directory. -l is also used with a to show the file permissions,size & modification information.

``` 
ls -a

``` 

If you list the hidden files in your root directory ('/') several well known dot files will be listed like the .bash_profile,.ssh folder etc.

Check out [here](https://dotfiles.github.io/) to get some really heavy customised dot files. Just clone the ones you like and replace the given dot files with your existing one or simply compile the code with make if a Makefile exists.
