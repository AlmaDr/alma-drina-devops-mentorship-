**Level 0:**

**The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.**

*Solution:* 
user@host -p 

$ ssh bandit0@bandit.labs.overthewire.org -p 2220 

$ ssh [ip or hostname] #Secure shell, an encrypted network protocol
#allowing for remote login and command execution
![l0](https://user-images.githubusercontent.com/72069598/232613268-80573dd2-797a-48d4-a018-6e781e79dcfd.png)

**Bandit Level 0 → Level 1**

*Level Goal*

**The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.**

*Solution:*

$ ls # Directory listing

$ cat readme #Display the contents of readme


![l0-1](https://user-images.githubusercontent.com/72069598/232613521-2b279f9b-8ec7-4a7a-bdc7-a97c0ba49bee.png)
**Bandit Level 1 → Level 2**

*Level Goal*

**The password for the next level is stored in a file called - located in the home directory**

*Solution:*

Special character - so we used cat ./- view the content of the file  


![l1-2](https://user-images.githubusercontent.com/72069598/232613707-83e26161-4479-4819-a005-a4bfb6059729.png)

**Bandit Level 2 → Level 3**

*Level Goal*

**The password for the next level is stored in a file called spaces in this filename located in the home directory**

*Solution:*

We use command cat „spaces in this filename“ to avoid white spaces 

![l2-3](https://user-images.githubusercontent.com/72069598/232613817-bd938fc2-eda3-4754-b693-e73d6ce0de45.png)

**Bandit Level 3 → Level 4**

*Level Goal*

**The password for the next level is stored in a hidden file in the inhere directory.**

*Solution:*

$ ls -la #list  

$ cd inhere #move to the directory inhere  

$ cat .hidden # show the content of the hidden file

![l3-4](https://user-images.githubusercontent.com/72069598/232613868-0ae4f3f6-daf1-4c21-b30b-896d65c5c941.png)


**Bandit Level 4 → Level 5**

*Level Goal*

**The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.**


*Solution:*

$ cd inhere # move to folder inhere
$ file ./* # use file command to check which file content is in Human Readable format
$ cat ./-file07 #from the list we see that file07 is ASCII text – which is human-readable file 

![4-5](https://user-images.githubusercontent.com/72069598/232613925-2e5e76a2-5754-432c-af7d-67aa1445d558.png)


**Bandit Level 5 → Level 6**

*Level Goal*

**The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

**human-readable**

**1033 bytes in size**

**not executable**

*Solution:*

$ cd inhere

$ find . -type f -readable -size 1033c ! -executable 

- type to specify the type f 
- readable human-redable file
- size 1033c the size of the file, c referts to bytes
- ! -executable  matches the executable file

![l5-6](https://user-images.githubusercontent.com/72069598/232613979-b3dad1ce-8f6e-4533-a40c-dc873f14a68d.png)


**Bandit Level 6 → Level 7**

*Level Goal*

**The password for the next level is stored somewhere on the server and has all of the following properties:**

**owned by user bandit7**

**owned by group bandit6**

**33 bytes in size**

*Solution:*

$ find / -user bandit7 -group bandit6 -size 33c 2>&1 | grep  -F -v Permission | grep -F -v directory
$ cat /var/lib/dpkg/info/bandit7.password #print out the files 

- find / - search the entire filesystem.
- type f -user bandit7 -group bandit6 - for a file owned by user bandit7 and group bandit6.
- 33c - file must be 33 bytes in size.
- 2>/dev/null - added to redirect error messages to /dev/null so that we only see the output of the command.


![l6-7](https://user-images.githubusercontent.com/72069598/232614014-fdbde5e6-5e26-4ff4-bb4c-9ea4d0a7a538.png)

**Bandit Level 7 → Level 8**

*Level Goal*

**The password for the next level is stored in the file data.txt next to the word millionth**

*Solution:* $ grep millionth data.txt # we use this command to search file data.txt with word millionth


![l7-8](https://user-images.githubusercontent.com/72069598/232614080-b4ddfd32-d856-4cc0-a64e-f7cd1c51267c.png)

**Bandit Level 8 → Level 9**

*Level Goal*

**The password for the next level is stored in the file data.txt and is the only line of text that occurs only once**

*Solution:*
$ sort data.txt | uniq -u # command filters out duplicate lines in a text file and outputs unique lines, with -u it will output those lines that occur EXACTLY once.

![l8-9](https://user-images.githubusercontent.com/72069598/232614131-8c8095f0-0545-4484-bfc5-e41e863b07a3.png)

**Bandit Level 9 → Level 10**

*Level Goal*

**The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.**

*Solution:*
$ strings data.txt | grep ==  # Command strings print the sequences of printable characters in files and grep = will print lines with ‘=’ in it

![l9-10](https://user-images.githubusercontent.com/72069598/232614199-c5638c68-b34c-414a-8861-c34995c28c20.png)
