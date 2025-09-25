## Level 0
- **Task:** SSH into bandit.labs.overthewire.org using user `bandit0`.  
- **Command used:** ssh bandit0@bandit.labs.overthewire.org -p 2220
- **Learning**: First time using SSH with custom port. Default SSH is port 22, here it’s 2220.

## Level 0 to 1
- **Task:**  The password for the next level is stored in a file called `readme` located in the home directory. Use this password to log into bandit1 using SSH on port 2220.
- **Command used:** ssh bandit0@bandit.labs.overthewire.org -p 2220
- **Learning**: the ls command lists files, and cat displays file content.
Password found: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

## Level 1 to 2
- **Task:**  The password for the next level is stored in a file called - located in the home directory
- **Command used:** ssh bandit1@bandit.labs.overthewire.org -p 2220
- **Learning**: How to handle strange filenames (like -) by using ./filename or -- to end options.
Password found: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

## Level 2 to 3
- **Task:**  The password for the next level is stored in a file called --spaces in this filename-- located in the home directory
- **Command used:** ssh bandit2@bandit.labs.overthewire.org -p 2220
- **Learning**: How to work with filenames that include spaces: quoting and escaping.
                More practice with SSH, ls, cat and careful shell quoting.
Password found: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

## Level 3 to 4
- **Task:**  The password for the next level is stored in a hidden file in the inhere directory.
- **Command used:** ssh bandit3@bandit.labs.overthewire.org -p 2220
- **Learning**: How to handle files with unusual names (leading dots, spaces, dashes) using quoting or ./.
                Practical use of file and strings to safely inspect unknown files.
Password found: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

## Level 4 to 5
- **Task:**  The password for the next level is stored in the only human-readable file in the inhere directory.
- **Command used:** ssh bandit4@bandit.labs.overthewire.org -p 2220
- **Learning**: How to handle filenames starting with - by using ./filename.
                How to quickly check multiple files with the file command.
Password found: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw


