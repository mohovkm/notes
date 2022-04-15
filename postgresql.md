### View databases
```sql
\l
\l+
SELECT datname FROM pg_database;
```

### View tables in db
```sql
\dt
```

### View sequenece
```sql
\ds
```

### View users and rights
```sql
\du
```

### View access privileges
```sql
\z
```

### Create role
```sql
CREATE ROLE readaccess;
```

### Assign permissions:
#### Assignt connect permission
```sql
GRANT CONNECT ON DATABASE mydb TO readaccess;
```

#### Assign permission to usage schema and query
```sql
GRANT USAGE ON SCHEMA public TO readaccess;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readaccess;
```

#### Assign select permission on specific table 
```sql
GRANT SELECT ON mytable IN SCHEMA public TO readaccess;
```

### Create user
```sql
CREATE USER read_user WITH PASSWORD 'read_password';
```

#### Add user to created role
```sql
GRANT readaccess TO read_user;
```

### Creating table
```sql
CREATE TABLE demo (
name varchar(25),
id serial,
start_date date);
```

### Inserting data into table
```sql
insert into demo VALUES ('Konstantin', DEFAULT, '2021-12-01');
```

### Change role passwrod
```sql
alter user postgres with PASSWORD 'new_pass';
```

### Restore db with pg_admin
```bash
pg_restore -U postgres -d postgres -x -c -1 /backups/backup_db.sql
```
