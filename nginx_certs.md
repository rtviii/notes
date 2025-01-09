This is how one of my httpd configs looks like. I'm interested in migrating this
to an equivalent nginx virtual host.

```
<VirtualHost *:80>
    ServerAdmin rtkushner@gmail.com
    DocumentRoot /var/www/r8-kdd.math.ubc.ca
    ServerName r8-kdd.math.ubc.ca
    ServerAlias www.r8-kdd.math.ubc.ca

    <Directory /var/www/r8-kdd.math.ubc.ca>
           #Allowoverride all    ###Uncomment if required
    </Directory>

    ErrorLog logs/r8-kdd_error.log
    CustomLog logs/r8-kdd_access.log combined

        RewriteEngine On
        RewriteCond %{HTTPS} off
        RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [R=302,L,QSA]


    #ProxyPreserveHost On
    #ProxyPass "/" "http://127.0.0.1:8000/"
    #ProxyPassReverse "/" "http://127.0.0.1:8000/"
RewriteCond %{SERVER_NAME} =www.r8-kdd.math.ubc.ca [OR]
RewriteCond %{SERVER_NAME} =r8-kdd.math.ubc.ca
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>

<VirtualHost *:443>
    ServerAdmin rtkushner@gmail.com
    DocumentRoot /var/www/r8-kdd.math.ubc.ca

    ServerName r8-kdd.math.ubc.ca
    ServerAlias www.r8-kdd.math.ubc.ca

    <Directory /var/www/r8-kdd.math.ubc.ca>
           #Allowoverride all    ###Uncomment if required
    </Directory>

    SSLEngine on

    ErrorLog logs/r8-kdd_ssl-error.log
    CustomLog logs/r8-kdd_ssl-access.log combined


    ProxyPreserveHost On
    ProxyPass "/""http://127.0.0.1:8000/"
    ProxyPassReverse "/""http://127.0.0.1:8000/"
    SSLCertificateFile        /etc/letsencrypt/live/r8-kdd.math.ubc.ca/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/r8-kdd.math.ubc.ca/privkey.pem
    Include /etc/letsencrypt/options-ssl-apache.conf
</VirtualHost>
```


Lwhile preserving all the tls securityet's try to keep track of the TLS Certificate's moving pieces:
```
    SSLCertificateFile        /etc/letsencrypt/live/r8-kdd.math.ubc.ca/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/r8-kdd.math.ubc.ca/privkey.pem
    Include /etc/letsencrypt/options-ssl-apache.conf
    SSLEngine on
```

We find the following at `/etc/letsencrypt/live`, which is basically the 4
parts:

```
This directory contains your keys and certificates.

`[cert name]/privkey.pem`  : the private key for your certificate.
`[cert name]/fullchain.pem`: the certificate file used in most server software.
`[cert name]/chain.pem`    : used for OCSP stapling in Nginx >=1.3.7.
`[cert name]/cert.pem`     : will break many server configurations, and should not be used
                 without reading further documentation (see link below).

WARNING: DO NOT MOVE OR RENAME THESE FILES!
         Certbot expects these files to remain in this location in order
         to function properly!

We recommend not moving these files. For more information, see the Certbot
User Guide at https://certbot.eff.org/docs/using.html#where-are-my-certificates.
```

What does each do and is there anything else that's necessary to create a a viable
443 Nginx Host?


This is a good explanation of what is meant by a certificate *chain* : https://support.dnsimple.com/articles/what-is-ssl-certificate-chain/.





