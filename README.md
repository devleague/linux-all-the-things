# linux-all-the-things

### Linux High Level Things You Should Know
1. **EVERYTHING** IS A FILE
1. What is a kernel?
1. What is a shell?
1. What is an environment?
1. What is a process?
1. What is `bash`?
1. What is `stdin`, `stdout`, `stderr`?
1. What is the purpose of common Linux system directories?  
    * Use `man hier`
2. **TAB LIKE YOU'VE NEVER TABBED BEFORE**
    * To complete file paths
    * To show possible options for commands

### Basic Tips & Tricks

##### Keyboard Shortcuts
* `Ctrl+a` - Go to beginning of line
* `Ctrl+e` - Go to end of line
* `Ctrl+b` - Go back one character (hold to scroll)
* `Ctrl+f` - Go forward one character (hold to scroll)
* `Ctrl+d` - Delete the next character
* `Ctrl+u` - Delete from cursor to beginning of line
* `!!` or `sudo !!` - Repeat the current line or repeat the current line as `sudo` respectively
* `!15` - Repeat line 15 from `history` 
* `$_` or `cd $_` - Repeat the argument from the previous command
* `history` - Show your history of commands if you can't remember what you've done or need to run a previous command again....*or to see what someone else has done*
* `alias` - Create aliases to save yourself from typing common complex commands repeatedly

##### Return Codes
Return codes indicate the outcome of a program running and finishing successfully or not. This is a standard convention for all Linux/Unix software.

* `0` - Program finished successfully
* `1-255` - Program finished with an error

[http://www.tldp.org/LDP/abs/html/exit-status.html]()

##### Piping or Redirection of I/O
* `|` - Used to direct the output of one program into input to another program
* `>, >>, <, <<` - Used to direct the output of one program into a file
* `/dev/null` - A file "descriptor" that output can be redirected to that is never saved to disk. Used to keep `stdout` from being polluted with lots of output.
* `>2&1` - Direct `stderr` to `stdout` to see all output and errors directed to one place. Can be either the terminal or a file.
* `2>/dev/null` - Don't show errors, direct `stderr` to nothingness

##### Chaining commands
* `&`, `;` - You can run many commands together in the terminal and separate them with either character

### Documentation
##### help
Most command line packages support either or both of the following flags to show a brief description of what arguments and flags a tool supports:

*  `-h`
*  `--help`

**Examples:**

`nmap --help`

`ping -h`

##### man pages (aka RTFM)
Most packages that come preinstalled and many add-on packages install their own **man pages** which are installed documentation for how a given program works.

**Examples:**

`man netcat`

`man ps`

`man grep`


#### Wildcard Characters
Wildcard characters can be used in any situation where you're specifying a filename or filepath to account for patterns as opposed to explicit matches.

* `*` - Wildcard, match any characters 
* `?` - Wildcard, match a single character

**Examples:**

`rm c*.png` - Remove all png files starting with a `c`, `cat.png`, `cut.png`, `cult.png`

`rm c?t.png` - Remove both `cat.png` and `cut.png` but not `cult.png`

### Package Managers/Management
The open source world is an ecosystem of code written by different authors, for different operating systems and having many different versions of each. 

To manage all of that, we need the use of tools. There are primarily two concepts we must remember:

* **Repositories** - The master list of where the physical code files reside and what the current versions are
* **Packages** - The actual code/packages themselves that get downloaded/installed/updated/removed by the package manager

**NOTE:** All of these packages can be downloaded, compiled and installed without the use of a package manager and people can host their own repositories as well.

#### Managing packages

##### Ubuntu/Kali/Debian
In *Ubuntu* and *Kali* (which are both forks of *Debian*) you can use both the `apt` or `apt-get` package managers
* `apt-get`
  * `install` - install a certain package by name
    * `--only-upgrade` - update a single package
  * `update` - Update the repository links and version. Does NOT update packages themselves.
  * `upgrade` - Upgrade ALL packages that have new versions or security updates
  * `remove` - Uninstall/remove a certain individual package
  * `autoremove` - Clean up all unused packages 


##### Other Linux Distributions
* `apt` - (alternative) Debian Linux based distributions
* `yum` - Red Hat Linux based distributions (Red Hat, Fedora, CentOS)
* `pacman` - Arch Linux

### Navigating and Referencing the File System

##### Current path
* `pwd` - Show the *present working directory*

##### Absolute vs relative paths
An `absolute path` is the entire file or directory path given from the `/` (root) of the file system.

Example: `/home/jaywon/Documents/secret.txt`

A `relative path` is the file path in relation to where the currently running program was started from. Relative paths make use of the `.` (current directory) and `..` (parent directory) special characters.

Examples: 

* `./script.sh` - Run the `script.sh` file in the *current* directory
* `../script.sh` - Run the `script.sh` in the *parent* directory

**NOTE:** Keep in mind that relative and absolute paths can be used in **any** place where a filename is referenced. This can be in programs, command line utilities, etc...
  
##### Common file system navigation commands
* `cd /some/directory/path` - Change directory to the specified path
  * `cd ~` - Change to the current user *home directory*
  * `cd -` - Change to the previous directory
  * `cd ..` - Change to the parent directory
* `mkdir` - Make a directory
* `touch` - Create a file with the specified name
* `mv somefile /some/other/path` - Move a file, also the only way to *rename* a file if the file is staying in the same directory
  * `-i` - Confirm to overwrite a file if it already exists
* `cp` - Copy a file to another location
  * `-r` - If copying an entire directory you must specify that it's a *recursive* copy
* `rm` - Remove a file
  * `-Rf` - If removing an entire directory you must specify that it's a *recursive* removal and to *force* the removal without confirmation for each file
* `ls` - List the contents of a directory, will not show hidden files
  * `-a` - List all files, including hidden files
  * `-l` - List all files, with more detail
  * `-h` - Show file sizes in human readable format
  * `-lah` - Use multiple flags together

**NOTE:** On Ubuntu you will see some aliases defined to make these commands more easily typed

* `cat` - Display the contents of a file or merge multiple files together
  * `-b` - show line numbers with output
* `wc -l` - Show the number of lines in a file
* `less` - Display the contents of a file with user navigation
* `more` - Like `less` with less options
* `head -n 5` - See the top `-n` lines of a file
* `tail -n 5` - See the bottom `-n` lines of a file
* `file` - Show information about the type of file
* `whatis` - General information about a file or command
* `which` - Show the file path for any utility
* `find` - Search for files in the file system
  * `find / -name jaywon` - Find files owned by a certain user
  * `find / -executable -perm -4000 2>/dev/null` - Find all executable files with the `setuid` flag and don't display all error messages 
  * `find / -perm -u=s -type f 2>/dev/null` - Find all files of any type that have the user `setuid` bit set and don't display all error messages
* `locate` - Similar to `find` with less options
* `grep` - Search for matching text in files
* `cut` - If piping (`|`) content into this utility, `cut` the contents into just the sections you want. Default *delimiter* is spaces or tabs (whitespace)
  * Ex. `cut -d: -f 1,7 /etc/passwd`



### Access Control
/etc/shadow (!, !!)
/etc/group
/etc/passwd

* whoami
* who
* id
  * user id
  * group id
  * group name
  * secondary groups
* sudo
* su
* passwd 
  * -l
  * -u
  * -L
  * -S
* adduser
* usermod
* deluser
* chmod
  * +x
  * u+x
* chown
* chage
  - chage -d 0
  - chage -l jaywon
* groups
* /etc/passwd
* /etc/shadow
* /etc/group
* ACL's
* umask (default permissions)

### Process/System Management
* uname -a
* service/systemctl
* uptime
* ~/.bash_profile vs ~/.bashrc
* env
  * export
  * unset
* ps
  * -aux
    * USER - the process owner
    * PID - the process ID (you will need this)
    * START - the date or time when this process started
    * TIME - the amount of CPU time used by this process
    * COMMAND - the command that started the process
* top
  * htop
* free
* kill -9
* bg
* fg
* jobs
* cron
  * config

### Disk Management
* du
* df
* ncdu (apt-get install ncdu)
* lsblk

### Screen Management
* `screen`
* `tmux`

TODO: Talk about Access Control concepts
TODO: Talk about VIM
  - insert mode
  - visual select
  - text operations
  - swap characters forward (xp)
  - swap characters backward (Xp)
     - http://vim.wikia.com/wiki/Swapping_characters,_words_and_lines
  - vimtutor
  - buffers
  - set numbers
  - open other files
  - executing commands in vim
TODO: Show alias capability
TODO: Show cron
TODO: Create and compile simple C program that sleeps to show process management
TODO: Simple bash scripting CLI exercise

#### Optional
* sort
  - k (column to sort on)
* uniq
  -c
* strings
* base64
* shasum -a 256
* tar (compression)
* gzip
* tr
* awk (ADVANCED)
* sed (ADVANCED)

### Resources
- [](http://vim.wikia.com/wiki/Vim_Tips_Wiki)
