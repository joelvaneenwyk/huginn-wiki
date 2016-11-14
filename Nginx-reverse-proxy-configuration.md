The settings below configures Nginx as a reverse proxy with the following assumptions:
* Huginn is running on machine with **IP** _127.0.0.1_ and listens on **port** _3000_
* Application is available only over **HTTPS** protocol and **FORCE_SSL** is set to _true_ in Huginn configuration
* Public domain name for the application is _huginn.server.com_

    server {
        # Make it available from the Internet
        allow all;
    
        listen 80;
    
        # server names for this server.
        # any requests that come in that match any these names will use the proxy.
        server_name huginn.server.com;
        access_log /var/log/nginx/huginn.server.com-access.log;
        error_log /var/log/nginx/huginn.server.com-error.log;
    
        location / {
            proxy_pass http://127.0.0.1:3000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    
        listen 443 ssl;
    
        # Setup SSL certificate with Let's Encript (https://letsencrypt.org/) 
        ssl_certificate /etc/letsencrypt/live/huginn.server.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/huginn.server.com/privkey.pem;
        include /etc/letsencrypt/options-ssl-nginx.conf;
        ssl_trusted_certificate /etc/letsencrypt/live/huginn.server.com/chain.pem;
        ssl_stapling on;
        ssl_stapling_verify on;
    
        if ($scheme != "https") {
            return 301 https://$host$request_uri;
        }
    }