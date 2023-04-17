Level 0:
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

Solution: 
user@host -p 
$ ssh bandit0@bandit.labs.overthewire.org -p 2220 
$ ssh [ip or hostname] #Secure shell, an encrypted network protocol
                       #allowing for remote login and command execution


Bandit Level 0 → Level 1
Level Goal
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Solution:
$ ls # Directory listing
$ cat readme #Display the contents of readme


Bandit Level 1 → Level 2
Level Goal
The password for the next level is stored in a file called - located in the home directory

Solution:
-	Is special character so we used cat ./- view the content of the file  


Bandit Level 2 → Level 3
Level Goal
The password for the next level is stored in a file called spaces in this filename located in the home directory

Solution: We use command cat „spaces in this filename“ to avoid white spaces 


Bandit Level 3 → Level 4
Level Goal
The password for the next level is stored in a hidden file in the inhere directory.

Solution:
$ ls -la #list  
$ cd inhere #move to the directory inhere  
$ cat .hidden # show the content of the hidden file


Bandit Level 4 → Level 5
Level Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Solution:
$ cd inhere # move to folder inhere
$ file ./* # use file command to check which file content is in Human Readable format
$ cat ./-file07 #from the list we see that file07 is ASCII text – which is human-readable file 


Bandit Level 5 → Level 6
Level Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
human-readable
1033 bytes in size
not executable

Solution:
$ cd inhere
$ find . -type f -readable -size 1033c ! -executable 

- type to specify the type f 
- readable human-redable file
- size 1033c the size of the file, c referts to bytes
- ! -executable  matches the executable file


Bandit Level 6 → Level 7
Level Goal
The password for the next level is stored somewhere on the server and has all of the following properties:
owned by user bandit7
owned by group bandit6
33 bytes in size

Solution:
$ find / -user bandit7 -group bandit6 -size 33c 2>&1 | grep  -F -v Permission | grep -F -v directory
$ cat /var/lib/dpkg/info/bandit7.password #print out the files 

- find / - search the entire filesystem.
-type f -user bandit7 -group bandit6 - for a file owned by user bandit7 and group bandit6.
- 33c - file must be 33 bytes in size.
- 2>/dev/null - added to redirect error messages to /dev/null so that we only see the output of the command.


Bandit Level 7 → Level 8
Level Goal
The password for the next level is stored in the file data.txt next to the word millionth

Solution: $ grep millionth data.txt # we use this command to search file data.txt with word millionth


Bandit Level 8 → Level 9
Level Goal
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Solution: 
$ sort data.txt | uniq -u # command filters out duplicate lines in a text file and outputs unique lines, with -u it will output those lines that occur EXACTLY once.


Bandit Level 9 → Level 10
Level Goal
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Solution:
$ strings data.txt | grep ==  # Command strings print the sequences of printable characters in files and grep = will print lines with ‘=’ in it
