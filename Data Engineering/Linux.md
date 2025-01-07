- Open Source Command Line based OS.
- Multi User OS - Multiple Users can access the OS at the same time.
- Flavors - Ubuntu, RedHat Linux, Kali Linux, etc.
- Widely used in Servers.
# cd

- Change Directory
- Command : `$ cd directory_name`
- Example : `$ cd /home/niranjan`
- `$ cd ..` : Go to Previous Directory
# mkdir

- Make Directory
- Command : `$ mkdir directory_name`
- Example : `$ mkdir dir1 dir2`
- `$ mkdir -p /dir1/dir2` : Create Directory within Directory, `-p` = Parent Directory
# pwd

- Present Working Directory
- Shows current path
- Syntax : `$ pwd`
# ls

- List Files and Folders in Current Directory
- Command : `$ ls`
- `$ ls -l` : List Files with Details
- `$ ls -r` : List and Sort in Descending/Reverse Order
- `$ ls -t` : List and Sort by Timestamp
- `$ ls -R` : Show files and folder from Current and Sub Directories
- `$ ls -a` : Shows Hidden Files and Directories
- Absolute Path : Path from root
- Relative Path : Path from Current Location

# rmdir

- Remove empty Directories
- Command : `$ rmdir dir_name`

# rm 

- Remove Files
- Command : `$ rm file_name`
- `$ rm -r dir_name`   : Remove files recursively, remove non empty directories as well
- `$ rm file1 file2 file3`
# less

- Browse files interactively
- Command : `$ less file_name.txt`
# cat 

- Display whole file on terminal
- Command : `$ cat file_name`
# cal  

- Display a calendar on the terminal
- Command : `$ cal`
# touch

- Create an empty file
- Command : `$ touch file_name.extension`
- Example : `$ touch file.txt file1.conf`
# cp

- Copy
- 

# mv 

- Move

# vi

- Vim text editor
- Default Mode : Read Mode
- Command : `$ vi file_name`
- Switch to Insert Mode by clicking the `insert` or `i` button on keyboard
- Switch to Read Mode by pressing `esc` on keyboard
- `:w` : Write/Save File
- `:q` : Exit Vim
- `:wq` : Write/Save and Exit
- `:<>!` : Override Commands, `:q!` : Force Quit, `:w` : Force Write
- `:set number` : Assign numbers to lines
- `:n` : Go to `n`'th line, `:10` : Go to the 10th line
- `Shift + G` : Go to last line
- `/text` : Search for string, `n` to find next occurrence of `text`
- `:set list` : Enable End Line Character, shows last character in a line
	


- history -> View previous commands
- clear -> Clear everything from the terminal
- date -> Shows current date and time
- head -> View top lines of a file
- tail -> View last lines of a file
- du -> Show size of the directory
- df -> shows disk details
- chmod -> Modify permissions
- chown -> Modify ownsership
- grep -> 
- find -> 
- zip -> Compress files
- > operator
	- Overwrites the output
	- creates file if not present
- >> operator
	- appends the output
	- creates file if not present
- unzip -> extracts .zip files
- gzip -> Compress files.
- gunzip -> Unzip files compressed using gzip 
- tar -> Create a tar file
- ifconfig -> View Network information
- ping -> Check reachability of website
- ln -> Create link between files
- whereis -> Location of software
- wc 