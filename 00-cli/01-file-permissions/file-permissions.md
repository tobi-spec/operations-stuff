## FIle Permissions

d|rwx|r-x|r-x  3 root root     4096 Jul 18  2025 ..
-|rw-|r--|r--  1 tobi tobi        0 Jul 16 15:16 test.txt

1. part: directory or file
2. part: permissions for user (u)
3. part: permissions for user group (g)
4. part: permissions for other (o)

r -> read
w -> write
x -> file can be executed aka. run as script
  -> directory can be cd into


add permissions, make file executable for everyone  
``
chmod +x test.txt
``

remove permissions for user
``
chmod u-x test.txt
``

each permission has a numeric representation
r=4 w=2 x=1

gives all permissions to everyon (user, group, other)
``
chmod 777 test.txt
``

gives all permissions to user and read/write to group
``
chmod 760 test.txt
``

recursively change permission for directory to read/write for user
``
chmod -R 600 Downloads
``