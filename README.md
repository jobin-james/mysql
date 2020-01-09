# Introduction

This role can be used to install and configure mysql server, create databases, and users.

```code
# Basic settings
mysql_port: 3306
mysql_bind_address: "0.0.0.0"
mysql_root_password: '123'
mysql_language: '/usr/share/mysql/'
mysql_ppa: ''
mysql_apt_key: ''
```
Decalare the Basic settings

### If you wish to fine tune the mysql, adjust the parameter
```code
# Fine Tuning
mysql_key_buffer: '16M'
mysql_max_allowed_packet: '128M'
mysql_thread_stack: '192K'
mysql_cache_size: 8
#mysql_myisam_recover: 'BACKUP'
mysql_max_connections: 100
mysql_table_cache: 64
# mysql_thread_concurrency: 10
mysql_query_cache_limit: '1M'
mysql_query_cache_size: '16M'
mysql_character_set_server: 'utf8'
mysql_collation_server: 'utf8_general_ci'
mysql_mysqldump_max_allowed_packet: '128M'
# mysql_isamchk_key_buffer: '16M'
```
### If you wish to fine tune the innodb, adjust the parameter
```code
# InnoDB tuning
mysql_innodb_file_per_table: 'innodb_file_per_table'
mysql_innodb_flush_method: 'fdatasync'
mysql_innodb_buffer_pool_size: '128M'
mysql_innodb_flush_log_at_trx_commit: 1
mysql_innodb_lock_wait_timeout: 50
mysql_innodb_log_buffer_size: '1M'
mysql_innodb_log_file_size: '5M'

# Full-Text Search
mysql_ft_min_word_len: 4
```

### Databases to be created
```code
# List of databases to be created
mysql_databases:
  - name: db
    collation: "utf8_general_ci"
    encoding: "utf8"     
```
### Users to be created
```code
# List of users to be created
mysql_users:
  - name: user
    pass: guacamole
    priv: "*.*:ALL" 
    host: "localhost" 

```
### Mysql package to be installed
```code
# List of apt packages to install
mysql_packages:
  - mysql-server
  - mysql-client
  - python-mysqldb
  - python3-pymysql
```


## How to run the playbook

Clone this repo to your roles folder and adjust the parameters

Create a `mysql.yml` file
```code
---
- hosts: dbserver
  become: yes
  roles:
    - mysql
```
run the playbook by 

`ansible-playbook -i hosts mysql.yml`
