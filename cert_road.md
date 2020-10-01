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

An external command command is indicated by the type command displaying the program'sd absolute directory reference within the virtual directory structure.

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

You can reverse any modifications you make to the variable by using the unset command.

67/688