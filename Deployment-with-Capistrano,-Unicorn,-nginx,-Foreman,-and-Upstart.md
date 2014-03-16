Deploying Huginn with Capistrano, Unicorn, and nginx is straight forward.  You can read more about using Foreman and Upstart together in general [here](http://michaelvanrooijen.com/articles/2011/06/08-managing-and-monitoring-your-ruby-application-with-foreman-and-upstart/).

Follow these steps:

* Edit your Gemfile and add the following:

        group :production do
          gem 'unicorn'
        end
        
        group :development do
          gem 'capistrano'
          gem 'rvm-capistrano'
        end

* Run `bundle` again after you do this to install `capistrano` and `rvm-capistrano`.
* Setup a place for Huginn to run.  I recommend making a dedicated user on your server for Huginn, but this is not required.  Setup nginx or Apache to proxy pass to unicorn.  There is an example nginx script in `doc/deployment/nginx/production.conf`.
* Setup a production database on your server for Huginn.
* Copy `doc/deployment/unicorn/production.rb` to `config/unicorn/production.rb` and replace instances of *you* with the correct username for your server.
* Copy `doc/deployment/capistrano/deploy.rb` to `config/deploy.rb` and change all instances of `you` and `yourdomain` to the appropriate values for your server setup.  If you want RVM to be used and installed, uncomment the appropriate lines.
* Run `cap deploy:setup` to create the basic Capistrano directory structure on your server.
* Make a copy of your `.env` file, setup your production settings, create a directory called `/home/you/app/shared/config` on your server, and place your production `.env` file in this directory.
* Make a copy of your `Procfile`, set it up for production, and place the copy in `/home/you/app/shared/config` on your server, just like you did with the `.env` file for production.
* Run `cap deploy`.  SSH into your server, go to your `deploy_to` directory, and checkout the logs coming from foreman and upstart in `upstart_logs` and `app/current/logs`.  You may wish to setup logrotate, especially for the Twitter agent log.
* Run `RAILS_ENV=production bundle exec rake db:seed` to generate your admin user.  Immediately login to your new Huginn installation with the username of `admin` and the password of `password` and change your email and password!

If you have improvements to this setup, please share!