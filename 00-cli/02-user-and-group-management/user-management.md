# User Management

show users
``
ls -la /home
``
show all, also technical, users
``
cat /etc/passwd
``
get user from passwd
``
cat /etc/passwd | grep testuser
``

create a user
``
sudo useradd -m testuser
``

remove user
``
sudo userdel -r testuser
``

set password
``
sudo passwd testuser
``

create system user
``
sudo useradd -r sysuser
``

field 1: username
field 2: password(encrypted)
field 3: userid: 1000+ -> humans, 1000- -> programms
field 4: user group
field 5: user informations field -> first- and lastname
field 6: home directory
field 7: shell
``
testuser:x:1001:1001::/home/testuser:/bin/sh
``

change to user
``
sudo su - testuser
``