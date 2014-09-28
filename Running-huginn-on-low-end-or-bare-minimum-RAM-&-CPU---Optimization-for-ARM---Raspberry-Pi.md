## huginn + sysvinit + unicorn + mysql + nginx can be at your service on: Raspberry Pi Model A 256 MB RAM @ 900 MHz

Please help improve these instructions - the mysql and nginx settings are experimental and for using huginn to serve only to one or a "few" users - 
please share your experience.

### Disable all unnecessary Agents in your Gemfile
```
/you/huginn/Gemfile
```
### Use Init Script instead of Upstart 

If you want to deploy via the Capistrano Tutorial but want to use Init Script to skip on upstart then 
include the following foreman export gem in your Gemfile.
```
gem 'foreman-export-initscript'
```

and then also adjust the deploy.rb file to make changes from upstart to initscript to the namespace :foreman do section
```
namespace :foreman do
  desc "Export the Procfile to Ubuntu's upstart scripts"
  task :export, :roles => :app do
    run "cd #{latest_release} && sudo bundle exec foreman export initscript /etc/init.d -a #{application} -u #{user} -l #{deploy_to}/init_logs"
    run "sudo chmod +x /etc/init.d/huginn"
  end

  desc 'Start the application services'
  task :start, :roles => :app do
    sudo "sudo service #{application} start"
  end

  desc 'Stop the application services'
  task :stop, :roles => :app do
    sudo "sudo service #{application} stop"
  end

  desc 'Restart the application services'
  task :restart, :roles => :app do
    run "sudo service #{application} start || sudo service #{application} restart"
  end
end
```


### Optimizing Mysql
The following is used as a mysql bare minimum for a single user huginn deployment set inside the /etc/mysql/my.cnf
taken from /usr/share/doc/mysql-server-5.5/examples/my-small.cnf
please make improvements and explanations

Example MySQL config file for minimal systems `etc/mysql/my.cnf`
```
[client]
port            = 3306
socket          = /var/run/mysqld/mysqld.sock

#Here follows entries for some specific programs

#The MySQL server
[mysqld]
port            = 3306
socket          = /var/run/mysqld/mysqld.sock

#Disable InnoDB and switch to MyISAM to save RAM
skip-innodb
default-storage-engine = myisam

skip-external-locking
key_buffer_size = 16K
max_allowed_packet = 1M
#How many tables do we need cached for huginn?
table_open_cache = 4
sort_buffer_size = 64K
read_buffer_size = 256K
read_rnd_buffer_size = 256K
net_buffer_length = 2K
thread_stack = 128K
query_cache_type = 1
query_cache_limit = 256
#going low on the query_cache_size value - how do we find the right values?
query_cache_size = 1M
server-id       = 1

[mysqldump]
quick
max_allowed_packet = 16M

[mysql]
no-auto-rehash
#Remove the next comment character if you are not familiar with SQL
#safe-updates

[myisamchk]
key_buffer_size = 8M
sort_buffer_size = 8M

[mysqlhotcopy]
interactive-timeout
```

## Optimizing Nginx
This is a bare minimum configuration for a single user huginn deployment set inside the /etc/nginx/conf.d/default.conf and /etc/nginx/nginx.conf and using unicorn as the upstream
please adjust to your needs and share updates - the goal is to get the most out of low end boxes

change you into your user name and adjust  server_name and the root accordingly in file
 /etc/nginx/conf.d/default.conf

```
upstream huginn_server {
  server unix:/home/you/app/shared/pids/unicorn.socket;
}

  server {
    listen 80;
    server_name 192.168.1.20;
    root /home/you/app/current/public;
    try_files $uri/index.html $uri.html $uri @app;
    error_page 500 502 503 504 /500.html;
    location = /500.html {
      root /home/you/app/current/public;
    }
    location @app {
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_set_header Host $http_host;
      proxy_redirect off;
      proxy_pass http://huginn_server;
    }
  }

```


change you into your user name and adjust  server_name and the root accordingly in file 
/etc/nginx/nginx.conf


```
user www-data;
worker_processes 1;
pid /var/run/nginx.pid;

events {
        worker_connections 8;
        # multi_accept on;
        accept_mutex on;

}

http {

        ##
        # Basic Settings
        ##

        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;
        # server_tokens off;

        # server_names_hash_bucket_size 64;
        # server_name_in_redirect off;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        ##
        # Logging Settings
        ##

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        ##
        # Gzip Settings
        ##

        gzip on;
        gzip_disable "msie6";

        #gzip_vary on;
        #gzip_proxied any;
        #gzip_comp_level 3;
        #gzip_buffers 16 8k;
        #gzip_http_version 1.1;
        #gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;

        ##
        # nginx-naxsi config
        ##
        # Uncomment it if you installed nginx-naxsi
        ##

        #include /etc/nginx/naxsi_core.rules;
        # nginx-passenger config
        ##
        # Uncomment it if you installed nginx-passenger
        ##

        #passenger_root /usr;
        #passenger_ruby /usr/bin/ruby;

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}


#mail {
#       # See sample authentication script at:
#       # http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#       # auth_http localhost/auth.php;
#       # pop3_capabilities "TOP" "USER";
#       # imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#       server {
#               listen     localhost:110;
#               protocol   pop3;
#               proxy      on;
#       }
#
#       server {
#               listen     localhost:143;
#               protocol   imap;
#               proxy      on;
#       }
#}

```


### Disable OpenSSH Server and enable Dropbear
(instructions comming soon)


