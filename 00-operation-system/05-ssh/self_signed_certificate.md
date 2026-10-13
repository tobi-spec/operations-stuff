# Self Signed Certificates


## Create a private CA:

openssl genrsa -out client-ca.key 4096

openssl req -x509 -new -nodes \                                                                                                                                                                                                   
-key client-ca.key \                                                                                                                                                                                                            
-sha256 \                                                                                                                                                                                                                       
-days 3650 \                                                                                                                                                                                                                    
-out client-ca.crt \                                                                                                                                                                                                            
-subj "/CN=Outsmart AI Client CA"    


## Create a client key and certificate request:

openssl genrsa -out firefox-client.key 4096

openssl req -new \                                                                                                                                                                                                                
-key firefox-client.key \                                                                                                                                                                                                       
-out firefox-client.csr \                                                                                                                                                                                                       
-subj "/CN=firefox-client-1" 

## Sign the client certificate with your CA:

openssl x509 -req \                                                                                                                                                                                                               
-in firefox-client.csr \                                                                                                                                                                                                        
-CA client-ca.crt \                                                                                                                                                                                                             
-CAkey client-ca.key \                                                                                                                                                                                                          
-CAcreateserial \                                                                                                                                                                                                               
-out firefox-client.crt \                                                                                                                                                                                                       
-days 365 \                                                                                                                                                                                                                     
-sha256 

## Export it for Firefox:

openssl pkcs12 -export \                                                                                                                                                                                                          
-out firefox-client.p12 \                                                                                                                                                                                                       
-inkey firefox-client.key \                                                                                                                                                                                                     
-in firefox-client.crt \                                                                                                                                                                                                        
-certfile client-ca.crt  

## Import in Firefox profile

apt install libnss3-tools

pk12util -i firefox-client.p12 \                                                                                                                                                                                            
-d sql:.config/mozilla/firefox/8aoaqn6u.default