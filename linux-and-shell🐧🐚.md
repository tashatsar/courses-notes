# linux-commands-and-shell

Short notes on course [Hands-on Introduction to Linux Commands and Shell Scripting](https://www.coursera.org/learn/hands-on-introduction-to-linux-commands-and-shell-scripting) by Coursera. 

## Table of Contents
1. [Introduction to Linux](#introduction-to-linux):
	1. [Introduction to Linux](#introduction-to-linux)
	1. [Questions and answers](###Questions-and-answers)
2. [Airflow](#airflow):
	1. [Commands](#commands)

## Introduction to Linux 🐧
### Introduction to Linux
|---|---|
|Linux|Information|
|---|---|
|usage|mobile devices, desktops, supercomputers, data centers, and cloud servers|
|distros|distributions differ by UIs, shell applications, and how the OS is supported and built. Popular distros: Red Hat Enterprise Linux (RHEL), Debian, Ubuntu, Suse (SLES, SLED, OpenSuse), Fedora, Mint, and Arch.|
|layers|five key layers: the UI, application, OS, kernel, and hardware|
|user interface |enables users to interact with applications|
|application|enable users to perform tasks within the system|
|OS|runs on top of the kernel and is vital for system health and stability|
|kernel|the lowest-level software that enables applications to interact with hardware|
|hardware|includes all the physical or electronic components of your PC|
|shell|OS-level application to send commands via terminal|
|filesystem|tree-like structure consisting of all directories and files on the system|
|text editors|command-line or GUI-based text editors such as GNU nano, vim, vi, and gedit|
|package managers|DEB and RPM packages are used by package managers in Linux operating systems. They are distinct file types containing software or updates for different Linux operating systems.|
|.deb files|used for Debian-based distributions such as Debian, Ubuntu, and Mint. Deb stands for Debian.|
|.rpm files|used for Red Hat-based distributions such as CentOS/RHEL, Fedora, and openSUSE. RPM stands for Red Hat Package Manager.|
|convert packages|Deb and RPM formats are equivalent, the contents of the file can be used on other types of Linux OSs. TO convert use the `alien` command and specify the package name that you want to convert|
---|---

### Questions and answers
1. Which one of the following statements about Linux distributions is true? *Debian is stable, reliable, and fully open source.*
2. Which layer of the Linux system contains system daemons and shells? *Application*
3. Which layer of the Linux system assigns software to users, helps detect errors, and performs file management tasks? *Operating system*
4. Which layer of the Linux system is responsible for memory management, process management, device driver management, system calls and security? *Kernel*
5. Which of the following is a standard directory in the Linux filesystem? *bin*
6. Which of the following is a GUI-based text editor? *gedit*
7. Which of the following path helps you navigate to the user’s home directory? *~*
8. Complete the following. Packages are: _Archive files_
9. Which command can you use to convert package files between deb and RPM formats? _alien_
10. Complete the following. An advantage of using a GUI-based package manager such as PackageKit is that: _It automatically checks for updates at configurable intervals. _





### Docker basics
**Docker:** a platform for developing, shipping, and running applications that  enables to separate applications from  infrastructure
