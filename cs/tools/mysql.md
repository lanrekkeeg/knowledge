
# MySQL

## Create a database

```shell
mysqladmin create <name> [-u <user> -p]
```

## Login

```shell
mysql [-u <user> -p]
```
 
## Backup a database

```shell
mysqldump <name> --add-drop-table -h localhost -u <USER> -p<PASSWORD> > backup.sql
```

## Restoring a database from a backup file

```shell
mysql -h localhost -u <USER> -p<PASSWORD> <DB> < backup.sql
```
