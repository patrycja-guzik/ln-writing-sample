# Linux `ln` command overview
*This section provides basic information on the `ln` command and its usage.*

`ln` (*link*) is one of the commands you can write in the Linux [shell](#Shell).

The most basic usage of the `ln` command allows you to create a link file (`link-name`) to your current file (`file-name`):
```
$ ln file-name link-name
```
There are a few additional syntax options you can use:

|Syntax|Explanation|
| ------------- | ------------- |
|`ln file-name link-name`| Creates a hard link to the file with the name provided by the user.|
|`ln file-name`| Creates a hard link in the current directory. The link name will be the same as the file name.|
|`ln file-name directory`| Creates a hard link in the directory given by the user. The link name will be the same as the file name.|

> **Note:**
By default, the `ln` command creates hard links. To create a symbolic link, use the `-s` [argument](#command-options).

Typically, `ln` does not replace existing files. If you would try to create a link with a `link-name` of an existing file, you will get an error:
```
ln: failed to create hard link 'link.txt': File exists
```
Use the `-f` (*force*) [argument](#command-options) to replace an existing file.

## Hard links overview
*This section provides basic information on hard links.*

Links are a method to refer to a file stored on the hard drive. They are a part of a file system that organizes directories and files.

A hard link is an exact copy of an existing file. It shares the same [inode](#inode), so the information on the file and its attributes (such as type of a file, size, physical address, or ownership).

> **Note:**
Hard links do not use extra memory as they do not create a physical copy of the file. They serve as an additional way to access the original file stored in the [inode](#inode).

![hardlinks](hard.jpg?raw=true "Hard links")

The hard link points directly to the file's [inode](#inode), not the file itself. Because of that, you can change the original file's contents or its location, and your hard link will still work. You can even remove the original file, and it will be accessible through the hard link. It will not become invalid.

## Symbolic links overview
*This section provides basic information on symbolic links.*

A symbolic link is a special file version that points to another file. It can be compared to the shortcut, popular in Microsoft Windows systems. Unlike a hard link, a symbolic link does not contain the data in the target file. It points to another entry somewhere in the file system. If the file or directory that the symbolic link points to gets deleted, the link becomes invalid.

![symlinks](soft.jpg?raw=true "Symbolic links")

# Practising link creation
*This procedure provides exercises to practice hard and symbolic links creation.*

**Prerequisites:**
- Access to a Linux [shell](#Shell)

**Procedure:**
1. Set up example directories and files.
2. Create a hard link to an existing file.
3. Create a symbolic link to an existing file.

**Result:**
Hard and symbolic links to the example files are created. 

## Setting up example directories and files
*This procedure describes example directories and files creation.*

**Prerequisites:**
- Access to a Linux [shell](#Shell)

**Procedure:**
1. Create a new `practice` directory using the `mkdir` command.
    ```
    $ mkdir -p /tmp/practice/
    ```
    > **Tip:**
    Create your practice files in the temporary (`/tmp/`) directory. The next time your PC boots up, all files and directories will be deleted.

2. Create the two example files using the `touch` command.
    ```
    $ touch file1.txt file2.txt
    ```

**Result:**
A new directory and two example files are created.

## Creating a hard link to an existing file
*This procedure describes a hard link creation.*

**Prerequisites:**
- Example directory and files are created

**Procedure:**
1. Go to the `practice` directory using the `cd` command.
    ```
    $ cd /tmp/practice
    ```
2. Create a hard link, within the current directory, to an `example1.txt` file using the `ln` command.
    ```
    $ ln example1.txt link1.txt
    ```
3. Optional: Check if the hard link was created correctly by checking the [inode](#inode) number, using the `ln -i` command.
    ```
    $ ls -i file1.txt link1.txt 
    ```
    **Expected output:**
    Files have the same [inode](#inode) number.
    ```
    522316 file1.txt  522316 link1.txt
    ```

**Result:**
A new file with the same [inode](#inode) number is created.

## Creating a symbolic link to an existing file
*This procedure describes a symbolic link creation.*

**Prerequisites:**
- Example directory and files are created

**Procedure:**
1. Go to the `practice` directory using the `cd` command.
    ```
    $ cd /tmp/practice
    ```
2. Create a symbolic link, within the current directory, to an `example2.txt` file using the `ln -s' command.
    ```
    $ ln -s example2.txt link2.txt
    ```
3. Optional: Check if the symbolic link was created correctly by checking the [inode](#inode) number using the `readlink` command.
    ```
    $ readlink link2.txt
    ```
    **Expected output:**
    ```
    file2.txt
    ```

**Result:**
A new symlink file is created. 

# Glossary

## inode
The [inode](#inode) is a database that uniquely describes a file with its attributes. Every newly created file receives a new [inode](#inode) number.

## Command options
Command options (also known as command arguments) are a list of parameters that can control the command's behavior. Options can add additional actions to a command or change its behavior.

## Shell
Shell is a command-line interface that directly exposes you to the operating system internals. It interprets your commands and passes the information on what to do with them to the operating system.
