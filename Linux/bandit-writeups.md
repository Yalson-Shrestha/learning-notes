## Level 0
- **Task:** SSH into bandit.labs.overthewire.org using user `bandit0`.  
- **Command used:** ssh bandit0@bandit.labs.overthewire.org -p 2220
- **Learning**: First time using SSH with custom port. Default SSH is port 22, here it’s 2220.

## Level 0 to 1
- **Task:**  The password for the next level is stored in a file called `readme` located in the home directory. Use this password to log into bandit1 using SSH on port 2220.
- **Command used:** cat readme
- **Learning**: the ls command lists files, and cat displays file content.
Password found: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

## Level 1 to 2
- **Task:**  The password for the next level is stored in a file called - located in the home directory
- **Command used:** ls -la , cat ./-
- **Learning**: How to handle strange filenames (like -) by using ./filename or -- to end options.
Password found: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

## Level 2 to 3
- **Task:**  The password for the next level is stored in a file called --spaces in this filename-- located in the home directory
- **Command used:** ls -la , cat -- "--spaces in this filename--"
- **Learning**: How to work with filenames that include spaces: quoting and escaping.
                More practice with SSH, ls, cat and careful shell quoting.
Password found: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

## Level 3 to 4
- **Task:**  The password for the next level is stored in a hidden file in the inhere directory.
- **Command used:** ls -la , cat './...Hiding-From-You'
- **Learning**: How to handle files with unusual names (leading dots, spaces, dashes) using quoting or ./.
                Practical use of file and strings to safely inspect unknown files.
Password found: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

## Level 4 to 5
- **Task:**  The password for the next level is stored in the only human-readable file in the inhere directory.
- **Command used:** file ./-file*
- **Learning**: How to handle filenames starting with - by using ./filename.
                How to quickly check multiple files with the file command.
Password found: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

## Level 5 to 6
- **Task:**  The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
human-readable
1033 bytes in size
not executable
- **Command used:** find . -type f -size 1033c ! -executable
- **Learning**: How to combine find filters (-type, -size, permission tests) to locate files meeting several criteria.
Password found: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

## Level 6 to 7
- **Task:**  The password for the next level is stored somewhere on the server and has all of the following properties:
owned by user bandit7
owned by group bandit6
33 bytes in size
- **Command used:** find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
- **Learning**: Using find with ownership filters (-user, -group) and searching system-wide from root /
Password found: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

## Level 7 to 8
- **Task:**  The password for the next level is stored in the file data.txt next to the word millionth
- **Command used:** grep millionth data.txt
- **Learning**: Using grep to search for specific text patterns in files and extract adjacent data
Password found: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

## Level 8 to 9
- **Task:**  The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
- **Command used:** sort data.txt | uniq -u
- **Learning**: Using sort and uniq commands together with pipes to find unique lines in a file
Password found: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

## Level 9 to 10
- **Task:**  The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
- **Command used:** strings data.txt | grep "=="
- **Learning**: Using strings to extract text from binary files and grep with pattern matching
Password found: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

## Level 10 to 11
- **Task:**  The password for the next level is stored in the file data.txt, which contains base64 encoded data
- **Command used:** base64 -d data.txt
- **Learning**: base64 -d to decode base64 encoded data and extract hidden information
Password found: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

## Level 11 to 12
- **Task:**  The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
- **Command used:** cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
- **Learning**: Using tr command for character translation and understanding ROT13 cipher
Password found: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

## Level 12 to 13
- **Task:**  The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)
- **Command used:** - mktemp -d (create temp directory)
                    - xxd -r data.txt > file (reverse hexdump)
                    - Multiple decompression cycles:
                    - gzip -d, bzip2 -d, tar xf
                    - Repeated file command to identify next compression type
- **Learning**: Working with hexdumps, multiple compression formats, iterative decompression, and temporary directories
Password found: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

## Level 13 to 14
- **Task:**  The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on
- **Command used:** - ssh -i sshkey.private bandit14@localhost -p 2220
- **Learning**: Using SSH keys for authentication instead of passwords, accessing restricted files
Password found: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

## Level 14 to 15
- **Task:**  The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
- **Command used:** - telnet localhost 30000 then pasted bandit14's password
- **Learning**: Telnet, Network communication with services on specific ports
Password found: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

## Level 15 to 16
- **Task:**  The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.
- **Command used:** - openssl s_client -connect localhost:30001
- **Learning**: Using SSL/TLS encrypted connections with openssl s_client
Password found: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

## Level 16 to 17
- **Task:**  The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
- **Command used:** - nmap, openssl s_client -connect localhost:31790 -quiet
- **Learning**: Port scanning, SSL service identification, private key authentication
Password found: EReVavePLFHtFlFsjn3hyzMlvSuSAcRD

## Level 17 to 18
- **Task:**  There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
- **Command used:** - diff passwords.old passwords.new
- **Learning**: Using diff to compare files and interpret the output ( < for first file, > for second file)
Password found: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

## Level 18 to 19
- **Task:**  The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
- **Command used:** - ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
- **Learning**: Bypassing shell initialization by passing commands directly to SSH
Password found: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

## Level 19 to 20
- **Task:**  To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
- **Command used:** - ./bandit20-do cat /etc/bandit_pass/bandit20
- **Learning**: Using setuid binaries for privilege escalation to access restricted files
Password found: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

## Level 20 to 21
- **Task:**  There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
- **Command used:** - echo "bandit20-password" | nc -l -p 1234 (set up listener)
                    - ./suconnect 1234 (connect to listener in another terminal)
- **Learning**: Network communication via localhost, using netcat as a simple server
Password found: EeoULMCra2q0dSkYj561DX7s1CpBuOBt

## Level 21 to 22
- **Task:**  A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
- **Command used:** - ls /etc/cron.d/,
                    -  cat cronjob_bandit22,
                    -  cat /usr/bin/cronjob_bandit22.sh
- **Learning**: Investigating cron jobs and understanding automated script execution
Password found: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q

## Level 22 to 23
- **Task:**  A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
- **Command used:** - cat /usr/bin/cronjob_bandit23.sh,
                    - echo "I am user bandit23" | md5sum | cut -d ' ' -f 1 (calculated the target filename),
                    - cat /tmp/[md5-hash] (read the password file)
- **Learning**: Investigating cron jobs and understanding automated script execution
Password found: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga

## Level 23 to 24
- **Task:**  A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
- **Command used:** - Created script in /tmp that copies /etc/bandit_pass/bandit24 to a readable location
                    - Copied script to /var/spool/bandit24/foo/ where cron job executes it
- **Learning**: Writing shell scripts, understanding cron job execution, file permissions, and privilege escalation through script execution
Password found: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8

## Level 24 to 25
- **Task:**  A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
- **Command used:** - Created brute force script with for pin in {0000..9999} and nc localhost 30002
- **Learning**: Basic brute forcing, generating number sequences, automation with bash scripts
Password found: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

## Level 25 to 26
- **Task:**  Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.
- **Command used:** - cat /etc/passwd | grep bandit26
                    - cat /usr/bin/showtext
                    - ssh bandit26@localhost -p 2220 -i bandit26.sshkey (with small terminal window)
                    - Press 'v' in more to enter vi
                    - In vi: :set shell=/bin/bash
                    - :shell
                    - cat /etc/bandit_pass/bandit26
- **Learning**: How restricted shells work, Exploiting pager programs (more) and editors (vi) for privilege escalation, The importance of understanding program behavior in different environment
Password found: s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ

## Level 26 to 27
- **Task:**  Good job getting a shell! Now hurry and grab the password for bandit27!
- **Command used:** - ./bandit27-do cat /etc/bandit_pass/bandit27
- **Learning**: Escaping restricted shells, exploiting more and vim to get system access, using setuid binaries
Password found: upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB

## Level 27 to 28
- **Task:**  There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27. Clone the repository and find the password for the next level.
- **Command used:** - git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
                    - cd repo
                    - cat README
- **Learning**: Working with git repositories over SSH, basic git commands
Password found: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN

## Level 28 to 29
- **Task:**  Clone git repository and find password (in commit history)
- **Command used:** - git clone, git log, git show, git log -p
- **Learning**: Examining git history, viewing commit differences, finding removed secrets
Password found: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7

## Level 29 to 30
- **Task:**  Clone git repository and find password in alternate branch
- **Command used:** - git clone, git branch -a, git checkout dev, cat README.md
- **Learning**: Exploring multiple git branches, checking out different branches to find hidden content
Password found: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL

## Level 30 to 31
- **Task:**  Clone git repository and find password in a git tag
- **Command used:** - git tag, git show secret
- **Learning**: Git tags as storage mechanism for hidden data, examining tag contents
Password found: fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy

## Level 31 to 32
- **Task:**  Push a specific file to the remote repository, bypassing .gitignore
- **Command used:** - echo 'May I come in?' > key.txt
                    - git add -f key.txt (force add to bypass .gitignore)
                    - git commit -m "Add key.txt"
                    - git push origin master
- **Learning**: Bypassing .gitignore with git add -f, git push workflow, pre-receive hooks
Password found: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K

## Level 32 to 33
- **Task:**  Escape from the uppercase shell restriction
- **Command used:** - $0 or other shell escape methods
- **Learning**: Shell escaping, uppercase command restrictions, shell builtins
Password found: tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0