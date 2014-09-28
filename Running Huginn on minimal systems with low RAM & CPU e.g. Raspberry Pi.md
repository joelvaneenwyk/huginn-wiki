**While this works, the resulting system is VERY SLOW (1-5 sec response time)**

It is possible to run Huginn on low end hardware such as single core ARM boards or older x86 hardware. The minimum requirements are yet to be specified.
Serving only a single user for an example:  huginn + sysvinit + unicorn + mysql + nginx can be at your service on: **Raspberry Pi 256 MB RAM, 4GB SD @ 900 MHz**

Before deploying Huginn make sure you use a suitable "lightweight" OS distribution for your minimal server. For the RPi Raspbian works quite responsive after some optimization.
Also remove all unnecessary packages and services and tweak the system to free as much RAM & CPU.
Please help improve these instructions - the mysql and nginx settings are experimental and for using huginn to serve only to one or a "few" users - 
please share your experience.

### Tuning Huginn for low Memory usage

To free up memory disable any unused optional Agent in huginn/Gemfile (read the inside comments for instructions). It is also possible to lower the refresh activity of huginn/lib/huginn_scheduler.rb - by default the frequency is set to 0.3s. You can change and experiment by adding (frequency: x) to the Scheduler.new (make link to comment by knu)

On the RPi a value of 3 is working well.

```
.
.
def initialize
  @rufus_scheduler = Rufus::Scheduler.new(frequency: 3)
  self.mutex = Mutex.new
end
.
.
```



### Assign and setup a static IP for your server and disable the DHCP entries 
for faster startup, memory and cpu savings edit your /etc/network/interfaces
e.g.:
````
auto lo
iface lo inet loopback
iface eth0 inet static
address 192.168.1.20
gateway 192.168.1.1
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
```



### Use Init Script instead of Upstart on Raspbian (Debian)

If you want to deploy via the [Capistrano Tutorial](https://github.com/cantino/huginn/wiki/Deployment-with-Capistrano,-Unicorn,-nginx,-Foreman,-and-Upstart) but want to use SysVinit instead of upstart - then 
include the following foreman export gem in your Gemfile.
```
gem 'foreman-export-initscript'
```

and then also adjust the deploy.rb file to make changes from upstart to initscript to the namespace :foreman do section accordingly
```
.
.
.
namespace :foreman do
  desc "Export the Procfile to init scripts"
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
.
.
.
```


### Optimizing Mysql - Switch to MyIsam + using Tuning Scripts

Use /usr/share/doc/mysql-server-5.5/examples/my-small.cnf  to replace (make backup beforehand) /etc/mysql/my.cnf and add/edit the following to switch to MyIsam. Do this before you run any deploy, rake db scripts on your server.

```
#Disable InnoDB and switch to MyISAM to save RAM
skip-innodb
default-storage-engine = myisam

```

After this restart your mysql server
'''
sudo service mysql restart
'''

Now you can deploy / create the database for your huginn installation. It is possible to fine tune the database using e.g. a script like [MySQLTuner](https://github.com/major/MySQLTuner-perl),  or [MySQL Performance Tuning Primer Script](http://www.day32.com/MySQL/). These scripts will help you determine possible optimizations for your database. **These scripts will read the database usage history and therefor it is best to leave the freshly replaced my.cnf + MyIsam  as is and do the fine tuning after huginn has been running for some time (recommended >= 48 hours)** Mysql tuning should be regularly repeated after a period of time and depending on the amount of Agents and data usage such scripts will keep you updated on possible optimizations. This is a [nice collection](http://helidigizen.com/blog/mysql-server-optimization-blogshot/) of Mysql optimization information

### Optimizing Nginx
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
        #gzip_comp_level 6;
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
```


### Disable OpenSSH Server and enable Dropbear
so far OpenSSH Server is used for deployment but once huginn is running it can be disabled and e.g. Dropbear + openssh-client used as a "lightweight" replacement freeing up to 10MB RAM. If you want to redeploy then you just enable OpenSSH + disable Dropbear temporarily.