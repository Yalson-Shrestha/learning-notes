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