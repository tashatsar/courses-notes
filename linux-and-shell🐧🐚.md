# linux-commands-and-shell🐧🐚
# Feb 2024

Short notes on course [Hands-on Introduction to Linux Commands and Shell Scripting](https://www.coursera.org/learn/hands-on-introduction-to-linux-commands-and-shell-scripting) by Coursera. 

## Table of Contents
1. [Introduction to Linux](#introduction-to-linux):
	1. [Introduction to Linux👋](#introduction-to-linux👋)
	1. [Questions and answers💯](#questions-and-answers💯)
2. [Linux Commands](#linux-commands):
	1. [Informational Commands](#informational-commandsℹ️)
 	2. [Navigating Files and Directories](#navigating-files-and-directories🗺️)
  	3. [Viewing file contents](#viewing-file-contents🔍)
   	4. [Questions and answers](#questions-and-answers💯)

## Introduction to Linux 🐧
### Introduction to Linux👋

|Linux|Information|
|---|---|
|**usage**|mobile devices, desktops, supercomputers, data centers, and cloud servers|
|**distros**|distributions differ by UIs, shell applications, and how the OS is supported and built. Popular distros: Red Hat Enterprise Linux (RHEL), Debian, Ubuntu, Suse (SLES, SLED, OpenSuse), Fedora, Mint, and Arch.|
|**layers**|five key layers: the UI, application, OS, kernel, and hardware|
|**user interface**|enables users to interact with applications|
|**application**|enable users to perform tasks within the system|
|**OS**|runs on top of the kernel and is vital for system health and stability|
|**kernel**|the lowest-level software that enables applications to interact with hardware|
|**hardware**|includes all the physical or electronic components of your PC|
|**shell**|OS-level application to send commands via terminal|
|**filesystem**|tree-like structure consisting of all directories and files on the system|
|**text editors**|command-line or GUI-based text editors such as GNU nano, vim, vi, and gedit|
|**package managers**|DEB and RPM packages are used by package managers in Linux operating systems. They are distinct file types containing software or updates for different Linux operating systems.|
|**.deb file**s|used for Debian-based distributions such as Debian, Ubuntu, and Mint. Deb stands for Debian.|
|**.rpm files**|used for Red Hat-based distributions such as CentOS/RHEL, Fedora, and openSUSE. RPM stands for Red Hat Package Manager.|
|**convert packages**|Deb and RPM formats are equivalent, the contents of the file can be used on other types of Linux OSs. TO convert use the `alien` command and specify the package name that you want to convert|

### Questions and answers💯
1. Which one of the following statements about Linux distributions is true? *Debian is stable, reliable, and fully open source.*
2. Which layer of the Linux system contains system daemons and shells? *Application*
3. Which layer of the Linux system assigns software to users, helps detect errors, and performs file management tasks? *Operating system*
4. Which layer of the Linux system is responsible for memory management, process management, device driver management, system calls and security? *Kernel*
5. Which of the following is a standard directory in the Linux filesystem? *bin*
6. Which of the following is a GUI-based text editor? *gedit*
7. Which of the following path helps you navigate to the user’s home directory? *~*
8. Complete the following. Packages are: _Archive files_
9. Which command can you use to convert package files between deb and RPM formats? _alien_
10. Complete the following. An advantage of using a GUI-based package manager such as PackageKit is that: _It automatically checks for updates at configurable intervals._


## Linux Commands
### Informational Commandsℹ️
#### Getting information
- `whoami` to return your username
- `uname` to print the kernel name
	- `uname -a` option prints all the system information
- `id` to display the user and group id
- `echo` to print given text
	- `echo -e` for working with special characters
- `date` to display the current time and date
	- `date '+%D' displays the current date in mm/dd/yy format
- `man` to get the user manual for a command
#### Monitoring system performance and status
- `df` to print available disk space
	- `df -h` to get available disk space in a "human-readable" format
- `ps` to list running processes and their process id
	- `ps -e` to display all of the processes running on the system
- `top` to view a real-time table of processes
	- `top -n 10` exit automatically after a specified number of repetitions
	- `Shift+m` Memory Usage 
	- `Shift+p` CPU Usage
	- `Shift+n` Process ID (PID)
	- `Shift+t` Running Time

### Navigating Files and Directories🗺️
#### Getting information
- `pwd` to get the location of your present working directory
- `ls` to list the files and directories within a directory
	- `-a`	list all files, including hidden files
	- `-d` list directories only, do not include files
	- `-h`	with -l and -s, print sizes like 1K, 234M, 2G
	- `-l`	include attributes like permissions, owner, size, and last-modified date
	- `-S`	sort by file size, largest first
	- `-t`	sort by last-modified date, newest first
	- `-r`	reverse the sort order
- `mkdir` to create a new directory
- `cd` to change your present working directory
#### Creating, copying, moving, and deleting files:
- `touch a_new_file.txt` creates an empty file or update existing file's timestamp
- `find` to search for and locate files
	- `find /etc -name \'*.txt\'` finds all .txt files in the /etc directory and all of its subdirectories
- `rm this_old_file.txt -v` removes a file verbosely
- `mv this_file.txt that_path/that_file.txt` changes file name of path
- `cp file.txt new_path/new_name.txt` copies a file

  
### Viewing file contents🔍
- `cat my_shell_script.sh` displays the tail end of the file
- `more filename.ext` displays the top portion of the file first, `q` for quitting
- `head -10 data_table.csv` displays first 10 lines of file
- `tail -10 data_table.csv` displays last 10 lines of file
- `wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0250EN-SkillsNetwork/labs/Bash%20Scripting/usdoi.txt`
#### Displaying basic stats:
- `wc usdoi.txt` to find the number of lines, words, and characters in a file
	- `wc  -l table_of_data.csv` lines
	- `wc  -w my_essay.txt` words
	- `wc  -m some_document.txt` characters

### Questions and answers💯









### Docker basics
**Docker:** a platform for developing, shipping, and running applications that  enables to separate applications from  infrastructure
