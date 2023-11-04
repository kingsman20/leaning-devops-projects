# Introduction to Linux and basic commands 

Linux is a family of open-source Unix operating system based on the Linux Kernel. As well include Red Hat,Debian,openSUSE,Fedora,and Ubuntu.

## What is Linux command?

A linux command is a program or utility that runs on the CLI- a console that interacts with the system via texts and processes. It's similar to the Command Promt application in Windows and the Terminal application in Mac.

Linux commands are executed on Terminal by pressing Enter at the end of the line. The commands perform various tasks. They are case sensitive, and are of three parts; CommandName(the rule that you want to perform), Option or Flag(modifies a commands operations and invoked by hypens"-"or double hypens "--") and Parameter or argument(specifies any necessary information for the command).

## Connected to my AWS ubuntu instance
<img width="1208" alt="Screenshot 2023-11-04 at 3 50 11 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4fe44463-24fb-41cd-a8e5-80c1e45ebc05">

## File Manipulation

### 1. `sudo` command:

Short for superuser do. Lets you perform tasks the require administrative or root permissions. 

`sudo apt upgrade` 
<img width="1214" alt="Screenshot 2023-11-04 at 3 59 32 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/7c4e92d4-32cd-425f-87a1-c971c251f36a">

### 2. `pwd` command:

Used to find the path of your Present Working Directory. Simply entering pwd will return full current path - a path of all the directories that starts with a forward slash(/).
<img width="483" alt="Screenshot 2023-11-04 at 4 00 25 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/8d8b2034-e121-4f66-b9db-af5adc9d028c">

### 3. `cd` command:
 
To navigate through the Linux files and directories, use the cd command. Depending on your current working directory, it requires either the full path or the directory name.


`cd LinuxCommand`

<img width="773" alt="Screenshot 2023-11-04 at 4 12 18 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/f898803f-3044-4010-b411-e153f730e3d6">


`cd ..`

<img width="1002" alt="Screenshot 2023-11-04 at 4 14 34 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/23a91f31-e885-4310-bb53-327c029a7db5">


### 4. `ls` command:

The ls command lists files and directories within a system/interface. Running it without a flag will show current working directory's content.

`ls`

<img width="367" alt="Screenshot 2023-11-04 at 4 01 07 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/9b9d2651-21dd-40ab-a215-7fdb8b6a75f7">


`ls -a`

<img width="1059" alt="Screenshot 2023-11-04 at 4 01 48 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/d89a0a31-fe2e-4083-968e-b1ca486609ed">


`ls -lh`

<img width="1208" alt="Screenshot 2023-11-04 at 4 02 50 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/c0f1c351-12b5-44c4-87cd-c8ccc932b9b4">

### 5. `cat` command:

Concatenate, or cat, is one of the most frequently used Linux commands. It lists, combines, and writes file content to the standard output. To run the cat command, type cat followed by the file name and its extension.

`cat file1.txt`

<img width="1097" alt="Screenshot 2023-11-04 at 4 51 14 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/f4b26aac-1226-4553-8de0-c4dc69246960">

`cat file1.txt > file2.txt`

<img width="1056" alt="Screenshot 2023-11-04 at 4 52 24 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/3c3bf525-e4a0-4628-9b7d-a66e3aae6534">

### 6. `cp` command:

Use the cp command to copy files or directories and their content. Take a look at the following use cases.

`cp file1.txt file2.txt`

<img width="1019" alt="Screenshot 2023-11-04 at 4 54 29 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4983ff3f-d43e-4207-9fa8-0eaf294aaa19">

### 7. `mv` command:

The primary use of the mv command is to move and rename files and directories. Additionally, it doesn’t produce an output upon execution.

`mv file1.txt file2.txt`

<img width="1086" alt="Screenshot 2023-11-04 at 4 56 09 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/62371698-8e02-41cb-bc8e-1a7517887ad1">


### 8. `mkdir` command:

Use the mkdir command to create one or multiple directories at once and set permissions for each of them. The user executing this command must have the privilege to make a new folder in the parent directory, or they may receive a permission denied error.


`mkdir music`

<img width="909" alt="Screenshot 2023-11-04 at 4 57 25 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/089bdde7-10f4-4a76-9167-a6d0f9ba87b0">

<img width="715" alt="Screenshot 2023-11-04 at 4 58 13 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/bc060536-b0a8-4166-9eb9-5cebae775f77">

### 9. `rmdir` command:

To permanently delete an empty directory, use the rmdir command. Remember that the user running this command should have sudo privileges in the parent directory.

`rmdir -p music/songs`

<img width="746" alt="Screenshot 2023-11-04 at 5 00 11 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/075be3bd-51e4-4020-8431-14072fe7f208">



### 10. `mkdir` command:

The rm command is used to delete files within a directory. Make sure that the user performing this command has write permissions.

`rm file2.txt`

<img width="747" alt="Screenshot 2023-11-04 at 5 02 11 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/6696cf88-6498-4258-8633-96035bf3ffcd">


### 11. `find` command:

The find command is used to search for files within a specific directory and perform specific operations.
For example, you want to look for a file called file2.html within the home directory and its subfolders:

`find /home -name file1.txt`

<img width="965" alt="Screenshot 2023-11-04 at 5 10 47 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/53be2a54-4ca0-43a1-afa3-6ea6d47e7866">

### 12. `find` command:

This command grep or global regular expression print lets you find a word by searching through large log file.

`grep line file1.txt`

<img width="706" alt="Screenshot 2023-11-04 at 5 13 08 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/9052f9e3-4c05-4431-a9fc-4bdb8cedb566">


### 13. `df` command:

This command df gives report of the system's disk space usage, shown in percentage and kilobyte(KB).

`df`

<img width="923" alt="Screenshot 2023-11-04 at 5 14 17 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/bb8c1226-4de5-4eee-bb51-458255ea2c09">


### 14. `du` command:

If you want to check how much space a file or diectory takes up, use the du command. You can run this command to identify which part of the system uses the storage excessively.

`du`

<img width="759" alt="Screenshot 2023-11-04 at 5 15 30 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/825bb682-6e26-4fbc-a260-f345ff5084ba">


### 15. `head` command:

The head command allows you to view the first ten(which can be changed by adding an option) lines of a text. It's also used to output piped data to the CLI.

<img width="799" alt="Screenshot 2023-11-04 at 5 16 34 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/93b91ffb-c4e1-48d1-88d5-43216af908ef">


### 16. `info` command:

This command gives you an meaning and function of a command.

<img width="1101" alt="Screenshot 2023-11-04 at 5 18 48 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/81c3da23-062e-4f5b-8b63-77c4135d8475">


### 17. `which` command:

This command is used to locate executable file associated with the given command by searching it in the path enviroment.

`which sudo`

<img width="554" alt="Screenshot 2023-11-04 at 5 20 13 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/852edde5-8733-4254-a89d-8b83d5dbb669">

### 17. `diff` command:

Short for difference, the diff command compares two contents of a file line by line. After analyzing them, it will display the parts that do not match.

`diff file1.txt file2.txt`

<img width="835" alt="Screenshot 2023-11-04 at 5 22 18 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4cccaa73-cd5f-4db9-b980-ca8435712a53">


### 17. `nano` command:

Linux allows users to edit and manage files via text editors such as nano,vi and jed.

<img width="1099" alt="Screenshot 2023-11-04 at 5 46 03 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/bb970f3c-06ae-4b00-9eaf-0ab4ff3bdbde">


### 18. `ps` command:

ps lists the signals or running processes

<img width="944" alt="Screenshot 2023-11-04 at 5 57 37 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/e208e4df-9874-4706-b35e-1882438e9eb3">


### 19. `wget` command:

This command line lets you download files from the internet.

<img width="1105" alt="Screenshot 2023-11-04 at 6 00 14 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/735e342c-fee2-424e-bd0b-603f22311226">

### 20. `uname` command:

The uname or unix name command will print detailed information about your Linux system and hardware. This includes the machine name, operating system, and kernel. To run this command, simply enter uname into your CLI.

<img width="553" alt="Screenshot 2023-11-04 at 6 01 25 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/7061b6a3-f44b-4d20-806f-1cffb7789ab2">

### 21. `history` command:

With history, the system will list up to 500 previously executed commands, allowing you to reuse them without re-entering. Keep in mind that only users with sudo privileges can execute this command. How this utility runs also depends on which Linux shell you use.

<img width="940" alt="Screenshot 2023-11-04 at 6 02 55 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/687b4fe7-990f-4d0e-9d8e-c095bcefe0d6">

### 22. `man` command:

The man command provides a user manual of any commands or utilities you can run in Terminal, including the name, description, and options.

<img width="1094" alt="Screenshot 2023-11-04 at 6 04 10 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/038cfd55-1d64-4f0d-b9f3-f3030db2edb9">

