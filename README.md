# ansible-guacamole

This ansible module build apache guacamole https://guacamole.apache.org/ with mysql and ldap extensions as authentication source.

## Description

The module configured mysql database to store connection info, and add extension support to ldap/freeipa with ldap user/group filtering.  
  * ansible: 2.4+
  * OS: Ubuntu and Centos

## installation/Configuration
1. to ensure it work correctly, first create a guacadmin user in your current ldap database, take a note of user password you set it to. while it's not neccessary to have same password on mysql, it's less confusing if we could keep both password same. if sepecific ldap user group will be used for filtering, add guacadmin user to that group as well.

2.  ansible-vault create/edit roles/server/var/vault.xml and fill in all vault value. see roles/server/var/vault.xml.template as example

3. change version desire on default/main.yml file, then 'ansible-play -v playbooks/server.yml',  this will setup guacamole server and client in one machine

  * Current guacamole version: **0.9.14**  
  * Current guacamole client version: including war  and extensions: **0.9.14**  
  * Current tomcat version: **tomcat8** (Ubuntu), **tomcat** (CentOS)  
  * GUACAMOLE_HOME is default to `/usr/share/{{ TOMCAT_VERSION }}/.guacamole`, it's also soft link to /etc/guacamole.  
  

4.  navigate to $host:8080/guacamole, login with guacadmin/guacadmin(default mysqldb password), and go to setting/preferences/change password to change password to match the one in ldap.
navigate to users tab, it should list all users from ldap.








