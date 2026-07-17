## Group Management

list groups for a user
``
groups testuser
``

list all groups
``
cat /etc/group
``

create group
``
sudo groupadd testgroup
``

delete group
``
sudo groupdel testgroup
``

add user to group
``
sudo usermod -aG testgroup testuser
-a append
-G Group
``

``
sudo gpasswd -a testgroup testuser
-a append
``

remove user from group 
``
sudo gpasswd -d testuser testgroup
``