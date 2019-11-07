
# MySQL

## Create a database

```
mysqladmin create <name> [-u <user> -p]
```

## Login

```
mysql [-u <user> -p]
```
 
## Backup a database

```
mysqldump <name> --add-drop-table -h localhost -u <USER> -p<PASSWORD> > backup.sql
```

## Restoring a database from a backup file

```
mysql -h localhost -u <USER> -p<PASSWORD> <DB> < backup.sql
```
