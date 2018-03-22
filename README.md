# ansible-guacamole

This ansible module build apache guacamole https://guacamole.apache.org/ with mysql and ldap extensions as authentication source.

## Description

The module configured mysql database to store connection info, and add extension support to ldap/freeipa with ldap user/group filtering.   
  * ansible: 2.4+
  * OS: Ubuntu 16.04 and Centos 7
  * should work with earlier version, not tested.
## Assumption:
   * you have a working ldap server. 
   * you have create a guacadmin user in your ldap server.
   * if you are using "ldap-user-search-filter", make sure guacadmin user is also a member of user group that you would be filtering. this is needed in order for guacamole to see all users in ldap.
   * take a note of password for the guacadmin user. you will NEED to have same password in mysql database for the application to see all users in ldap that match criteria.
   
   
## Installation/Configuration

1.  we use ansible-vault to store sensitive information, ie database password, ldap bind info. to create your own vault.xml: 
   * create a .vault_pass file and enter your pass phrase in the file. 
     this file is added in .gitignore, therefore will not be checking into git repo. 
   * ansible-vault create group_vars/all/vault.yml --vault-password-file=.vault_pass
   and fill in all vault value. see roles/server/var/vault.xml.template as example
   * use ansible-playbook --ask-vault-pass if prefer. just update ansible.cfg to reflect the option.
   
2. change value on group_var/all/vars.yml file to your own environment, then 'ansible-play -v playbooks/server.yml',  this will setup guacamole server and client in one machine

  * Current guacamole version: **0.9.14**  
  * Current guacamole client version: including war  and extensions: **0.9.14**  
  * Current tomcat version: **tomcat8** (Ubuntu), **tomcat** (CentOS)  
  * GUACAMOLE_HOME is default to `/usr/share/{{ TOMCAT_VERSION }}/.guacamole`, it's also soft link to /etc/guacamole.  
  

3.  navigate to $host:8080/guacamole, login with guacadmin/guacadmin(default mysqldb password), and go to setting/preferences/change password to change password to match the one in ldap. logout, then login again with your new password. 
navigate to users tab, it should now list all users from ldap that match ldap parameters.











