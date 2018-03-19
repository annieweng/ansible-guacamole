# ansible-guacamole

This module, use mysql database to store connection info, and support ldap/freeipa with ldap user/group filtering.
to ensure it work correctly, first create a guacadmin user in your current ldap database, take a note of user password you set it to. while it's not neccessary to have same password
on mysql, it's less confusing if we could keep both password same. 
if sepecific ldap user group will be used for filtering, add guacadmin user to that group as well.



install apache guacamole server with ansible with ansible-play -v playbooks/server.yml. this will setup guacamole server and client in one machine
change version desire on default/main.yml file.

it install mysql and ldap extension.
Current guacamole version: **0.9.14**
Current guacamole client version: including war  and extensions: **0.9.14**
Current tomcat version: **tomcat8** (Ubuntu), **tomcat** (CentOS)


GUACAMOLE_HOME is default to `/usr/share/{{ TOMCAT_VERSION }}/.guacamole`, it's also soft link to /etc/guacamole.

once complete. navigate to $host:8080/guacamole, login with guacadmin/guacadmin(default mysqldb password), and go to setting/preferences/change password to change password to match the one in ldap.

navigate to users tab, it should list all users from ldap.








