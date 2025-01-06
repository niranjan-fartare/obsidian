- Linux Program
- 

# Options

- -d -> Checks of given path is a directory
- -f -> Checks of given path is a file

```shell
#!/bin/bash

mkdir d1 d2 d3
touch f1 f2 f3
cp f2 d2
```

# Run

- `./file.sh` -> Requires Execute permission
- `bash file.sh` 
- `sh file.sh`
# Echo

- Used for printing messages on the terminal

```bash
#!/bin/bash

echo Welcome to Linux Programming!
```

```sh
$ bash echo.sh 
Welcome to Linux Programming!
```
# Variables

```sh
#!/bin/bash

name="Niranjan"
age=25
echo Welcome to Linux Programming!
echo My name is $name and I am $age years old.
```

# Passing Input

```sh
#!/bin/bash

name=$1
age=$2
city=$3

echo Welcome to Linux Programming!
echo My name is $name and I am $age years old. I am from $city.
```

```sh
$ bash input.sh "Niranjan" 25 "Pune"
Welcome to Linux Programming!
My name is Niranjan and I am 25 years old. I am from Pune.
```

# If Else

```shell
#!/bin/bash

#run : bash myscript "Niranjan" 25

name=$1
age=$2

if [ ${age} -gt 18 ] ;then
	echo $name you are eligible for voting!!!
else
	echo $name you are not eligible for voting!!!
fi

echo Script Completed
```

```shell
#/bin/bash

# Script to check if file/folder exists

if [ -d /home/niranjan/saayu/check/d1 ] ;then
	echo "D1 Directory already exists"
else
	mkdir /home/niranjan/saayu/check/d1
fi


if [ -d /home/niranjan/saayu/check/d2 ] ;then
	echo "D2 Directory already exists"
else
	mkdir /home/niranjan/saayu/check/d2
fi


if [ -f /home/niranjan/saayu/check/d1/f1 ] ;then
	echo "f1 file Already exists"
else
	touch /home/niranjan/saayu/check/d1/f1
fi

cp -r /home/niranjan/saayu/check/d1/f1 /home/niranjan/saayu/check/d2/f1

echo Script Completed
```

# Hive Operations

```shell
#/bin/bash

# Script to backup given Table
# Run Command : bash backup_hive.sh "Schema" "TableName"

schema=$1
table_name=$2

today=`date +"%Y%m%d%H%M%S"`

echo Backing up Table ${schema}.${table_name}

echo "create table ${schema}.${table_name}_${today} as select * from ${schema}.${table_name};" | hive

echo Backup complete for table ${schema}.${table_name}
```


```shell
#!/bin/bash

#Script to drop given Table
#Run Command : bash drop_table.sh "schema" "table_name"

schema=$1
table_name=$2

echo Dropping Table ${schema}.${table_name}

echo "drop table ${schema}.${table_name};" | hive

echo Dropped Table ${schema}.${table_name}
```

```shell
#!/bin/bash 

#Script to truncate given Table
#Run Command : bashtrncate_hive.sh "Schema" "Table Name"

schema=$1
table_name=$2

echo Cleaning Table ${schema}.${table_name}

echo "truncate table ${schema}.${table_name};" | hive

echo Cleaning Table ${schema}.${table_name} completed.
```

```shell
#!/bin/bash

#Command to backup multiple tables 
#Run Command : bash backup_bulk.sh "Schema"

echo Script Started

today=`date +"%Y%m%d%H%M%S"`

schema=$1

while read table_name
do
echo Backup for table ${table_name} started,

echo "create table ${schema}.${table_name}_${today} as select * from ${schema}.${table_name};" | hive

echo Backup for table ${table_name} completed.

done < /home/hadoop/niranjan/table_list.txt

echo Script Completed!
```

# Functions

```shell
#!/bin/bash

#Run command : bash func.sh

greeting(){
echo Hello World!
}

welcome(){
echo Welcome to Linux Programming!
}

# Calling function
greeting
welcome
```


```shell
#!/bin/bash
#Run Command : bash hive_ops.sh "Schema" "B/NA" "T/NA" "D/NA"
#B = Backup, T = Truncate, D = Drop 

echo script started 

schema=$1
bkp_flg=$2
tru_flg=$3
drop_flg=$4
today=`date +"%Y%m%d%H%M%S"`

bkp_tbl(){
	echo backup for ${table_name} started
	echo "create table ${schema}.${table_name}_${today} as select * from  ${schema}.${table_name};" | hive
	echo backup for ${table_name} completed
}

truncate_tbl(){
	echo truncating table ${schema}.${table_name}
	echo "truncate table ${schema}.${table_name};" | hive
	echo truncating table ${schema}.${table_name}
}

drop_tbl(){
	echo dropping table ${schema}.${table_name}
	echo "drop table ${schema}.${table_name};" | hive
	echo dropping table ${schema}.${table_name}
}

while read table_name
do

if [ $bkp_flg == "B" ] ;then
	bkp_tbl
fi

if [ $tru_flg == "T" ] ;then
	truncate_tbl
fi

if [ $drop_flg == "D" ] ;then
	drop_tbl
fi

done < /home/hadoop/table_list.txt

echo script completed
```


# Crontab

- Used for Scheduling Scripts/Tasks
- Minimum frequency -> 1min
- `crontab -l` -> List all tasks
- `crontab -e` -> Open Cron Editor 