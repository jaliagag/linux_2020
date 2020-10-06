# LPIC-101&&102.v5

[Study file](LPIC-1%20Linux%20Professional%20Institute%20Certification%20Study%20Guide%20Exam%20101-500%20and%20Exam%20102-500%20by%20Christine%20Bresnahan,%20Richard%20Blum%20(z-lib.org).pdf)

- LINKS
  - <https://www.booleanworld.com/guide-linux-top-command/>
  - <https://www.certdepot.net/>

## Chapter 1

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

### Regualr expressions

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

55/105


