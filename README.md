# Day 7 Shells and Essential Commands

![Static Badge](https://img.shields.io/badge/%24shell-003545?style=for-the-badge&logo=gnu-bash&logoColor=white&color=black)
![Static Badge](https://img.shields.io/badge/linux-black?style=for-the-badge&logo=linux&logoColor=black&color=FCC624)

# Homework 1

### Set Environment Variable to Machinewise. (Permanently)

If you are using zsh shell, edit .zprofile which is under home directory,

```
vi ~/.zprofile
#add lines at the bottom of the file:
export KEY="VALUE"
```

After updating the .zprofile, run source ~/.zprofile for immediate effect.

# Homework 2

## Linux Alternate Commands for Window Shell

#### Summary

| No. | Linux Command | Window Alternative |
| --- | ------------- | ------------------ |
| 1   | LS            | DIR                |
| 2   | CD            | CD                 |
| 3   | PWD           | CD                 |
| 4   | MKDIR         | MKDIR / MD         |
| 5   | RM            | RMDIR/ DEL         |
| 6   | CP            | COPY/ XCOPY        |
| 7   | MV            | MOVE, RENAME/REN   |
| 8   | ALIAS         | DOSKEY             |

#### Details Usages

#### DIR Alternative to Window Shell

Usages :

1.  display the contents of the current directory (not included hidden files)

```
dir
```

2. display the contents of the current directory (included hidden files)

```
dir /A
```

3. display the contents of the current directory ( hidden files only )

```
dir /A:H
```

4. List the contents under C:\DirectoryName directory

```
dir C:\\DirectoryName
```

5. display the contents together with owner information under current directory

```
dir /Q
```

#### CD alternate to Window Shell

Name: CD
Usage :

1. Changing to specific directory

```
cd C:\Users\KKH
```

2. Changing to root directory

```
cd \
```

3. Changing to the Parent direcotyr

```
cd ..
```

4. Changing the Disk

```
cd /d D:\Yourfolder
```

5. Changing to a directory which included space

```
cd "C:\Program File"
```

#### PWD & MKDIR

Alternate to pwd in linux, we can use 'cd' to display the current directory

```
cd
```

'mkdir' command in linux is the same to window command

```
mkdir directoryname
```

Window also have shorter version of 'mkdir', 'md'.

```
md directoryname
```

#### RM

To remove file, we can use 'del' or 'erase' in window.

```
del filename.txt
```

To remove directory, can use 'rmdir',

```
rmdir directoryname
```

If you want to remove the directory and it's content recursively, use with /S option

```
rmdir /S /Q directoryname
```

'/S' flag remove all directories and files in specified directory name, and '/Q' is to omit the confirmation prompt.

#### CP

CP Command alternate to window are 'copy' and 'xcopy'.

```
copy source.txt destination.txt
```

```
xcopy sourcedir destinationdir /E /I
```

`/E` copies all subdirectories, including empty ones.
`/I` assumes the destination is a directory if it doesn't exist.

#### MV

MV command alternate to window is 'move'. But if we want to rename file or directory, we can use 'rename' or 'ren' command. Below are the example usages.

```
move sourcedir destinationdir
```

```
rename oldname.txt newname.txt
```

### alias

Alternate to alias in linux, we can use doskey command in window for temporary alias setting.

```
doskey gping=ping 8.8.8.8
```

and 'gping' command will ping to google dns server and display the response.

```
gping
```

# Homework 3

## Build a Knowledge base with other Text Processing tools

### 1. Grep

User can specify the string or text by using Grep command from command line output (stdout) or text and display the line which included the text specified.
Use case :
display only to the service using port 80

```
netstat -an | grep "80"
```

### 2. Sed (Stream Editor)

Sed command is very powerful command to search, replace, insert and delete the text format files on linux command line. Its also support regular expression.

Basic

```
sed [options] 'script' [file]
```

Replace Text (s/ flag) follow by /oldstring and /newstring

```
sed 's/old_string/new_string' file.txt
```

Delete Line (/d) flag

```
sed '/remove_me/d' file.txt
```

Insert Line (-i ) flag

```
sed -i '1i\Hello World' file.txt
```

### 3. awk

**1. AWK Operations:**   
(a) Scans a file line by line   
(b) Splits each input line into fields   
(c) Compares input line/fields to pattern   
(d) Performs action(s) on matched lines

**2. Useful For:**   
(a) Transform data files   
(b) Produce formatted reports

**3. Programming Constructs:**   
(a) Format output lines   
(b) Arithmetic and string operations   
(c) Conditionals and loops
Example usages of AWK
Let's say you have a text file named 'userinfo.txt' and contains below data :

```
fristName       lastName        age     city       ID

Thomas          Shelby          30      Rio        400
Omega           Night           45      London    600
Wood            Tinker          54      Lisbon     N/A
Giorgos         Georgiou        35      London     300
Timmy           Turner          32      Berlin     N/A
```

```shell
awk '{print $0}' userinfo.txt
```

Above command will give you the output of all data in shell, as it is.
But it have build-in variable 'NR' which can output the line number in shell along with the data.

```shell
awk '{print NR,$0}' userinfo.txt
```

```
1 fristName     lastName        age     city       ID
2
3 Thomas        Shelby          30      Rio        400
4 Omega         Night           45      London    600
5 Wood          Tinker          54      Lisbon     N/A
6 Giorgos       Georgiou        35      London     300
7 Timmy         Turner          32      Berlin     N/A
```

Ok, lets print by columns. If you want to display first column only, you can use following command:

```shell
awk '{print $1}' userinfo.txt
```

```shell
fristName

Thomas
Omega
Wood
Giorgos
Timmy
```

Let's display firstName and lastName.

```shell
awk '{print $1,$2}' userinfo.txt
```

```
fristName  lastName

Thomas     Shelby
Omega      Night
Wood       Tinker
Giorgos    Georgiou
Timmy      Turner
```

We can manipulate the stdout by using grep or head with pipe, as below example,

```shell
awk '{print $1}' userinfo.txt | head -1
```

```
FirstName
```

```shell
awk '{print $1,$2}' userinfo.txt | grep "Omega"
```

```
Omega Night
```

We can use Regular expression to stdout the data as well. Using '^' between '/ /' to find the string start by character follow to ^. For example, to find the string start with T, we can write as below

```shell
awk '/^T/' userinfo.txt
```

```
Thomas          Shelby          30      Rio        400
Timmy           Turner          32      Berlin     N/A
```

```shell
awk '/0$/' userinfo.txt
```

It output all the string end by zero 0.

```
Thomas          Shelby          30      Rio        400
Omega           Night           45      London    600
Giorgos         Georgiou        35      London     300
```

We can combine regular expression and specific column as well.
Below example command will output the first name and last name which start by letter 'O'.

```shell
awk '/^O/{print $1,$2}' userinfo.txt
```

To find all the information of people living in `London`

```shell
awk '/London/' userinfo.txt
```

```
Omega           Night           45      London    600
Giorgos         Georgiou        35      London     300
```

We can also do the Arithmetic operation. Lets find out the people who is under `40`,

```shell
awk '$3 <  40 { print $0 }' userinfo.txt
```

```
Thomas          Shelby          30      Rio        400
Giorgos         Georgiou        35      London     300
Timmy           Turner          32      Berlin     N/A
```

#### 4. Wget

Wget is the non-interactive network downloader which is used to download files from the server.
Basic Usage :

```shell
wget [option] [URL]
```

Example :

```shell
wget -b http://www.example.com/filename.txt
```

-b flag is to run the download process on background.

Other options are as below :

```shell
wget -c // to resume partially downloaded file
	 --tries=10 // specify the number of retry attemps
	 -w 10 // set wait time between retrievals
	 -r // enable recursive retrieval
	 -i fileincludeurl.txt // read urls from given file and download
```

# Homework 4

## Text manipulation with shell Homework

1. To download the text file from url, I will use wget as below :

```shell
wget https://raw.githubusercontent.com/khantnaingset-kns/wops-devops-pe-training-kns/main/hm1.txt
```

2. Process the Text File

```shell
cat hm1.txt
```

3. To count the occurrence of 'AI' and 'NLP'

```shell
ai_count=$(grep -o 'AI' hm.txt | wc -l)
nlp_count=$(grep -o 'NLP' hm.txt | wc -l)

```

4. Modify Text
   To replace 'AI' with 'gen AI' and save to a new file using Loop.

- create a new bash file

```shell
vi replaceai.sh
```

```
#!/bin/bash

while IFS= read -r line; do
if echo "$line" | grep -q 'AI'; then
line=$(echo "$line" | sed 's/AI/gen AI/g')
fi

echo "$line"

done < hm1.txt
```

- Then place that shell under same directory with hm1.txt and run as below :

```shell
./replaceai.sh
```

- It will replace the 'AI' with 'gen AI' and 'strout' the replaced text in shell.

5. Output the Results

- Print the counts of "AI" and "NLP".

```shell
echo $ai_count
Output : 6
echo $nlp_count
Output : 5
```

- Save the modified text to a new file
  run 'replaceai.sh' shell and redirect the output into new file

```shell
./replaceai.sh > new_hm.txt
```

Open the newly created file and see the changes

```shell
cat new_hml.txt
```
