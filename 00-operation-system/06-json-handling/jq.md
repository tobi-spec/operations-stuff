## jq


gives json as pretty print
``
jq "." test.json
``

gives second level of nested json
``
jq "user.name" test.json
``

gives second level of nested json without brackets for pipe
``
jq "user.name" test.json -r
``

gives object in list, can be indexed
``
jq "user.names[]" test.json 
``