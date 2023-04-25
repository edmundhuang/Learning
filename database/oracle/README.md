### Oracle

Connection to Oracle
Type : TNS/Direct/LDAP


Parameter (Direct):
* Host
* Port - 1521
* Service Name  / SID

* User ID
* Password

### Toad for Oracle Database



### Create readonly role 
1. Create role "ReadOnlyRole"
2. Run script to grant all "Select" privileges or use UI to grant it.
```
-- SYSTEM PRIVILEGES
GRANT SELECT ANY MINING MODEL TO "ReadOnlyRole" ;
GRANT SELECT ANY TABLE TO "ReadOnlyRole" ;
GRANT SELECT ANY CUBE DIMENSION TO "ReadOnlyRole" ;
GRANT SELECT ANY SEQUENCE TO "ReadOnlyRole" ;
GRANT SELECT ANY TRANSACTION TO "ReadOnlyRole" ;
GRANT SELECT ANY DICTIONARY TO "ReadOnlyRole" ;
GRANT SELECT ANY CUBE TO "ReadOnlyRole" ;
```

3. Create user with "ReadOnlyRole" 
-- USER SQL
CREATE USER "DevReadOnly" IDENTIFIED BY "Test1234"  ;

-- QUOTAS

-- ROLES
GRANT "ReadOnlyRole" TO "DevReadOnly" ;

-- SYSTEM PRIVILEGES

CREATE USER "DevReadOnly" IDENTIFIED BY "Test1234"  
DEFAULT TABLESPACE "OPERA_DATA"
TEMPORARY TABLESPACE "TEMPSEG";

-- QUOTAS

-- ROLES
GRANT "CONNECT" TO "DevReadOnly" ;
GRANT "ReadOnlyRole" TO "DevReadOnly" ;


1.1 Work
```
CREATE USER ro_user
 IDENTIFIED BY ro_user
 DEFAULT TABLESPACE OPERA_DATA
 TEMPORARY TABLESPACE TEMPSEG;
```

1.2 
```
GRANT CREATE SESSION to ro_user
```

1.3. Grant all select privilege to user
```
GRANT SELECT ANY MINING MODEL TO "ro_user" ;
GRANT SELECT ANY TABLE TO "ro_user" ;
GRANT SELECT ANY CUBE DIMENSION TO "ro_user" ;
GRANT SELECT ANY SEQUENCE TO "ro_user" ;
GRANT SELECT ANY TRANSACTION TO "ro_user" ;
GRANT SELECT ANY DICTIONARY TO "ro_user" ;
GRANT SELECT ANY CUBE TO "ro_user" ;
``


set default schema for user.
````
alter session set current_schema = otheruser; 
```