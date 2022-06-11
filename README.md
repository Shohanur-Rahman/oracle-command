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


# SQL PLUS CONNECT SYS

``` 
user name: sys as sysdba
password: sys
```


# CREATE USER AND GRANT ALL MANUALLY

```
alter session set "_ORACLE_SCRIPT"=true;  
CREATE USER USER_NAME IDENTIFIED BY your_password;
GRANT CONNECT TO USER_NAME;
GRANT CREATE SESSION, GRANT ANY PRIVILEGE TO USER_NAME;
GRANT CREATE SESSION, GRANT ALL PRIVILEGE TO USER_NAME;
GRANT UNLIMITED TABLESPACE TO USER_NAME;
CREATE TABLESPACE USER_NAME DATAFILE 'USER_NAME.dbf' SIZE 3000M;
ALTER USER USER_NAME DEFAULT TABLESPACE USER_NAME;
GRANT CREATE TABLE TO USER_NAME;
GRANT CREATE VIEW TO USER_NAME;
GRANT CREATE SESSION TO USER_NAME;
GRANT ALL PRIVILEGES TO USER_NAME;
GRANT GRANT ANY PRIVILEGE TO USER_NAME;
GRANT CREATE PROCEDURE TO USER_NAME;
GRANT CREATE JOB TO USER_NAME;
GRANT CREATE SYNONYM TO USER_NAME;
GRANT ALTER ANY TABLE TO USER_NAME;
GRANT CREATE SEQUENCE TO USER_NAME;
GRANT CREATE TRIGGER TO USER_NAME;
GRANT CREATE ANY INDEX TO USER_NAME;
GRANT CREATE TYPE TO USER_NAME;
```


# SELECT ALL SEQUENCE NAME

```
select SEQUENCE_NAME from USER_SEQUENCES;

select SEQUENCE_NAME from USER_SEQUENCES where SEQUENCE_NAME='ECOM_DB';

```


#ORACLE INCREASE SEQUENCE VALUE BY LOPP

```

DECLARE
  ROW_VALUE NUMBER;
  ROW_TABLE_NAME VARCHAR(200);
BEGIN
  FOR J IN (select SEQUENCE_NAME from USER_SEQUENCES) LOOP
      BEGIN
                      FOR I IN 1..650 LOOP
                      BEGIN
                              EXECUTE IMMEDIATE 'SELECT '||J.SEQUENCE_NAME||'.NEXTVAL FROM DUAL';
                              COMMIT;
                              EXCEPTION WHEN OTHERS THEN
                              NULL;
                      END;
                  END LOOP;
              COMMIT;
              EXCEPTION WHEN OTHERS THEN
              NULL;
      END;
  END LOOP;
END;

```


# ORACLE DELTE ALL TABLE DATA IN ONCE

```
DECLARE
  ROW_VALUE NUMBER;
  ROW_TABLE_NAME VARCHAR(200);
BEGIN
  FOR J IN (SELECT TABLE_NAME FROM USER_TABLES HERE WHERE HERE.TABLE_NAME <> '__EFMigrationsHistory') LOOP
      BEGIN
              EXECUTE IMMEDIATE 'DELETE FROM '||J.TABLE_NAME;
              COMMIT;
              EXCEPTION WHEN OTHERS THEN
              NULL;
      END;
  END LOOP;
END;
```

### Connection string from ORACLE to C Sharp

```
Data Source=(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=urHost)(PORT=urPort)))(CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=urOracleSID)));User Id=urUsername;Password=urPassword;

```

### Generate Class From Existing Database

```

Scaffold-DbContext 'Data Source=(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=urHost)(PORT=urPort)))(CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=urOracleSID)));User Id=urUsername;Password=urPassword; DBA Privilege=SYSDBA/DEFAULT' Oracle.EntityFrameworkCore -Tables universities -OutputDir Models 

```

### Oracle Map User Roles based on select query

```
DECLARE
  ROW_VALUE NUMBER;
  ROW_TABLE_NAME VARCHAR(200);
BEGIN
  FOR ROLESS IN (SELECT ID ROLE_ID FROM TBL_ROLE_INFORMATION WHERE ID IN (1,2,3,4,5,6,7,8))  LOOP
      BEGIN
              
              FOR USERSS IN (SELECT ID USER_ID FROM TBL_USERS WHERE USER_TYPE_ID=3)  LOOP
                  BEGIN
                          INSERT INTO TBL_USER_ROLE (USER_ID, role_info_id)
                          SELECT * FROM (
                          SELECT USERSS.USER_ID USER_ID, ROLESS.ROLE_ID ROLE_ID FROM DUAL
                          ) RUR WHERE NOT EXISTS (SELECT 1 FROM TBL_USER_ROLE EX 
                                    WHERE EX.USER_ID = RUR.USER_ID AND EX.role_info_id = RUR.ROLE_ID);
                          COMMIT;                         
                          EXCEPTION WHEN OTHERS THEN
                          NULL;
                  END;
              END LOOP;
      END;
  END LOOP;
END;

```