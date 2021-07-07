# linux-all-the-things

### Linux Distributions
[List_of_Linux_distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions)

### Linux High Level Things You Should Know
1. **EVERYTHING** IS A FILE
1. What is a kernel?
   * Read Chapter 1 in The Linux Command Line
1. What is a shell?
   * Read Chapter 1 in The Linux Command Line
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
* `Alt+b` - Go back one word
* `Alt+f` - Go forward one word
* `Ctrl+d` - Delete the next character
* `Ctrl+u` - Delete from cursor to beginning of line
* `Ctrl+w` - Delete the word before the cursor
* `Ctrl+xx` - Go to beginning of line, edit and repeat command to return to previous position
* `!!` or `sudo !!` - Repeat the current line or repeat the current line as `sudo` respectively
* `!15` - Repeat line 15 from `history` 
* `$_`  - Alias for the value of the argument from the previous command
    * Ex. `cd $_`
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

**NOTE:** Chaining commands is a common tactic in command injection or remote code execution exploits 

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

##### TL;DR man page alternative
[TL;DR](https://github.com/tldr-pages/tldr) - Installable tool that generates shorter man pages for many utilities

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
  * `search` - 


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
* `ln` - Create hard link between two files, both exist as primary
    * `-s` - make soft or symlink which is just an alias to another file
    * `-sf` - overwrite existing symlink

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
When managing users on a Linux system there are three key files that contain all information about a given user:

* `/etc/passwd` - File that stores all user profile info including:
    * `username` - users login name
    * `password` - if an `x` is marked here, it means the user has a password stored in the `/etc/shadow` file
    * `userid(uid)` - unique user id for user
    * `groupid(gid)` - primary group id for this user
    * `user info` - user information entered at time of creation with `adduser` command
    * `home directory`
        * **NOTE:** Some users in the `/etc/passwd` file have the `/sbin/nologin` path as their home directory
    * `shell` - what shell a session will invoke
    * [https://www.cyberciti.biz/faq/understanding-etcpasswd-file-format/]()
* `/etc/shadow` - File that stores all encrypted user passwords and any password related requirments for that user including:
    * `username` - username for password entry
    * `password` - hashed password in the format *`$id$salt$hashed`*
        * The `$id` value stores the encryption algorithm used for hashing the password
    * `lastchanged` - days since last password change
    * `minimum` - minimum number of days required between password changes
    * `maximum` - maximum number of days password is valid 
    * `warn` - number of days to warn user before password expires 
    * `inactive` - number of days after password expires before account is disabled
    * `expire` - days that account has been disabled
    * `!` or `!!` - shows that the user cannot login, default after user is created if no password is set with `useradd`
    * [https://www.cyberciti.biz/faq/understanding-etcshadow-file/](https://www.cyberciti.biz/faq/understanding-etcshadow-file/)

* `/etc/group` - File used to manage all groups and users within them including:
    * `group name` - name of group
    * `password` - usually has an `x`, not used often
    * `group id (gid)` - unique group identifier
    * `group list` - names of the users currently part of that group
    * [https://www.cyberciti.biz/faq/understanding-etcgroup-file/](https://www.cyberciti.biz/faq/understanding-etcgroup-file/)

* `whoami` - shows the current user 
* `who` - shows all users logged into the system
* `id` - show detailed information on owner of current process including:
  * user id
  * group id
  * primary and secondary group names
* `sudo` -  run following command as privileged user if part of the `sudo` group or added to entries in `/etc/sudoers` file
    * **NOTE:** Remember if you forget to add `sudo` when you type a command, rerun the same command with the `sudo !!` shortcut
* `su` - switch user command
* `adduser` - add a new user to the system, this command will prompt for a password and create a home directory and default shell for user. The alternate `useradd` command will **just** create a user in the `/etc/passwd` file with no password and no home directory assigned. Most service accounts are of this type.
* `usermod` - modify existing user group or info settings
    * `-aG sudo bob` - add user to specified group
* `userdel` - delete a given user from the system
* `gpasswd` - used to administer group information
    * `-a bob` - add user to named group
    * `-d bob` - delete user from group
* `groupadd` - create a new group
* `groupdel` - delete a group
* `groupmod` - modify an existing group
* `chage` - manage the password expiration for a user account
  - `chage -d 0` - expire password immediately, forcing user to set a new password upon next login
  - `chage -l bob` - show current password requirement settings
* `passwd` - set a user's password as `root` or for an individual to change their own password
  * `-l user` - lock the account of the specified user
  * `-u user` - unlock the account of the specified user
  * `-S` - show password policy settings for a given user
* `pwck` - check if all settings in `/etc/passwd` or `/etc/shadow` file are correct
* `chown` - change the file ownership settings for a file or directory
    * `-R` - recursively set ownership settings in all files and directories
    * `user:group` - change the user and group ownership settings
    * `user` - change just the owner of the file but not the group
    * `:group` - change just the group ownership of the file but not the user
* `chmod 755 filename` - change the permissions of the specified file or directory using the following bit settings for `user:group:id`
    * bit settings
        * `4` - read
        * `2` - write
        * `1` - execute
    * `-r` - recursively apply permissions
    * without bit syntax
        * `+x` - make executable for user, group and everyone
        * `u+x` - make executable only for user
        * `g+x` - make executable only for group
        * `e+x` - make executable only for everyone
* `groups` - show all groups current user is part of
    * `groups username` - show all groups for another user
* `umask` - current mask for creating default files 
* *ACL's* - **TBD**

### Process/System Management
* `uname` - Print information about the current kernel
    * `-a` - Show all information
    * `-r` - Show just kernel version

* `service` - Manage running *services* or processes that are part of the `System V Init System`, usually files stored in `/etc/init.d`
    * `service ssh status` - show status of service
    * `service ssh start` - start a service
    * `service ssh stop` - stop a service
    * `service ssh restart` - restart a service
    * `service ssh reload` - reload configuration files of running service
    * `service --status-all` - runs status of all defined scripts in `/etc/init.d`
* `systemctl` - Newer/preferred way of managing processes using the `systemd` init system, show all current services and status, with files stored in `/etc/systemd`
    * `systemctl status ssh.service` - show status of service
    * `systemctl start ssh.service` - start service
    * `systemctl stop ssh.service`  - stop service
    * `systemctl restart ssh.service` - restart service
    * `systemctl reload ssh.service` - reload configuration file of running service
* `~/.bash_profile` - Bash script that runs when a user logs in
* `~/.bashrc` - Bash script that runs every time a user open a session window 
* `env` - Current *variables* set for the current running terminal session or running process
  * `export` - Set an environment variable in the current session
  * `unset` - Remove a currently set environment variable in the current session
  * `echo $PATH` - Show the current value of any environment variable
* `uptime` - Show how long the system has been running since last reboot (Linux FTW)
* `ps`
  * `-aux`
    * `USER - the process owner`
    * `PID - the process ID (you will need this)`
    * `START - the date or time when this process started`
    * `TIME - the amount of CPU time used by this process`
    * `COMMAND - the command that started the process`
* `kill -9` - Kill a running process by id immediately
* `top` - See detailed information about all current usage for memory and cpu, in addition to per process usage and parent/child relationships
* `htop` - Awesome third party browsable process view utility (`apt-get install htop`)
* `free` - See current memory usage
* `jobs` - show running jobs/background processes
* `bg` - Send running job to the background
* `fg` - Continue a stopped job back in the foreground
* `cron` - Linux scheduled job process
    * `crontab -e` - Open/edit the current user's crontab entry in a text editor of choice
    * `/etc/cron.d/`
    * `/etc/cron.hourly`
    * `/etc/cron.daily`
    * `/etc/cron.weekly`
    * `/etc/cron.monthly`
    * Configuration helper: [crontab guru](https://crontab.guru/)

### Disk Management
* `du` - Show disk usage statistics
    * `-h` - show in human readable format
* `df` - Show free disk space
    * `-h` - show in human readable format
* `ncdu` - Awesome third party browsable disk usage utility (`apt-get install ncdu`)
* `lsblk` - List block devices (attached storage) 

### Screen Management
* `screen` - Utility to keep terminal session alive when closing a terminal session or logging out of a server
* `tmux` - Similar utility to `screen` with many additional features (preferred)

### VIM (VI Improved)
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

#### Optional
* `sort`
    * `- k` (column to sort on)
* `uniq`
  * `-c` ()
* `strings`
* `base64`
* `shasum -a 256`
* `tar (compression)`
* `gzip`
* `tr`
* `awk (ADVANCED)`
* `sed (ADVANCED)`

### Resources
- Vim Tips - [http://vim.wikia.com/wiki/Vim_Tips_Wiki]()
- TL;DR man pages- [https://github.com/tldr-pages/tldr]()
