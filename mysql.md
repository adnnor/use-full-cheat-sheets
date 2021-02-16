## MySQL
MySQL is an open-source relational database management system. Its name is a combination of "My", the name of co-founder Michael Widenius's daughter, and "SQL", the abbreviation for Structured Query Language. [Source][3]

### Export Database
You can export database using your favorite MySQL visual tool such as [DBeaver][1] or [MySQL Workbench][2]. If you are not using or don't have any then you can use native linux terminal.

**Export single database**
```bash
mysqldump -u [username] -p [database] > [file]
# e.g.
mysqldump -u root -p sample > sample.gz
```

**Export single gzipped-compressed database**
```bash
mysqldump -u [username] -p [database] | gzip > [file]
# e.g.
mysqldump -u root -p sample | gzip > sample.gz

# remove the definer 
mysqldump -u [username] -p [database] | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > [file]
```

**Export a table from the database**
```bash
# gzipped-compressed
mysqldump -u [username] -p [database] [table] | gzip > [file]
# or uncompressed
mysqldump -u [username] -p [database] [table] > [file]
```

### Import Database
You can import your database in multiple ways, it also depends on what kind of format do you.   

**Import gzipped database**
```bash
zcat [path] | mysql -u [username] -p [database]
# e.g.
zcat /path/to/sample.gz | mysql -u root -p sample
```

**Import .sql database**
```bash
mysql -u [username] -p [database name] < [.sql path]
# e.g.
mysql -u root -p sample < ~/Downloads/sample.sql
```

**Import using MySQL source command**   

Open MySQL cli
```bash
mysql -u [username] -p
```
When logged in, create the database if not exists;
```bash
CREATE DATABASE IF NOT EXISTS sample;
```
Then, switch to desired or newly created database;
```bash
USE sample;
```
Finally, import the database;
```bash
SOURCE [.sql path]
# e.g.
SOURCE /home/ad/Desktop/sample.sql;
```





### Tricks
**Run MySQL query on terminal**
```bash
mysql -u root -p -e "CREATE DATABASE database-name;"
```

[1]: https://dbeaver.io/
[2]: https://www.mysql.com/products/workbench/
[3]: https://en.wikipedia.org/wiki/MySQL
