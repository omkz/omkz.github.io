---
published: true
title: Buat User baru dengan Password di Postgresql
layout: post
categories: postgresql
tags: [postgresql]
---

```
omenks@ip-172-31-24-xxx:~$ sudo su - postgres

postgres@ip-172-31-24-xxx:~$ createuser test_user

postgres@ip-172-31-24-xxx:~$ psql
psql (9.3.9)
Type "help" for help.

postgres=# \password test_user

Enter new password: 
Enter it again: 

postgres=# psql
postgres-# \q
postgres@ip-172-31-24-xxx:~$ psql -U test_user -d postgres -h 127.0.0.1 -W

Password for user test_user: 
psql (9.3.9)
SSL connection (cipher: DHE-RSA-AES256-GCM-SHA384, bits: 256)
Type "help" for help.

postgres=# \du
                             List of roles
 Role name |                   Attributes                   | Member of 
-----------+------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication | {}
 test_user |                                                | {}
 xxx       |                                                | {}

postgres=# \l
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-----------+----------+----------+-------------+-------------+-----------------------
 jerry     | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 test1     | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
(5 rows)

postgres=# 
```