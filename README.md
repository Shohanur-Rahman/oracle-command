# SQL PLUS CREATE NEW USER IN ORACLE


```
alter session set "_ORACLE_SCRIPT"=true;

Session altered.



create user user_name identified by password;

User created.


grant create session to user_name;

Grant succeeded.



connect

```

