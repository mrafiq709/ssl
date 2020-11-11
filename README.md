# ssl-nginx-localhost

Generate private key
--------------------
    openssl genrsa -des3 -out myCA.key 2048
    
Generate root certificate
------------------------------
    openssl req -x509 -new -nodes -key myCA.key -sha256 -days 825 -out myCA.pem

Create CA-signed certs
----------------------

    NAME=mydomain.com # Use your own domain name
    
Generate a private key
----------------------
    openssl genrsa -out $NAME.key 2048
    
Create a certificate-signing request
------------------------------------------
    openssl req -new -key $NAME.key -out $NAME.csr
    
Create a config file for the extensions
---------------------------------------
  ```
  >$NAME.ext cat <<-EOF
  authorityKeyIdentifier=keyid,issuer
  basicConstraints=CA:FALSE
  keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
  subjectAltName = @alt_names
  [alt_names]
  DNS.1 = $NAME # Be sure to include the domain name here because Common Name is not so commonly honoured by itself
  DNS.2 = bar.$NAME # Optionally, add additional domains (I've added a subdomain here)
  IP.1 = 127.0.0.1 # Optionally, add an IP address (if the connection which you have planned requires it)
  EOF
  ```
Create the signed certificate
---------------------------------
    openssl x509 -req -in $NAME.csr -CA myCA.pem -CAkey myCA.key -CAcreateserial \
    -out $NAME.crt -days 825 -sha256 -extfile $NAME.ext
    
At this point we have 7 files
-------------------------------
```
  - mydomain.com.crt
  - mydomain.com.ext
  - mydomain.com.csr
  - mydomain.com.key
  - myCA.srl
  - myCA.pem
  - myCA.key
  ```
Copy `mydomain.com.crt` and `mydomain.com.key` to `/etc/ssl/` folder

Import Certificate Authority to Chrome
---------------------------------------
```
chrome
|__Settings
   |__Secutity
      |__Manage certificates
         |__Authorities
            |__Import
            
 Select "myCA.pem" and import.
 ```
    
Server Config [Nginx]
---------------------------
```
server {
        listen 443 ssl;
        listen [::]:443 ssl;
        ssl_certificate /etc/ssl/mydomain.com.crt;
        ssl_certificate_key /etc/ssl/mydomain.com.key;

        server_name mydomain.com www.mydomain.com;
        root /var/www/one;
        index index.html index.php;

        location / {
            proxy_pass http://localhost:3000;
        }
}


server {
    listen 80;
    listen [::]:80;

    server_name mydomain.com www.mydomain.com;

    return 302 https://$server_name$request_uri;
}
```
Now Restart nginx server

<a href="https://i.imgur.com/RC3rSmI.png"><img src="https://i.imgur.com/RC3rSmI.png" title="source: imgur.com" /></a><br/><br/>

##### Reference
https://stackoverflow.com/questions/7580508/getting-chrome-to-accept-self-signed-localhost-certificate?page=1&tab=votes#tab-top
