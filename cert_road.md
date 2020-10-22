# LPIC-101&&102.v5

[Study file](LPIC-1%20Linux%20Professional%20Institute%20Certification%20Study%20Guide%20Exam%20101-500%20and%20Exam%20102-500%20by%20Christine%20Bresnahan,%20Richard%20Blum%20(z-lib.org).pdf)

- LINKS
  - <https://www.booleanworld.com/guide-linux-top-command/>
  - <https://www.certdepot.net/>

## Chapter 1 - Exploring Linux Command-Line Tools

When you successfully log into a tty terminal, the program providing that prompt is a shell. Some shells:

- **Bash**: GNU Bourne Again Shell
- **Dash**: Debian Almquist Shell. Smaller shell does not alow command-line editing or command history, but it does provide faster shell program execution.
- **KornShell**: programming shell compatible with Bourne shell but supports advanced programming features, such as those available in the C programming languages
- **tcsh**: TENEX C shell is an upgraded version of the C Shell. Command completion; incorporates element of C programming language into shell scripts.
- **Z shell**: incorporates features from Bash, tcsh, and Kornshell.

The _bin/sh_ file originally was the location of the system's shell. Nowadays it's now a symbolic link to a shell.

When talking about shell command's syntax, the braket means that it's optional (`echo [OPTION] ... [STRING]`).

Metacharacters: `* ? [ ] ' " \ $ ; & ( ) | ^ < >`; escape character: `\`

### Navigating the Directory structure

```bash
cd
cd -
cd ~
cd $HOME
cd ..
pwd
```

Files on a Linux system are stored within a single directory structure, called a _virtual directory_. The virutal directory contains files from all the computer's storage devices and merges them into a single directory structure. This structure has a single base directory called the _root directory_, often simply called _root_.

A current working directory is the directory your process is currently using within the virtual directory structure.

### Understanding Internal and External Commands

```bash
type <command>
```

Within a shell, some commands that you type at the command line are part of (internal to) the shell program. These internal commands are sometimes called _built-in commands_. Other commands are external programs, because they are part of the shell.

An external command command is indicated by the type command displaying the program's absolute directory reference within the virtual directory structure.

### Using Environment Variables

Environment variables track specific system information, such as the name of the user logged into the shell, the default home directory for the user, the search path the shell uses to find executable programs... Most common environment variables:

| Name | Description |
| ------ | -------- |
| BASH_VERSION | Current Bash shell instance's version number (chap 1) |
| EDITOR | default editor used by some shell commands (chap 1) |
| GROUPS | user account's group memberships (chap 7) |
| HISTFILE | name of the user's shell command history file (chap 1) |
| HISTSIZE | maximum number of commands stored in history file (chap 1) |
| HOME | current user's home directory name (chap 1) |
| HOSTNAME | current system's host name (chap 8) |
| LANG | locale category for the shell (chap 6) |
| LC_* | various locale settings that override LANG (chap 6) |
| LC_ALL | locale category for the shell that overrides LANG (chap 6) |
| LD_LIBRARY_PATH | colon-separated list of library directories to search prior to looking through the standard library directories (chap 2) |
| PATH | colon-separated list of directories to search for commands (chap 1) |
| PS1 | primary shell command-line interface prompt string (chap 1) |
| PS2 | secondary shell command-line interface prompt string |
| PWD | user account's current working directory (chap 1) |
| SHLVL | current shell level (chap 1) |
| TZ | user's time zone, if different from system's time zone (chap 6) |
| UID | user account's user identification number (chap 7) |
| VISUAL | default screen-based editor used by some shell commands (chap 1) |

Display list of active variables: `set` command - also `env` and `printenv`.

When you enter a program name (command) at the shell prompt, the shell will search all the directories listed in the **_PATH_** environment variable for that program. If the shell cannot find the program, you will receive a `command not found` error message.

To run a program that does not reside in a PATH directory location, you must provide the command's absolute directory reference when entering the program's name at the command line.

The `which` utility searches through the PATH directories to find the program. If it locates the program, it displays its absolute directory reference.

A _subshell_ is created when you perform certain tasks, suchas running a shell script or running particular commands. We can determine whether your process is currently in a subshell by looking at the data stored in the SHLVL environment variable. A **1** indicates you are _not_ in a subshell, because subshells have higher numbers. Thus, if SHLVL contains a number higher than 1, this indicates you're in subshell.

The bash command automatically creates a subshell, which is helpful for demonstrating the temporary nature of employing the simple environment variable modification method.

To preserve an environment variable's setting, you need to employ the `export` command. You can either use export when typing in the original variable definition or use it after the variable is defined, by typing **export _variable-name_** at the comman-line prompt.

You can reverse any modifications you make to the variable by using the `unset` command.

The shell keeps track of all the commands you have recently used and stores them in your login session's history list - `history` command. To reexecute a command from a history list, we use the number to the left of the history command's output preceded by `!` - `!920`. Run `!!` to run the most recent command

The history list is preserved between login sessions in the file designated by the $HISTFILE environment variable. It's typically the .bash_history file in your home directory.

To remove contents from the histroy file: `history -c` (clear current history list); then, `history -w` (copies the now blank history list to the .bash_history file, overwriting it's contents).

### Editing Text Files

Determine the editor command: `which vim` or `which vi`. _vim_ modes:

1. Command mode: sometimes called normal mode. Best mode for quickly moving around the buffer area.
2. Insert mode: simple editing. Pressing the **I** key, for _INSERT_.
3. Ex mode: colon command mode, every command is preceded with a colon (:).

| Keystroke(s) | Description |
| ------ | -------- |
| ? | forward search |
| / | backward search |
| h | Move cursor left one character.|
| l | Move cursor right one character.|
| j | Move cursor down one line (the next line in the text).|
| k | Move cursor up one line (the previous line in the text).|
| w | Move cursor forward one word to front of next word.|
| e | Move cursor to end of current word.|
| b | Move cursor backward one word.|
| ^ | Move cursor to beginning of line.|
| $ | Move cursor to end of line.|
| gg | Move cursor to the file’s first line.|
| G | Move cursor to the file’s last line.|
| nG | Move cursor to file line number n .|
| Ctrl+B | Scroll up almost one full screen.|
| Ctrl+F | Scroll down almost one full screen.|
| Ctrl+U | Scroll up half of a screen.|
| Ctrl+D | Scroll down half of a screen.|
| Ctrl+Y | Scroll up one line. |
| Ctrl+E | Scroll down one line. |
|dd | Delete current line. |
|dw | Delete current word. |

### Processing Text using Filters

There are variants of teh cat command - `bzcat`, `xzcat` and `zcat`. These utilities are used to display the contents of compressed files.

`paste` command: display files side by side in an ugly manner.

The `od` utility allows you to display a file's contents in octal (base 8 - default option), hexadecimal (base 16), decimal (base 10) and ASCII; `od [OPTION]... [FILE]...`

`split` command: allows you to divide a large file into smaller chunks, which is handy when you want to quickly create a samaller text file for testing purposes. `split [option] [input [prefix]]`

`sort` command: the output is sorted: `sort [option] [file]`; -n option to order numbers; save output `sort -o newfile originalfile`.

`nl` command: number lines in a text file in powerful ways. `nl [option] [file]`; by default, blank lines are no numbered - use the `-ba` switch to number all lines.

### File-viewing commands

A pager utility allows you to view one text page at a time and move throgh the text at your own pace - `more` and `less` utilities.

- `more [option] file`: you can move forward through a text file by pressing the spacebar (one page down) or the Enter key (one line down); you _cannot_ move backward through a file.
- `less`: more flexible; allows you to move backward. It allows faster file traversal because it does not read the entire file prior to displaying the file's first page. `esc+V` go back one page. Backward search with `?`; Forward search `/`.
- `head [option] [file]`: by default, it will display the first 10 lines of a text file; display x quantity of lines: `head -n 150 [file]` =  `head -150 [file]`.
- `tail [option] [file]`: a file's last lines, by default the last 10. Use the `-f` switch to follow and see how the file logs are added.

### File-Sumirizing Commands

- `wc`: determining counts in a text file `wc [option] [file]`; without options, wc will display the file's -number of lines -words -bytes in that order.
- `cut`: view particular fields within a file's records `cut option [file]`
  - a text file record is a singgle-file line that ends in a newline linefeed, which is teh ASCII character LF. If your text file records end in the ASCII character NUL (run cat -E filename), you can also use cut on them, but you must use the -z option.
  - text file record demiliter: for some of the cut command options to be properly used, fields must exist within each text file record. these fields are not database-style fields but instead data that is separated by some delimiter. A delimiter is one or more characters that create a boundary between different data items within a record. A single space can be a delimiter.
  - text file changes:the cut command does not change any data within the text file. It simply copies the data you wish to view and displays it to you.
- `uniq`: find repeated text lines in a text file. Uniq will find repeated text lines only if they come right after one another
- `md5 algorithm`: orginally created to be used in cryptography (no longer due to various known vulnerabilities); it's excellent for checking a file's integrity. The md5sum produces a 128-bit hash value. If you copy a file to another system on your network, run the md5sum on the copied file. If you find that the hash values of the original and copied file match, this indicates no file corruption occurred during its transfer. `md5sum file`
- Secure Hash Algorithms (SHA) is a family of various hast functions. Though typically used for cryptography purposes, they can also be used to verify a file's integrity after it's copied or moved to another location. Usually located `/usr/bin/sha???sum` or `/bin/sha???sum` - each utility includes the SHA message digest it employs within its name. the sha512sum utility uses SHA-512 algorithm, which is the best to use for security purposes and is typically employed to hash salted passwords the the /etc/shadow file on Linux

### Regular expressions

A regular expression is a pattern template you define for a utility such as grep, which then uses the pattern to filter text.

The `grep` command is powerful in its use of regex, which will help with filtering text files.

| short | long | description |
| ---- | ----- | ------ |
| -c | --count | Display a count of text file records that contain a PATTERN match. |
| -d action | --directories=action | When a file is a directory, if action is set to read,read the directory as if it were a regular text file; if action is set to skip, ignore the directory; and if action is set to recurse, act as if the - R, -r, or --recursive option was used. |
| -E | --extended-regexp | Designate the PATTERN as an extended regular expression. |
| -i | --ignore-case | Ignore the case in the PATTERN as well as in any text file records. |
| -R, -r | --recursive | Search a directory’s contents, and for any subdirectory within the original directory tree, consecutively search its contents as well (recursively). |
| -v | --invert-match | Display only text files records that do not contain a PATTERN match. |
| -f | -file? | indicate the file that holds the patterns |
| -v | ? | list  of text file records that do not contain the pattern |

`grep [option] pattern [file]`

The grep command returns each file record (line) that contains an instance of the PATTERN.

- .* --> multiple characters
- . --> a single character
- [] --> to represent various characters
- ^ --> find text records that begin with particular characters
- $ --> find text file records where particular characters are at the record's end.

To search for a special character, preced the pattern by \

- grep -F == fgrep
- grep -E == egrep

### Using Streams, Redirection, and Pipes

It is important to know that Linux treats every object as a file. Each file object is identified using a _file descriptor_, an integer that classifies a process's open files. The file descriptor that identifies output from a command or script file is 1; it is also identified by the abbreviation STDOUT.

By default, STDOUT directs output to your current terminal. Your prcess's current terminal is represented by the /dev/tty file.

`>` redirection operator. `>>` append operator

#### Redirecting Standard Error

The file descriptor that identifies a command or script file error is 2. It is also identified by the abbreviation STDERR; by default, it's sent to the terminal. The basic redirection operator to send STDERR to a file is the `2>` operator. `2>>` append.

To send STDERR and STDOUT to the same file, use `&>`. 

To _throw away_ the STDERR you can redirect them to `/dev/null` file (AKA black hole; anything you put into it, you cannot retrieve).

```bash
grep -d skip hsots: /etc/* 2> /dev/null
```

#### Regulating Standard Input

Standard input, by default, comes into your Linux system via the keyboard and/or other input devices. The file descriptor that identifies an input into a command or script file is 0, and it's abbreviation is STDIN. The basic redirection for STDIN is `<`; the `tr` command is one of the few utilities that require you to redirect STDIN.

#### Pipes

With the pipe, you can redirect STDOUT, STDIN, and STDERR between multiple commands all on one command line. The first command is executed; it's STDOUT is redirected as STDIN into the second command

#### Using sed

_Stream editor_. Edit text without having to pull out a full-fledged text editor. A stream editor modifies text that is passed to it via a file or output from a pipeline. This editor uses special commands to make text changes asthe text "streams" through the editor utility.

- `sed`: it edits a stream of text data based on a set of commands you supply ahead of time.

The sed editor changes data based on commands either entered into the command line or stored in a text file.

1. reads one text line at a time from the input stream
2. matches that text with the supplied editor commands
3. modifies the text as specified in the commands
4. displays the modified text

Syntax

`sed [options] [script] [filename]`

By default, sed will use the text from STDIN to modify it according to the specified commands. Example:

`echo 'I like cake' | sed 's/cake/donuts` > `I like donuts`

The sed utility's command (substitute) specifies that if the first text string, cake, is found, it is changed to donuts in te output. Text words delimited via `/` and the SCRIPT is encased in single quotation marks. The example above only removes the _first_ instance of the cake word; to substitute all, you can add and the end of the script `/g`.

The data on a file is _NOT_ changed; the stream editor only displays the modified text to STDOUT.

- To delete lines: syntax `PATTERN/d` for the sed command's script. `sed '/paula/d'` < delete lines that contain 'paula'.
- change an entire line of text `ADDRESScNEWTEXT`; the address refers to the file's line number, and the newtext is the different text line you want displayed. `sed '4cThe cake was a lie' file.txt`

| short | long | description |
| ----- | ------ | -------- |
|-e script | --expression=script | Add commands in script to text processing. The
script is written as part of the sed command. |
|-f script | --file=script | Add commands in script to text processing. The
script is a file.|
| -r | --regexp-extended | Use extended regular expressions in script. |

To run multiple sed commands include a semicolon (;) between the two script commands.

### Generating Command Lines

Methods to create command-line commands: xargs utility. By piping STDOUT from other commands into the xargs utility, you can build command-line commands on the fly.

`ls -1 EmptyFile?.txt | xargs -p /usr/bin/rm`

- xargs -p : stop and ask permission before enacting the constructed command-line command. When using xargs, it's sometimes required to use the absolute path of the command we are trying to use.

`rm -i $(ls EmptyFile?.txt`

- since the ls command is encased by the $() symbols, the filenames, the STDOUT, are passed to the rm -i command, which inquires as whether or not to delete each found file.

### Summary

- the shell program provides the command-line prompt
- there are multiple shell programs, the most popular is the bash shell, typically located in the /bin/bash file.

1. D
2. A
3. D
4. A y C
5. A y D
6. C
7. B
8. E
9. B
10. E
11. C y D
12. D
13. C
14. A C D E
15. E o C?
16. B
17. B y E
18. D - /dev/tty
19. A
20. E

## Chapter 2 - Managing Software and Processes

Linux distributions have created a system for bundling already compiled applications for distribution. This bundle is called a _package_, and it consists of most of the files required to run a single application. You can then install, remove, and manage the entire application as a single package rather than as a group of disjointed files.

Tracking software packages on a Linux system is called _package management_. Linux implements package management by using a database to track the installed packages on the system. The package management database keeps track of not only what packages are installed but also the exact files and file locations required for each application.

- Red Hat package management (RPM)
- Debian package management (Apt)

Each one uses a different method of tracking application packages and files, but they both track similar information:

- application files: the package database tracks each individual file as well as the folder where it's located
- library dependencies: the package database tracks what library files are required for each application and can warn you if a dependent library file is not present when you install a package
- application version: the package database tracks version numbers of applications so that you know whne an updated version of the application is available.

### Using RPM

RPM let's you install, modify, and remove software packages. RH, CentOS and Fedora use RPM, openSUSE. RPM packages have an .rpm extension.

`package-name-version-release.architecture.rpm`

- package-name: name of the software. different distributions may have different package-names
- version: version number and represents software modifications that are more recent than older version numbers
- release: also called build number. It represents a smaller program modification than does the version number.
- architecture: designation of CPU architecture. x86_64 listed for 64-bit processors. Sometimes `noarch` is used to indicate that the package is architectually neutral. Older CPU architecture designations include i386(x86)

```md
There are two types of RPM packages: **source** and **binary**. Most of the time, you'll want the binary package, because it contains the program bundle needed to successfully run the software. A source RPM contains the program's source code, which can be useful for analysis (or for incorporating your own package customizations). You can tell the differenc between these two package file types because a source RPM has `src` as its _architecture_ in the RPM filename

To obtain copies of RPM files on a RH-based distro employ the yumdownloader utility. On openSUSE, you'll need to employ the zypper install -d package-name command.
```

The main tool for working with RPM files is the _rpm_ program. It installs, modifies, and removes RPM software packages.

`rpm action [option] package-file`

rpm command actions

| short | long | description |
| ----- | ------ | -------- |
| -e | --erase | removes the specified package|
| -F | --freshen | upgrades a package only if an earlier version already exists |
| -i | --install | installs the specified package |
| -q | --query | queries whether the specified package is installed |
| -U | --upgrade | installs or upgrades the specified package|
| -V | --verify | verifies whether the package files are present and the package's integrity |

To use the rpm command, you must have the .rpm package file downloaded onto your system. It's common to use the -U action, which installs the new package or upgrades the package if it's already installed.

Adding the -vh option is a popular combination that shows the progress of an update and what it's doing.

Use the -q action to perform a simple query on the package management database for installed packages.

```bash
rpm -q zsh
rpm -q docker
```

rpm command query action options

| short option | long option | description |
| ------ | -------- | -------- |
| -c | --configfiles | lists the names and absolute directory references of package configuration files |
| -i  | --info | provides detailed information, including version, installation date, and signatures |
| N/A | --provides | shows what facilities the package provides |
| -R | --requires | displays various package requirements (**dependencies**) |
| -s | --state | provides states of the different files in a package, such as normal (installed), not installed, or replaced |
| N/A | --what-provides | shows to what package a file belongs |
| -a | --all? | list of all the instlaled packages on the system |
| -p | ? | determine information such as an RPM package's signature or license (from uninstalled package) |

#### Verifying RPM packages

The rpm utility's verify action: if you receive a dot (.) from the `rpm -V <package-name>` command, that's good

| code | description |
| ----- | -------- |
| ? | unable to perform verification tests|
| 5 | digest number has changed |
| c | file is a configuration file for the package |
| D | device number (major or minor) has changed | 
| G | group ownership has changed |
| L | link path has changed |
| missing | missing file |
| M | mode (permission or file type) has changed |
| P | capabilities have changed |
| S | size of file has changed |
| T | time stamp (modification) has changed |
| U | user ownership has changed |

#### Removing RPM packages

To remove an installed package, just use the `-e` action for the rpm command.

#### Extracting data from RPMs

The _rmp2cpio_ utility is helpful to extract files from a RPM package file without installing it. It allows you to build a `cpio` archive from an RPM file. 

1. You need to use the > redirection symbol in order to create the archive file.

```bash
rpm2cpio emacs-24.3-22.el7.x86_64.rpm > emacs.cpio
```

2. Move the files from the cpio archive into directories via the `cpio` command using the `-id` options (-i employs cpy-in mode, which allows files to be copied in from an archive file; -d creates subdirectories in the current working directory whose names match the directory names in the archive, with the exception of adding a precedint dot (.) to each name; the -v option displays what the command was doing as it created the needed subdirectoties and extracted the files)

```bash
cpio -idv < emacs.cpio
```

#### Using YUM

Each linux distribution has its own central clearinghouse of packages, called a _repository_. The repository contains software packages that have been tested and known to install and work correctly in the distribution environment. By placing all known packages into a single repository, the Linux distribution can create a one-stop shopping location for installing all applications.

YUM: YellowDog Update Manager, it allows you to query, install, and remove software packages on your system directly from an official Red Hat directory. The yum command uses the `/etc/yum.repos.d/` directoy to hold files that list the different repositories it checks for packages. Each file in the `yum-repos.d` folder contains information on a repository, such as its URL address and the location of additional package files within the repository. The yum program checks each of these defined repositories for the package requested on the command line.

| Command | Description |
| ------ | ------- |
| check-update | Checks the repository for updates to installed packages |
| clean | Removes temporary files downloaded during installs |
| deplist | Displays dependencies for the specified package |
| groupinstall |   Installs the specified package group|
| info | Displays information about the specified package |
| install | Installs the specified package |
| list | Displays information about installed packages |
| localinstall | Installs a package from a specified RPM file |
| localupdate | Updates the system from specified RPM files |
| provides | Shows to what package a file belongs |
| reinstall | Reinstalls the specified package |
| remove | Removes a package from the system |
| resolvedep | Displays packages matching the specified dependency |
| search | Searches repository package names and descriptions for specified keyword |
| shell | Enters yum command-line mode |
| update | Updates the specified package(s) to the latest version in the repository |
| upgrade | Updates specified package(s) but removes obsolete packages |

Primary YUM configuration file is the `/etc/yum.conf`. This file contains settings (directives) that determine things such as where to record YUM log data.

#### Using ZYpp

openSUSE has its own package management tool called ZYpp (AKA _libzypp_). Its zypper command allows you to query, install, and remove software packages on your system directly from an openSUSE repository. Most common commands:

- help
- install (short: in)
- info
- list-updates
- lr (displays repository information)
- packages (lists all available packages or lists available packages from a specified repository)
- refresh
- remove (short: re)
- search (short: se)
- what-provides
- update
- verify

### Using Debian Packages

#### Debian Package File Conventions

Debian bundles application files into a single .deb package file for distribution that uses the following filename format: `PACKAGE-NAME-VERSION-RELEASE_ARCHITECTURE.deb`. In the architecture you typically find amd64.

#### The _dpkg_ Command Set

The core tool to use for handling .deb files is the _dpkg_ program, which is a cl utility that has options for installing, updating, and removing .deb package files. Command actions:

|Short|Long|Description|
|-----|-------|--------|
|-c | --contents | Displays the contents of a package file|
|-C| --audit| Searches for broken installed packages and suggests how to fix them|
|N/A| --configure| Reconfigures an installed package |
|N/A |--get-selections| Displays currently installed packages|
|-i|--install| Installs the package; if package is already installed, upgrades it|
|-I |--info| Displays information about an uninstalled package file|
|-l |--list| Lists all installed packages matching a specified pattern|
|-L |--listfiles| Lists the installed files associated with a package|
|-p |--print-avail|  Displays information about an installed package|
|-P |--purge| Removes an installed package, including configuration files|
|-r|--remove| Removes an installed package but leaves the configuration files|
|-s |--status| Displays the status of the specified package |
|-S|--search| Locates the package that owns the specified files|

To use the `dpkg` program, you must have the .deb software package available on your system. The Debian distribution also provides a central clearinghouse for Debian packages at <www.debian.org/distrib/packages>.

For missing dependency problems, you can quickly check whether a particular package or library is installed via the dpkg -s action.

Removing a package

1. `-r` action removes the package but keeps any configuration and data files associated with the package installed (useful when reinstalling an existing package and don't want to have to reconfigure things)
2. `-P` to remove the entire package, purges the entire package, including config files and data files from the system

#### Looking at the APT Suite

The Advanced Package Tool (APT) suite is used for working with Debian repositories. This includes the _apt-cache_ program that provides information about the package database, and the _apt-get_ program that does the work of installing, updating and removing packages. New Debian package managent tool: _apt_. It provides improved user interface features and simpler commands; also, easier to understand action names.

the APT suite of tools relies on the `/etc/apt/sources.list` file to identify the locations of where to look for repositories. 

- _apt-cache_ for displaying information about packages
  - depends: display dependencies required
  - pkgnames: all packages installed on the system
  - search
  - showpkg lists information about a specific package
  - stats - package statistics
  - unmet: shows unmet dependencies for all installed packages or the specified installed package
- _apt-get_ - it's what you use to install, update, and remove packages from a Debian package repository.
  - autoclean: removes information about packages that are no longer in the repository
  - check: checks the package management db for inconsistencies
  - clean: cleans up the db and any temporary download files
  - dist-upgrade: upgrades all packages, but monitors for package dependencies
  - dselect-upgrade: completes any package changes left undone
  - install: intalls or updates a package and updates the package management db
  - source: retrieves the source code package for the specified package
  - update: retrieves updated information about packages in the repository
  - upgrade: upgrades all installed packages to newest versions

#### Reconfiguring Packages

_dpkg-reconfigure_ tool: used to return packages to return to the package's initial installation state (say changes that caused serious unexpected problems). _debonf-show_ allows you to view the package's configuration.

### Managing Shared Libraries

#### Library Principles

A system _library_ is a collection of items, such as program functions. _Functions_ are self-contained code modules that perform a specific task within an application, such as opening and reading a data file. The benefit of splitting functions into separate library files is that multiple applications that use the same functions can share the same library files.

Linux supports two different flavors of libraries. One is static libraries (AKA _statically linked libraries_) that are copied into an application when it is compiled. The other flavor is _shared libraries_ (aka _dynamic libraries_) where the library functions are copied into memory and bound to the application when the program is launched. This is called _loading a library_.

#### Locating Library Files

When a program i using a shared function, the system will search for the function's library file in a specific order; looking in directories stored within:

1. LD_LIBRARY_PATH environment variable
   1. modifying this env var by including a program's definition: export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/devops/library/
2. Program's PATH environment variable
3. /etc/ld.so.conf.d/ folder
4. /etc/ld.so.conf file
5. /lib*/ and /usr/lib*/ folders
   1. /lib*/ folders such as /lib/ and /lib64/ libraries needed by system utilities that reside in the /bin/ and /sbin/ directories
   2. /usr/lib*/ folders, such as /usr/lib/ and /usr/lib64/ are for libraries needed by additional software, suchas database utilities like MariaDB

If another library is located in the /etc/ld.so.conf fi le and it is listed above the include operation, then the system will search that library directory before the fi les in the /etc/ld.so.conf.d/ folder. This is something to keep in mind if you are troubleshooting library problems.

#### Loading Dynamically

When a program is started, the _dynamic linker_ (or _dynamic loader_) is responsible for finding th eprogram's needed library functions. After they are located, the dynamic linker will copy them into memory and bind them to the program.

Historically, the dynamic linker executable has a name like ld.so and ld-linux.so*

#### Library Management Commands

##### Managing the Library Cache

The _library cache_ is a catalog of library directories and all the various libraries contained within them. The system reads this cache file to quickly find needed libraries when it is loading programs. This makes it much faster for loading libraries than searching through all the possible direcotory locations for a particular required library file.

When new libraries or library directories are added to the system, this library cache file must be updated. However, it is not a simple text file you can just edit. Instead, you have to employ the _ldconfig_ command.

Typically, when installing software via a package manager, the ldconfig command is run automatically.

- ldconfig -v : see what library files are cataloged.

Troubleshooting shared library dependencies: `ldd <command>` track down missing library files for an application; displays a list of the library files required for the specified app.

### Managing Processes

#### Examining Process Lists

Linux calls each running program a _process_. The linux system assigns each process a _process ID (PID)_ and manages how the process uses memory and CPU time based on that PID. When a Linux system first boots, it starts a special process called the _init process_. The `init` process is the core of the Linux system; it runs scripts that start all of the other processes

##### Viewing Processes with ps

Processes that are currently running: `ps`. By default the ps program shows only the processes that are running in the current user shell.

The basic output of the `ps` command shows the PID assigned to each process, the terminal (TTY) that they were started from, and the CPU time that the process has used. The current ps program used in Linux supports three different styles fo command-line options:

- Unix-style options, which are preceded by a dash
- Berkley Software Distribution (BSD)-style options, which are not prceded by a dash
- GNU long options, which are preceded by a double dash

To see every process running on the system, use the Unix-style -ef option combination, `ps -ef`. This information provides:

- UID: the user responsible for running the process
- PID: process ID of the process
- PPID: parent process OD (if a process was started by another process)
- C: the processor utilization over the lifetime of the process
- STIME: the system time when the process was started
- TTY: the terminal device from which the process was started
- TIME: the cumulative CPU time required to run the process
- CMD: the name of the program that was started in the process

If a process is shown in _brackets_, it means that the process is currently _swapped_ out of physical memory into virtual memory on the hard drive.

##### Understanding Process States

Processes that are swapped into virtual memory are called _sleeping_. Often the Linux kernel places a process into sleep mode while the process is waiting for an event. When the event triggers, the kernel sends the process a signal.

If the process is _interruptible sleep_ mode, it will receive the signal immediately and wake up.

If the process is in _uninterruptible sleep_ mode, it only wakes up based on an external event, such as hardware becoming unavailable. It will save any other _signals_ sent while it was sleeping and act on them once it wakes up.

If a process has eneded but its parent process hasn't acknowledged the termination signal because it's sleeping, the process is considered a _zombie_. It's stuck in a limbo state between running and terminating until the parent process acknowledges the termination signal.

##### Slecting Processes with ps

|     Option(s)                                          |     Description                                                                                     |
|--------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
|     A                                                  |     Display every process on the system   associated with a tty terminal                            |
|     -A, -e                                             |     Display every process on the system                                                             |
|     -C CommandList                                     |     Only display processes running a command in the CommandList                                     |
|     -g GIDList, or -group GIDList                      |     Only display processes whose current effective group is in GIDList                              |
|     -G GIDList, or -Group GIDList                      |     Only display processes whose current real group is in GIDList                                   |
|     -N                                                 |     Display every process except selected processes                                                 |
|     p PIDList, -p PIDList or   --pid PIDList           |     Only display PIDList   processes                                                                |
|     -r                                                 |     Only display selected processes that are in a state of running                                  |
|     -t ttyList, or --tty ttyList                       |     List every process associated with the ttyList terminals                                        |
|     -T                                                 |     List every process associated with the current ttyterminal                                      |
|     -u UserList, or --user UserList                    |     List every process associated with the current tty terminal                                     |
|     -U UserList, or --User UserList                    |     Only display processes whose real user (username or UID) is in UserList                         |
|     x                                                  |     Remove restriction of “associated with a   tty terminal”; typically used with the a   option    |

Groups and users are designated real or effective:

- Real indicates that this is the user or group the account is associated with when logging into the system and/or the primary account's group.
- Effective indicates that the user or group is using a temporary alternative user or group identification, as in the case of SUID and GUID permissions.

If you want ot see _every_ process associated with a particular user or group, it's best to employ both the effective and real options.

##### Viewing Processes with top

The top command displays process information similar to the ps command, but it does it in real-time mode.

The first section of the top output shows general system information. The first line shows the current time, how long the system has been up, the number of users logged in, and the load average on the system.

The load average appears as three numbers: the 1-minute, 5-minute, and 15-minute load averages. The higher the values, the more load the systems is experiencing. If the 15-minute load value is high, your system may be in trouble.

```bash
last pid:  1712;  load avg:  0.63,  0.99,  0.88;  up 38    +06:41:14                                                                                                    06:06:24
120 processes: 119 sleeping, 1 on cpu
CPU states: 97.3% idle,  1.4% user,  1.3% kernel,  0.0% stolen,  0.0% swap
Kernel: 5273 ctxsw, 42 trap, 3171 intr, 2960 syscall, 16 flt
Memory: 40G phys mem, 1841M free mem, 8192M total swap, 8187M free swap

PID   USERNAME  NLWP  PRI NICE  SIZE   RES  STATE     TIME    CPU COMMAND
17860 idmadmin  177   59   0    11G   8064M sleep   265:27  0.26% java
15587 idmadmin  186   59   0   6036M  3307M sleep   190:31  0.48% java
13880 idmadmin  140   59   0   3706M  2794M sleep    20.1H  0.10% java
8864  idmadmin  138   59   0   3665M  1786M sleep   136:45  0.56% java
```

The top utility's second line shows general process information: how many processes are running,sleeping, stopped, or in a zombie state.

The next line shows general CPU information. The top display breaks down the CPU utilization into several categories depending on the owner of the process (user vs system processes) and the state of the processes (running, idle, or waiting).

Following that, in the top utility's output there are two lines that detail the status of the system memory. The first line shows the status of the _physical_ memory in the system, how much total memory there is, how much is currently being used, and how much is free. The second memory line shows the status of the swap memory area in the system (if any is installed) with the same information.

To look at memory usage:

```bash
free -h
      total   used   free   shared buff/cache available
Mem:  3.9G    1.0G   2.2G     30M   710M        2.6G
Swap: 472M     0B     472M
```

- PID: The process ID of the process
- USER: The username of the owner of the process
- PR: The priority of the process
- NI: The nice value of the process
- VIRT: The total amount of virtual memory used by the process
- RES: The amount of physical memory the process is using
- SHR: The amount of memory the process is sharing with other processes
- S: The process status (D = interruptible sleep, I = idle, R = running, S = sleeping, T = traced or stopped, and Z = zombie)
- %CPU: The share of CPU time that the process is using
- %MEM: The share of available physical memory the process is using
- TIME+: The total CPU time the process has used since starting
- COMMAND: The command-line name of the process (program started)

By default, when you start `top`, it sorts the processes based on the %CPU value. You can change the sort order by using servera interactive commands

- z: configures color for the table
- l: toggles display of the load average information line
- t: toggles display of the CPU information ine
- m: toggles display of the MEM and SWAP information lines

A handy little utility for monitoring process information is the `watch` command. To use it, you enter watch and follow it by a command you’d like to enact over and over again. By default watch will reissue the command every two seconds. For example, you can type watch uptime to only monitor the system load. But you aren’t limited to just process tracking commands. You can monitor a directory’s changes in real time and more.

#### Terminal Multiplexer: screen and tmux

Multiplexing refers to the usage of two terminal windows side by side; each terminal is it's own process

A `pts` terminal is a pseudo-terminal. the /# after pts indicates which pseudo-terminal the user is employing

#### Foreground and Background Processes

##### Sending a Job to the Background

Place an ampersand symbol (&) after the command - `sleep 3000 &`. When a  command is sent to the background, the system assigns it a job number (in [brackets]) as well as a PID.

##### Sending multiple jobs to the background

You can start anay number of background jobs from the cl prompt. Each time you start a new job, the shell assigns it a new job number. and the Linux system assigns it a new PID. The plus sign (+) next to the new background job's number denotes the last job added to the background job stack. The minus sign (-) indicates that this particular job is the second-to-last process, which was added to the job stack.

##### Bringing Jobs to the Foreground

To bring a process to the foreground, use the `fg` command and the background job's number, prceded by a percent sign (%) `fg %2`

##### Sending a Running Program to the Background

First pause the process using the Ctrl+Z key combination; this will stop (pause) the program and assign it a job number. After you have the paused program0s job number, employ the bg command to send it to the background.

##### Stopping a job

Stopping a bg job before it has completed: _kill_ command and the job's number preceded by & `kill %1`.

##### Keeping a Job Running after Logout

Each bacckground process is tied to your session's terminal. If the terminal session exits, the brackground process also exits. If you want your script to continue running in background mode after you'be logged off the temrinal, you'll need to emplot the _nohup_ utility. This command will make your background jobs immune to hang-up signals, which are sent to the job when a termina lsession exits. `nohup bash CriticalBackups.sh`

#### Managing Process Priorities

The scheduling priority for a process determines when it obtains CPU time and memory resources in comparison to other processes that opearte at a different priority. However, you may run some applications that need either a higher or lower level of priority.

The _nice_ and _renice_ commands allow you to set and change a program0s _niceness level_, which in turn modifies the priority level assigned by the system to an application The `nice` allows you to start an application with a nondefault niceness level setting. `nice -n VALUE COMMAND`; It allows you to set the value of the priority for the process.

The VALUE parameter is a numberic value from -20 to 19. The lower the number, the higher priority the process receives. The default niceness level is zero.

The COMMAND argument indicates the program must start at the specified niceness level.

To change the priority of a process that's already running, use the _renice_ command: `renice PRIORITY [-p PIDS] [-u USERS] [-g GROUPS]`; This command allows you to change the priority of multiple processes based on a list of PID values, all of the processes started by one or more users, or all of the processes started by one or more groups.

`# sudo renice -10 -p 1949`
`# 1949 (process ID) old priority -5, new priority -10`

Only if you have super user privileges can you set a nice value less than 0 (increase the priority) of a running process.

```bash
# starting a process
nice -10
# PID 10
# starting a process and giving it a value of -10
sudo nice --10
```

#### Sending Signals to Processes

In Linux, processes communicate with each other using process signales. A _process signal_ is a predefined message that processes recognize and may choose to ignore or act on. A few of these signals:

|Number| name | description|
|-------|-------- | ------- |
|1| HUP| hangs up|
|2| INT| interrupts|
|3| QUIT| stops running|
|9| KILL| Unconditionally terminates|
|11| SEGV| segments violation|
|15| TERM| terminates if possible|
|17| STOP| stops unconditionally, but doesn't terminate|
|18| TSTP| stops or pauses, but continues to run in background|
|19| CONT| resumes execution after STOP or TSTP|

You'll often see the Linux process signals written with SIG attached to them. For example, TERM is also written as SIGTERM, and KILL is also SIGKILL.

#### Sending Signals with the KILL Command

By default the `kill` command sends a TERM signal to all the PIDs listed on the command line.

To send a process signal, you must either be the owner of the process or have super user privileges. The TERM signal only asks the process to _kindly_ stop running. To kill a process running in the background, we can use the job number, preceeded by a percent sign `kill -9 %1`. When processes ignores de request, we need to get **forceful**: use the `-s` option to specify other signals.

It is generally accepted procedure to first try thee TERM signal. If the process ignores that, try the INT or HUP signal. These signal try to gracefully stop doing what it was doing before shutting down.

#### Sending Signals with the killall Command

The kill command only accepts the process PID; the _killall_ command can select a process based on the command it is executing and send it a signal. Similar to kill, if no signal is specified, TERM is sent.

#### Sending Signals with the pkill Command

We can send signals by defining user-name, user ID (UID), terminal with which the process is associated, and so on. We can also use wildcard characters. `-t` option is used to see all running processes by their termianl (reguarly used with pgrep to see the output of what we are about to kill). Like the other signal-sending utilities, the pkill command by default sends a TERM signal.

### EXAMN

1. E, A
   1. A, B, D, E
2. E
3. E, C
4. A
5. C, D
6. D
7. A
8. C
9.  B
10. C, E, B
    1.  C, D E
11. A, C, D
12. D
13. A
14. E (boleo)
15. B (boleo)
    1.  D
16. B
17. A
18. B
19. C
20. D

17/20

## Chaper 3 - Configuring Hardware

pag183pdf





 


