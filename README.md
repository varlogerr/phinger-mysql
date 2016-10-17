#Phinger MySQL

Collection of phing targets for MySQL manipulations

## Installation

1) Run `composer require phinger/mysql`  
2) Add  
```
<property file="{path-to-lib}/mysql.yml" override="false" />
<import file="{path-to-lib}/mysql.xml" />
```
to your build file  
3) Create overrides configuration file and import it __before__ importing configuration from the library in order to override library properties.  
4) Run `phing -l` if you want to list all available targets  
5) Use library targets  

### Demo

This demo will create a dump of 'my_database' in './backup/mysql/dump.sql' file.  

_{project-path}/my-conf.yml_
```
# Only these 4 settings will be overriden. You can override any
# setting in the same way
phinger:
  mysql:
    dbname: my_database # override default database name ('acme')
    dbuser: my_user     # override default database user ('root')
    dbpass: my_password # override default database password ('')
    dump_path: ./backup/mysql/dump.sql # override default dumpfile path ('./backup/sql/dump.sql')
```

_{project-path}/build.xml_
```
<?xml version="1.0" encoding="UTF-8" ?>

<project
        name="test"
        default="dump-db"
>
    <property file="./my-conf.yml" />
    
    <property file="./vendor/phinger/mysql/mysql.yml" override="false" />
    <import file="./vendor/phinger/mysql/mysql.xml" />
    
    <target
            name="dump-db"
            depends="phinger:mysql:dump-create"
    />
</project>
```

## Targets

### Dump database to an sql file
`phinger:mysql:dump-create `  
**NB** Dump-file directory will be created if it doesn't exist

#### Properties / params (defaults):
* `phinger.mysql.dbhost`           (127.0.0.1)  
* `phinger.mysql.dbport`           (3306)  
* `phinger.mysql.dbname`           (acme)  
* `phinger.mysql.dbuser`           (root)  
* `phinger.mysql.dbpass`           ('')  
* `phinger.mysql.dumper_bin_path`  (/usr/bin/mysqldump)  
* `phinger.mysql.dump_path`        (./backup/sql/dump.sql)  
* `phinger.mysql.dump_no_comments` (true)  
* `phinger.mysql.dump_no_locks`    (true)  
