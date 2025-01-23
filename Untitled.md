
# Linux Commands Guide

## Linux Overview
- Linux is an Open Source Command Line based Operating System
- It is a Multi User Operating System, i.e. Multiple Users can access the Operating System at the same time
- Flavors Of Linux - Ubuntu, RedHat Linux, Kali Linux, etc.
- It is widely used in Servers

## Commands

### bc
- Basic Calculator
- Command: `$ bc`

### cal
- Display a Calendar on the terminal
- Command: `$ cal`
- `$ cal -3`: Show previous, current, next month
- `$ cal -y`: Show all months in current Year

### cat
- Display whole file on terminal
- Command: `$ cat file_name`

### cd
- Change Directory
- Command: `$ cd directory_name`
- Example: `$ cd /home/niranjan`
- `$ cd ..`: Go to Previous Directory

### chmod
- Change Permissions of Files and Directories
- `d rwx r-x r-x`: file/directory, owner permissions, group permissions, other permissions
- `r`: Read Permission (4)
- `w`: Write Permission (2)
- `x`: Execute Permission (1)
- `d`: Directory
- Command: `$ chmod permissions file/directory`, `permissions` represented by 3 digits
- Example: `$ chmod 700 data.txt`, `0` = no permission

### chown
- Modify ownership of files/directories

### clear
- Clear everything from the terminal
- Command: `$ clear`

### comm
(No description provided)

### cp
- Copy Files or Directories
- Command: `$ cp source destination`
- Example: `$ cp sample.txt d1`
- Copy Folders: `$ cp d1/ d2/ -r`

### cut
- Extract specific columns from files
- Command: `cut -d seperator -f'n' file`, `-d`: separator / delimiter, `-f`: Field Number
- Example: `cut -d , -f1 data.txt`

### date
- Shows current date and time
- Command: `$ date`

### df
- Disk Free
- Shows disk details
- Command: `df`
- `$ df -h`: Shows free space in human readable format

### diff
- Differentiate Files

### du
- Disk Usage
- Show size of the directory
- Command: `du file/folder`
- `$ du -h file/folder`: Shows size of file/folder in human readable format
- `$ du -s`: Shows summarized size of folder

### find
- Find files and folders
- Command: `$ find location options`
- `$ find location -type f/d`, `-f`: Show files, `-d`: Show only directories
- `$ find location -name pattern`: Find files with the given pattern
- `$ find location -iname pattern`: Find files with the given pattern ignoring the case of the file name
- `$ find . -perm permissions`: Find files with the given permissions
- `$ find . -user username`: Find files with the given username
- `$ find . -empty`: Find empty files
- `$ find . -mtime -n`
- `$ find . -mmin -n`
- `$ find . -size size`: Find files based on the given `size`, `+5M` for files greater than 5MB or `-5M` for vice versa
- `$ find . -size size -size size`: Range

### grep
- Global Search for Regular Expressions
- Search patterns in files and return the lines with the pattern
- Command: `$ grep "pattern" file`
- `$ grep -i "Linux" f1.txt`, `-i`: Ignore case of pattern
- `$ grep -c "Linux" f1.txt`, `-c`: Number of lines where the pattern is present
- `$ grep -v "Open" f1.txt`, `-v`: Shows all the lines that do not contain the specified pattern
- `$ grep -l "Linux" *`, `-l`: Shows all the files where the pattern is present
- `$ grep -R "Linux" *`, `-i`: Search sub directories
- `$ grep -R 'operating\|Open' *`: Search multiple patterns

### gunzip
- Unzip files compressed using gzip

### gzip
- Compress files

### head
- View top lines of a file
- Shows top 10 lines by default
- Command: `$ head file.txt`
- `$ head -n file.txt`, `-n` = number of lines to show

### history
- View previous 1000 commands
- Command: `$ history`

### ifconfig
- View Network information
- Command: `ifconfig`

### less
- Browse files interactively
- Command: `$ less file_name.txt`

### ln
- Create link between files
## Hard Link
- Link works even after deleting the original folder
- Command: `ln file link_name`
## Soft Link / Symbolic Link
- Link does not work after deleting the original folder
- Command: `ln -s file link_name`

### ls
- List Files and Folders in Current Directory
- Command: `$ ls`
- `$ ls -l`: List Files with Details
- `$ ls -r`: List and Sort in Descending/Reverse Order
- `$ ls -t`: List and Sort by Timestamp
- `$ ls -R`: Show files and folder from Current and Sub Directories
- `$ ls -a`: Shows Hidden Files and Directories
- Absolute Path: Path from root
- Relative Path: Path from Current Location

### mkdir
- Make Directory
- Command: `$ mkdir directory_name`
- Example: `$ mkdir dir1 dir2`
- `$ mkdir -p /dir1/dir2`: Create Directory within Directory, `-p` = Parent Directory

### more
- Browse files
- Command: `$ more file.txt`

### mv
- Move Files or Directories
- Command `$ mv source destination`
- Example: `$ mv sample.txt d1`
- Rename File/Folder: `$ mv old_name.txt new_name.txt`

### paste
- Combine 2 files line by line
- Command: `paste file1 file2`
- `paste -d '|' city.txt state.txt`, `-d`: separator / delimiter

### ping
- Check reachability of website
- Command: `$ ping domain/ip`

### pwd
- Present Working Directory
- Shows current path
- Command: `$ pwd`

### rm
- Remove Files
- Command: `$ rm file_name`
- `$ rm -r dir_name`: Remove files recursively, remove non-empty directories as well
- `$ rm file1 file2 file3`

### rmdir
- Remove empty Directories
- Command: `$ rmdir dir_name`

### sed
- Stream Editor
- Command: `sed 's/Linux/UNIX/' data.txt`

### tail
- View last lines of a file
- Shows last 10 lines by default
- Command: `$ tail file.txt`
- `$ tail -n file.txt`, `-n` = number of lines to show

### tar
- Create a tar file

### touch
- Create an empty file
- Command: `$ touch file_name.extension`
- Example: `$ touch file.txt file1.conf`

### users
- Find all the active users
- Command: `$ users`

### vi
- Vim text editor
- Default Mode: Read Mode
- Command: `$ vi file_name`
- Switch to Insert Mode by clicking the `insert` or `i` button on keyboard
- Switch to Read Mode by pressing `esc` on keyboard
- `:w`: Write/Save File
- `:q`: Exit Vim
- `:wq`: Write/Save and Exit
- `:<>!`: Override Commands, `:q!`: Force Quit, `:w`: Force Write
- `:set number`: Assign numbers to lines
- `:n`: Go to `n`'th line, `:10`: Go to the 10th line
- `Shift + G`: Go to last line
- `/text`: Search for string, `n` to find next occurrence of `text`
- `:set list`: Enable End Line Character, shows last character in a line
- `ndd`: Delete `n` lines from the current location of cursor

### whereis
- Location of software

### whoami
- View username
- Command: `$ whoami`

### wc
- Word Count
- Command: `$ wc file_name`
- `$ wc -l file`: Count only lines
- `$ wc -w file`: Count only words
- `$ wc -c file`: Count only characters

### Operators
#### > Operator
- Overwrites the output
- Creates file if not present

#### >> Operator
- Appends the output
- Creates file if not present
- Example: `$ cut -d , -f 2 data.txt >> new_data.txt`

#### ! Operator
- Passes output of first command to the second command as an input
- Command: `command 1 | Command 2`
- Example: `$ cut -d , -f2 data.txt | head -2`

### Compression Commands
- zip: Compress files
- unzip: Extract .zip files
- gzip: Compress files
- gunzip: Unzip files compressed using gzip
