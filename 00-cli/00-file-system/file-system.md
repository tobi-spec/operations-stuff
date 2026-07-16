## File System Commands

Create file with content
``
touch test.txt
touch "hello world" > test.txt
touch "hello world" >> test.txt
``


Current working dir
``
pwd
``

Directory content,
``
ls -la
a -> shows hidden directories
l -> long format display
R -> recursive
``

change into directory
``
cd
``

Delete file

``
rm -rf
r -> recursiv
f -> force
``

Show file content
``
cat test.txt
``

``
less test.txt
``

``
more test.txt
``

copy file
``
cp -r (source) (destination)
``

move and rename files
``
mv (source) (destination)
``

This finds files whose names contain "test"
``
find -type f -iname "*test"
-type d -> only directories
-type f -> only files
"*" -> part of filename
``

searches every printed line from less
``
less test.txt | grep hello
``

searches every printed line from ls
``
ls -laR | grep (part of file name)
``