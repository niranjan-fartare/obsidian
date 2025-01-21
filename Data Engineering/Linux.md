- Open Source Command Line based OS.
- Multi User OS - Multiple Users can access the OS at the same time.
- Flavors - Ubuntu, RedHat Linux, Kali Linux, etc.
- Widely used in Servers.
# Table Of Contents
- [cd](#cd)
- [mkdir](#mkdir)
- [pwd](#pwd)
- [ls](#ls)
- [rmdir](#rmdir)
- [rm](#rm)
- [less](#less)
- [more](#more)
- [cat](#cat)
- [cal](#cal)
- [touch](#touch)
- [cp](#cp)
- [mv](#mv)
- [vi](#vi)
- [history](#history)
- [clear](#clear)
- [date](#date)
- [head](#head)
- [tail](#tail)
- [rename files](#mv)
- [du](#du)
- [df](#df)
- [chmod](#chmod)
- [chown](#chown)
- [grep](#grep)
- [find](#find)
- [zip](#zip)
- [> operator](#-operator)
- [>> operator](#-operator-1)
- [unzip](#unzip)
- [gzip](#gzip)
- [gunzip](#gunzip)
- [tar](#tar)
- [ifconfig](#ifconfig)
- [ping](#ping)
- [ln](#ln)
- [whereis](#whereis)
- [wc](#wc)

# bc

- Basic Calculator
- Command : `$ bc`
# cd

- Change Directory
- Command : `$ cd directory_name`
- Example : `$ cd /home/niranjan`
- `$ cd ..` : Go to Previous Directory

# cut

- Extract specific columns from files
- Syntax : `cut -d seperator -f'n' file`, `-d` : seperator, `-f` : Field Number
- Example : `cut -d , -f1 data.txt`

```shell
$ cut -d , -f1 data.txt 
eid
1
2
3

$ cut -d , -f 2,3 data.txt 
 ename, did
 Niranjan, 10
 NoOne, 20
 Gaurav 40, 50000
```

# grep

- Global Search for Regular Expressions
- Search patterns in files and return the lines with the pattern
- Syntax : `$ grep "pattern" file`
- `$ grep -i "Linux" f1.txt`, `-i` : Ignore case of pattern
- `$ grep -c "Linux" f1.txt`, `-c`  : Number of lines where the pattern is present
- `$ grep -v "Open" f1.txt`, `-v` : Shows all the lines that do not contain the specified pattern
- `$ grep -l "Linux" *`, `-l` : Shows all the files where the pattern is present
- `$ grep -R "Linux" *`, `-i` : Search sub directories

```shell
$ cat f1.txt 
This is Linux
Linux is Easy.
Linux is a multi user operating SYstem
Linux is Open Source

$ grep "Open" f1.txt 
Linux is Open Source

$ grep -c "Linux" f1.txt
5

$ grep -l "Linux" *
f1.txt
f2.txt

$ grep -R "Linux" *
d1/f2.txt:Linux is Open Source
d1/f2.txt:I use Arch Linux btw.
f1.txt:This is Linux
f1.txt:Linux is Easy.
f1.txt:Linux is a multi user operating SYstem
f1.txt:Linux is Open Source
f1.txt:I use Arch Linux btw.


```
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
# more

- Browse files
- Command : `$ more file.txt`
# cat 

- Display whole file on terminal
- Command : `$ cat file_name`
# cal  

- Display a Calendar on the terminal
- Command : `$ cal`
- `$ cal -3` : Show previous, current, next month
- `$ cal -y` : Show all months in current Year
# touch

- Create an empty file
- Command : `$ touch file_name.extension`
- Example : `$ touch file.txt file1.conf`
# cp

- Copy Files or Directories
- Command : `$ cp source destination`
- Example : `$ cp sample.txt d1`
- Copy Folders : `$ cp d1/ d2/ -r`
# mv 

- Move Files or Directories
- Command `$ mv source destination`
- Example : `$ mv sample.txt d1`
- Rename File/Folder : `$ mv old_name.txt new_name.txt`
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
- `ndd` : Delete `n` lines from the current location of cursor
# history

- View previous 1000 commands
- Command : `$ history`
# clear

- Clear everything from the terminal
- Command : `$ clear`
# date

- Shows current date and time
- Command : `$ date`
- 
# head 

- View top lines of a file
- Shows top 10 lines by default
- Command : `$ head file.txt`
- `$ head -n file.txt`, `-n` = number of lines to show 
# tail 

- View last lines of a file
- Shows last 10 lines by default
- Command : `$ tail file.txt`
- `$ tail -n file.txt`, `-n` = number of lines to show 
# du

- Disk Usage
- Show size of the directory
- Command : `du file/folder`
- `$ du -h file/folder` :  Shows size of file/folder in human readable format
- `$ du -s` : Shows summarized size of folder
# df

- Disk Free
- Shows disk details
- Command : `df`
- `$ df -h` : Shows free space in human readable format

# chmod

- Change Permissions of Files and Directories

```bash
$ ls -l
drwxr-xr-x 3 niranjan niranjan 4096 Jan  8 10:25 d3
-rw-r--r-- 1 niranjan niranjan  323 Jan  7 11:28 data.txt
```

- `d rwx r-x r-x` : file/directory, owner permissions, group permissions, other permissions
- `r` : Read Permission (4)
- `w` : Write Permission (2)
- `x` : Execute Permission (1)
- `d` : DIrectory
- Command : `$ chmod permissions file/directory`, `permissions` represented by 3 digits
- Example : `$ chmod 700 data.txt`, `0` = no permission
# chown 

- Modify ownership of files/directories
# grep  

- 
# find

-
# zip

- Compress files
# unzip 

- extracts .zip files
# gzip 

- Compress files.
# gunzip

- Unzip files compressed using gzip 
# tar 

- Create a tar file
# ifconfig 

- View Network information
# ping 

- Check reachability of website
# ln 
- Create link between files
# whereis 

- Location of software
# wc

- Word Count
- Command : `$ wc file_name`

```bash
$ wc test.txt 
1 1001 6364 test.txt
```

- `1 1001 6364 test.txt` : lines, words, characters, file_name
- `$ wc -l file` : Count only lines
- `$ wc -w file` : Count only words
- `$ wc -c file` : Count only characters
# > operator

- Overwrites the output
- creates file if not present
# >> operator

- appends the output
- creates file if not present
- Example : `$ cut -d , -f 2 data.txt >> new_data.txt`
# ! Operator

 - Passes output of first command to the second conmand as an input
 - Syntax : `command 1 | Command 2`
 - Example : `$ cut -d , -f2 data.txt | head -2
 
```shell
$ cut -d , -f2 data.txt | head -2
 ename
 Niranjan
```