# ansible-oracle-modules
Oracle modules for Ansible

If you have any questions/requests just create an issue and I'll look into it
I've alsi included a playbook (test-modules.yml) that'll give you an idea on how the modules can be used.

To use the modules, create a 'library' directory next to your top level playbooks and put the different modules in that directory. Then just reference them as you would any other module.
For more information, check out: http://docs.ansible.com/developing_modules.html


Most (if not all) requires cx_Oracle either on your controlmachine or on the managed node

These are the different modules:

<b> oracle_user </b>

pre-req: cx_Oracle

 - Creates & drops a user. 
 - Grants privileges only (can not remove them with oracle_user, use oracle_grants for that)

<b> oracle_tablespace </b>

pre-req: cx_Oracle

 - Manages normal(permanent), temp & undo tablespaces (create, drop, make read only/read write, offline/online)
 - Tablespaces can be created as bigfile, autoextended


<b> oracle_grants </b>

pre-req: cx_Oracle

 - Manages privileges for a user
 - Grants/revokes privileges
 - Handles roles/sys privileges properly. Does NOT yet handle object privs. They can be added but they are not considered while revoking privileges
 - The grants can be added as a string (dba,'select any dictionary','create any table'), or in a list (ie.g for use with with_items)

<b> oracle_role </b>

pre-req: cx_Oracle

 - Manages roles in the database

<b> oracle_parameter </b>

pre-req: cx_Oracle

 - Manages init parameters in the database (i.e alter system set parameter...)
 - Also handles underscore parameters. That will require using mode=sysdba, to be able to read the X$ tables needed
 to verify the existence of the parameter.
