# Programming Basics questions

## Software Development Methodologies

#### What is the main goal of a retrospective meeting?
The goal is to discuss what went well and what did not, and draw up an action item.

## Programming environment

### Unix

#### What is UNIX and what is Linux?

The primary difference is that Linux and Unix are two different Operating Systems though they both have some common commands. 
The source code of Linux is freely available to it's users. Linux is a UNIX Clone.

#### What do we call the shell in Linux?
The shell is a program that takes commands from the keyboard and gives them to the operating system to perform.

#### What does root means in a Linux environment?
Root is the user name or account that by default has access to all commands and files on a Linux.

#### How do you access your hard drives in Linux?
#### How can you install an application in Linux?
Most of the time from terminal or ubuntu software manager
 
#### What do we call a repository in Linux? (context: package management)
A Linux repository is a storage location from which your system retrieves and installs OS updates and applications. 
Each repository is a collection of software hosted on a remote server and intended to be used for installing and updating software packages on Linux systems.

#### How do you navigate in the filesystem with the command line?
#### What does the following commands do: mkdir, rm, cat, cp, touch?
__mkdir__ - create a folder or a directory 

__rm__ - delete files and directories (rm -r is used to delete just the directory not the files)
 
__cat__ - display the contents of a file
 
__cp__ - copy files (2 arguments, file name and location)
 
__touch__ - create a file

#### How can you look up what does a command do in Linux if you have no internet connection?
With the help of man and help command.
- 'man cd' shows the manual pages of the cd command
- 'cd -help' shows which ways the command can be used

#### What does the following commands do: head, tail, more, less?
__head__: The _head_ command reads the first ten lines of a any given file name (head -5 fileName shows the first 5 lines). 

__tail__: The _tail_ command allows you to display last ten lines of any text file. 

__more__: The _more_ command is used to display the contents of a file in a console. 

__less__: The _less_ command allows you to view the contents of a file and navigate through file. 

The main difference between _more_ and _less_ is that _less_ command is faster because it does not load the entire file at once 
and allows navigation though file using page up/down keys.

#### How do you download a file from the internet using the terminal?
wget "https://codecool.gitlab.io/codecool-curriculum/#/" - to download the file to the current directory
