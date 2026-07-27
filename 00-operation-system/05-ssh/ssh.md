# SSH

use ssh
``
ssh <username>@<ip/domain>
``

## use scp
``
scp  <source> <destination>
``

Upload file to remote server
``
scp /my/file.txt myuser@1.1.1.1:/myuser/demo.txt
``

Download file from remote server to home directory
``
scp myuser@1.1.1.1:/myuser/demo.txt ~/
``

Download directory from remote server to home directory
``
scp -r myuser@1.1.1.1:/myuser/demo.txt ~/
``

## rsync
synchronise to directories on different machines
``
rsync <source> <destination>
``

synchronise configs folder
``
rsynv -av ~/configs myuser@1.1.1.1:~/configs
``

