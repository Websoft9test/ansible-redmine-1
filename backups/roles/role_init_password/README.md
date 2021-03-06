Ansible Role: init_password
=========

在CentOS或者Ubuntu服务器上初始化随机密码

Requirements
------------

无特殊要求,此 role 需要 root 用户权限,可以在playbook全局加入 `become: yes`,或者如下调用 role:

```
- hosts: all
  roles:
    - role: init_password
      become: yes
```

Role Variables
--------------

下面列出了可用变量和默认值(请参见"defaults/main.yml"):

```
init_db: 
  mysql:
    user: root
    password: 123456

  # postgrepsql:
  #   user: postgres
  #   password: ABCDEFG

  # mongodb:
  #   user: root
  #   password: mongodb_pass


init_application:
  application_name: 
  application_service:
  application_database: 
  application_database_user:
  application_database_host: 
  application_database_password: 
  application_config_path: []



```



Dependencies
------------

None

Example Playbook
----------------

```
- hosts: all
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - { role: mysql }
    - { role: init_password }
```

`vars/main.yml` :
```
mysql_version: 5.7
mysql_root_password: 123456  

mysql_databases: 
  - name: example 
    encoding: utf8mb4

  
mysql_users: 
  - name: example
    host: locahost
    password: example_password
    priv: 'example.*:ALL'


init_db: 
  mysql:
    user: root
    password: 123456


init_application:
  application_name: example
  application_service: php-fpm
  application_database: example 
  application_database_user: example
  application_database_host: localhost
  application_database_password: example_password
  application_config_path: 
    - /data/config/example.config

```

License
-------

BSD

