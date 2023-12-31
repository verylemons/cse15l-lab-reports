**CSE 15L Lab Report 1**

**Kwae Htoo, A17327141**

**Share an example of using the command with no arguments.**
*No argument means that you just type in "cd", "ls", and "cat" in the terminal and nothing after it.*

![Image](1.png)

Using "CD" without an argument takes us back to the home directory or the previous directory. For example, if you are in the folder path home/images/myself. When you use "cd", you will be taken back to the previous directory which is images (home/images). However, if you are at the home directory, you cannot go back any further, therefore, if you use "cd", nothing will happen.

![Image](2.png)

Using "ls" without an argument lists all the files and folders in the current directory.

![Image](3.png)

Using "cat" without an argument makes it wait for an input. Once you type and input something, it will print out what you just put on the terminal. This is not an error because since there's no argument/file to read from, "cat" will read from the standard input instead which is what you type in the terminal.

**Share an example of using the command with a path to a directory as an argument.**
*With a path to a directory means that after typing "cd", "ls", and "cat", you also type in a directory name.*

![Image](4.png)

Using  "cd" with a path to a directory as an argument changes the current directory to the chosen directory. You cannot access directories that are not in the current directory or else the terminal will display an error message: "no such directory or file."

![Image](5.png)

Using "ls" with a path to a directory as an argument shows all the files/folders that are within the chosen directory. You cannot use "ls" to access directories that are not within the current directory or else the error message, "no such file or directory", will be displayed.

![Image](6.png)

Using "cat" with a path to a directory as an argument prints information that the chosen directory is a directory. "cat" will tell you what the argument type is. Since we have a path to a directory as our argument, then "cat" will display that the chosen directory is a directory. You cannot use "cat" and add a directory that is outside the current directory. If you do so, this will cause an error and the error message "No such file or directory" will be displayed.

**Share an example of using the command with a path to a file as an argument.**
*With a path to a file as an argument means that after typing in "cd", "ls", and "cat", you also type a file name after the initial command.*

![Image](7.png)

Using "cd" with a path to a file as an argument with print out the error message: "not a directory." Since "cd" stands for "change directory," trying to pass a file as an argument will prompt the error message because a file is not a directory.

![Image](8.png)

Using "ls" with a path to a file as an argument will print out the file name. You cannot use "ls" on files that are outside of the current directory or else an error message will be displayed.

![Image](9.png)

Using "cat" with a path to a file as an argument will print out the contents in the file. You cannot access files that are outside of the current directory or else an error message will be displayed.
