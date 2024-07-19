Go to Huginn installation folder

```
cd /home/huginn/huginn
sudo -u huginn -H editor config/unicorn.rb
```

change:  
listen "#{wd}/tmp/sockets/unicorn.socket"in config/unicorn.rb  
 to  
listen "127.0.0.1:3000"

Oh so cleverly adapted from [this page](https://gist.github.com/MrZYX/719014).

```
# Make sure mod_ssl, mod_rewrite, mod_headers, mod_proxy,
# mod_proxy_http and mod_proxy_balancer are enabled

<VirtualHost *:80>
    ServerName huginn.example.org
    RedirectPermanent / https://huginn.example.org/
</VirtualHost>
<VirtualHost *:443>
    ServerName huginn.example.org
    DocumentRoot /path/to/huginn/public

    RewriteEngine On

    RewriteCond %{DOCUMENT_ROOT}/%{REQUEST_FILENAME} !-f
    RewriteRule ^/(.*)$ balancer://upstream%{REQUEST_URI} [P,QSA,L]

    <Proxy balancer://upstream>
        BalancerMember http://127.0.0.1:3000
    </Proxy>

    ProxyRequests Off
    ProxyVia On
    ProxyPreserveHost On
    RequestHeader set X_FORWARDED_PROTO https

    <Proxy *>
        Order allow,deny
        Allow from all
    </Proxy>

    <Directory /path/to/huginn/public>
        Allow from all
        AllowOverride all
        Options -MultiViews
    </Directory>

    SSLEngine On
    SSLCertificateFile /path/to/cert
    SSLCertificateKeyFile /path/to/private_key
    # maybe not needed, need for example for startssl to point to a local
    # copy of http://www.startssl.com/certs/sub.class1.server.ca.pem
    SSLCertificateChainFile /path/to/chain_file
</VirtualHost>
```

**Please note:** If you have problems getting the above configuration to work, have a look at [this issue](https://github.com/huginn/huginn/issues/2322#issuecomment-399763418) for further information and an alternative configuration.

## Important:

In Apache 2.4 there are few changes do be done in .htaccess or VirtualHost setting. You need to replace Allow from and Deny from options with Require all granted and Require all denied as given below.

From

```
    <Proxy *>
        Order allow,deny
        Allow from all
    </Proxy>

    <Directory /path/to/huginn/public>
        Allow from all
        AllowOverride all
        Options -MultiViews
    </Directory>
```

to

```
    <Proxy *>
         Require all granted
    </Proxy>

    <Directory /path/to/huginn/public>
        Require all granted
        AllowOverride all
        Options -MultiViews
    </Directory>
```

More Information here: http://tecadmin.net/authz-core-error-client-denied-by-server-configuration/
