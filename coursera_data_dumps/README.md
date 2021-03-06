# Introduction

This folder contains helper functions for each Coursera data dump. This README also provides some basic information on MySQL databases, such as how to load data from a MySQL database, and how to convert a MySQL database to a SQLite database. 

More Information:

 1. [Coursera help pages](https://partner.coursera.help/hc/en-us/articles/203586039-Manual-Data-Exports)
 2. [Installing MySQL & MySQL workbench](https://dev.mysql.com/downloads/mysql/)
 3. [MySQL v. SQLite](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems)

# Working with the MySQL coursera data dumps

After installing MySQL on your environment, you should start by changing the password.

- default username is 'root'. This comes with a pre-determined pwd. Here's how to change it (see: http://stackoverflow.com/questions/10895163/how-to-find-out-the-mysql-root-password)

		* If server is running: stop it --> sudo /usr/local/mysql/support-files/mysql.server stop
		* Start in safe mode --> sudo mysqld_safe --skip-grant-tables 
		* Log in to root (from another terminal window): mysql -u root
		* Change pwd: mysql> UPDATE mysql.user SET Password=PASSWORD('password') WHERE User='root';
		* Start server: sudo /usr/local/mysql/support-files/mysql.server start

## Basic commands

### Starting server 

- sudo /usr/local/mysql/support-files/mysql.server start

### Stopping server

- sudo /usr/local/mysql/support-files/mysql.server stop

### Restarting server

- sudo /usr/local/mysql/support-files/mysql.server restart

### Exporting path

- export PATH=$PATH:/usr/local/mysql/bin/

	* If problem exists that you have to export EVERY time you start a new terminal instance, see: http://hathaway.cc/post/69201163472/how-to-edit-your-path-environment-variables-on-mac

### Importing a sql dump file

Coursera gives us data in the form of MySQL dumps. Once you obtain these, follow the steps below to import a SQL file. 

	1. If MySQL is not running, start it using: sudo /usr/local/mysql/support-files/mysql.server start 
	2. Open a terminal instance 
	3. Enter MySQL environment ----> mysql -u <USERNAME> -p
	4. Drop database ----> DROP DATABASE <dbname>;
	5. Create database ----> CREATE DATABASE <dbname>;
	6. Exit MySQL environment ----> EXIT;

Now, import a sql dumpfile into the mysql database with the following command. You will be prompted to enter your password after executing this line

	6. mysql -u <USERNAME> -p -D my_session < /path/to/FILENAME.sql

## A note on my use of SQLite databases

I generally convert all of the Coursera MySQL dumps to SQLite databases and use these interchangeably. SQLite databases work in a similar way to MySQL databases. However, they are serverless and take a hit on security (among other differences). Also, I find it's straightforward to copy SQLite files into the vagrant box as part of the standard VM population. 

However, I have added a quick how-to on working with R & MySQL in the "/R_and_RMySQL" folder. I also altered the [SQL quick access helper function](https://github.com/JasperHG90/MOOCs/blob/master/workflow/generic_helper_functions/helper_functions.R) to be able to query from both SQLite & MySQL databases. 

It is possible to convert MySQL databases to SQLite (see: https://gist.github.com/esperlu/943776)

To convert, download the script. Then, navigate to the folder where the script is located and run the following line:

	- sh mysql2sqlite.sh -u root -p <MySQLtablename> | sqlite3 /path/to/folder/<dbname>.sqlite

You will be prompted to enter the mySQL password, after which the MySQL database will be converted to the location you specified.

## Working with MySQL databases directly from within R

Please see a short how-to in the "/R_and_RMySQL" folder



