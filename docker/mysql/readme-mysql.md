# MySql  
- 이미지 빌드  
```bash
docker build -t mysql-tmp .
```

- 사용하기  
```bash
docker run -it --name mysql -d mysql-tmp 
docker exec -it mysql /bin/bash
```

```sql
-- 172.17.0.2 
show databases;
select host, user, authentication_string from mysql.user;
quit;
```

```bash
docker run -it --name mysql2 mysql-tmp /bin/bash  
mysql -h172.17.0.2 -uhive -phive -Dmetastore  
#==> ERROR 2003 (HY000)
grep ^bind-address /etc/mysql/my.cnf 
# vi /etc/mysql/mysql.conf.d/mysqld.cnf
# bind-address 0.0.0.0
```

## Hue database 생성  
```sql
set global validate_password_policy=LOW;
set global validate_password_length=3;
CREATE USER 'hue'@'%' IDENTIFIED BY 'pwd_hue';
CREATE DATABASE hue;
GRANT ALL privileges on hue.* to 'hue'@'%' with GRANT option;
flush privileges;
```