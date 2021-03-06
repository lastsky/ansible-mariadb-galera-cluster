Role Name
=========

An [Ansible] role to install/configure a [MariaDB-Galera Cluster]

Requirements
------------

None

Vagrant
-------
Spin up a test 3-node cluster using Vagrant....
````
git clone https://github.com/mrlesmithjr/ansible-mariadb-galera-cluster.git
cd Vagrant
vagrant up
````
When you are done testing tear it all down....  
````
./cleanup.sh
````

Role Variables
--------------

```
---
# defaults file for ansible-mariadb-galera-cluster

# Define the cacti user info for cacti db monitoring - If used. May remove later.
cacti_db_password: 'cactiuser'
cacti_db_user: 'cactiuser'

# Defines debian db password
# generate using echo password | mkpasswd -s -m sha-512
galera_deb_db_password: '{{ mariadb_mysql_root_password }}'

# Defines email address to receive notifications
galera_email_notifications: 'notifications@{{ mariadb_smtp_domain_name }}'

# Defines if cacti monitoring should be enabled for mysql - If used. May remove later.
galera_enable_cacti_monitoring: false

galera_enable_galera_monitoring_script: false

# Defines if we should enable the MariaDB repo or use version within OS repos.
galera_enable_mariadb_repo: true

# Defines if root logins should be allowed from any host
galera_allow_root_from_any: false

# Define the name of the cluster
galera_cluster_name: 'vagrant-test'

# Define bind address for galera cluster
# For example, if running in Vagrant define this as:
# '{{ ansible_eth1.ipv4.address }}' or any other interface address
galera_cluster_bind_address: '0.0.0.0'
galera_cluster_nodes_group: 'galera-cluster-nodes'
galera_monitor_script_name: 'galeranotify.py'
galera_monitor_script_path: '/etc/mysql'

# Defines the which node should be considered the master in the cluster
# Used to bootstrap cluster
galera_mysql_master_node: '{{ groups[galera_cluster_nodes_group][0] }}'

# Define email address that cluster notifications will be sent from
galera_notify_mail_from: 'galeranotify@{{ mariadb_smtp_domain_name }}'
# Define email address that cluster notification will be sent to
galera_notify_mail_to: '{{ galera_email_notifications }}'

# Define smtp server to send notifications through
galera_notify_smtp_server: '{{ mariadb_smtp_server }}'

# Defines if the cluster should be reconfigured
galera_reconfigure_galera: false

# MariaDB Repo Info
mariadb_debian_repo: 'deb [arch=amd64,i386,ppc64el] https://mirrors.evowise.com/mariadb/repo/{{ mariadb_version }}/{{ ansible_distribution|lower }} {{ ansible_distribution_release|lower }} main'
mariadb_debian_repo_key: '0xF1656F24C74CD1D8'
mariadb_debian_repo_keyserver: 'keyserver.ubuntu.com'
mariadb_debian_repo_pin: 'mirrors.evowise.com'
mariadb_redhat_repo: 'http://yum.mariadb.org/{{ mariadb_version }}/{{ ansible_distribution|lower }}{{ ansible_distribution_major_version|int}}-amd64'
mariadb_redhat_repo_key: 'https://yum.mariadb.org/RPM-GPG-KEY-MariaDB'
mariadb_version: '10.1'

# Define mysql root password
# generate using echo password | mkpasswd -s -m sha-512
mariadb_mysql_root_password: 'root'

# Define the primary domain name of your environment
mariadb_pri_domain_name: 'example.org'

# Define smtp domain for email
mariadb_smtp_domain_name: '{{ mariadb_pri_domain_name }}'

# Define smtp server to send email through
mariadb_smtp_server: 'smtp.{{ mariadb_pri_domain_name }}'
```

Dependencies
------------

None

Example Playbook
----------------


License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com

[Ansible]: <https://www.ansible.com>
[MariaDB-Galera Cluster]: <https://mariadb.com/kb/en/mariadb/what-is-mariadb-galera-cluster/>
