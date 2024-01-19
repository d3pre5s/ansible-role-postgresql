PostgreSQL
=========

Playbook for postgreSQL

VSEM PRIVET  

Requirements
------------
-

Role Variables
--------------

```
# validate certs for postgresql repo key
postgresql_validate_certs: "yes"

# postgresql apt key name
postgresql_apt_key: "ACCC4CF8.asc"

# version of postgresql (9.1, 9.2, 9.3, 9.4, 9.5, 9.6, 10, 11)
postgresql_version: 12

# version of postgis (2.4, etc)
postgresql_postgis_version: []
postgresql_postgis_names:
    - "postgresql-{{ postgresql_version }}-postgis-{{ postgresql_postgis_version }}"
    - "postgresql-{{ postgresql_version }}-postgis-{{ postgresql_postgis_version }}-scripts"

# Database port to connect to
postgresql_port: 5432

# Path to postgresql.conf
postgresql_config_path: "/etc/postgresql/{{ postgresql_version }}/main"
# Options for postgresql config
postgresql_config_options:
  - option: listen_addresses
    value: "*"
    state: 'present' # present (default)| absent
  - option: port
    value: "{{ postgresql_port }}"

# Options for createcluster config, used for creating folders' tree
postgresql_cluster_options: []

# list of database users
postgresql_users: []
#  - name:
#    password:
#    encrypted: no (optional)
#    role_attr_flags: NOSUPERUSER (optional) http://docs.ansible.com/ansible/latest/postgresql_user_module.html#options

# list of databases
postgresql_dbs: []
#  - db:
#    user:
#    encoding: UNICODE (optional)
#    ext: (optional)
#      - ext1
#      - ext2
#    schema: (optional)
#      - schema1
#      - schema2

# flag to create the databases
postgresql_create_db: true

# path to template of pg_hba.conf
postgresql_pghba_template_path: "{{ role_path }}/templates/pg_hba.conf.tpl"

```

Dependencies
------------
-

Example Playbook
----------------
main.yml
```
---
- hosts: db
  roles:
    - postgresql
```
group_vars/db/main.yml
```
---
postgresql_users:
  - user: test
    password: "strong_password_1"

postgresql_dbs:
   - db: test_db
     user: test
     host: 1.0.0.29/32
```

License
-------

BSD

Author Information
------------------

Konstantin Deepezh, https://t.me/deusops
