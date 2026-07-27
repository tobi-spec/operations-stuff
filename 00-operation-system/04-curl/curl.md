## Curl 

-f (--fail): Bei HTTP Fehlern wie 404 oder 500 mit Fehler Exit Code abbrechen
-s (--silent): Progress Bar und Fortschritts Ausgabe unterdrücken
-S (--show-error): Zusammen mit -s Fehler trotzdem anzeigen
-L (--location): Redirects (301, 302) automatisch folgen
-I (--head): Nur HTTP Header abrufen, keinen Body
-o (--output): Response in Datei speichern
-O (--remote-name): Datei mit Original Namen speichern
-H (--header): Custom HTTP Header mitsenden
-d (--data): POST Body mitsenden
-X (--request): HTTP Methode setzen (GET, POST, PUT, DELETE, PATCH)
--max-time: Timeout in Sekunden
-v (--verbose): Debug Ausgabe mit Request und Response Headern


Runs curl, abort if error http status codes, doesn't show progress bar, shows errors and follows redirect.
Eventual runs the downloaded content as bash script
``
curl -fsSL https://bun.sh/install | bash
``

Pipes content in jq, without download bar
``
curl -s https://api.github.com/users/octocat | jq ".name"
``

now progress bar, but errors
``
curl -sS --max-time 10 https://nevercodealone.de/api/health
``

shows only the headers and follows redirects
``
curl -IL https://nevercodealone.de/glossare
``

saves body in file named after resource
``
curl -JO https://api.github.com/users/octocat
``

multiple authentication header
``
curl -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -H "X-Request-ID: $(uuidgen)" \
     -d '{"name":"Roland"}' \
     https://api.example.com/users
``

call a patch request and gets body from file
``
curl -X PATCH \
     -H "Content-Type: application/json" \
     --data-binary @update.json \
     https://api.example.com/users/123
``

shows exit status for previouse command
``
echo $?
``
