_These instructions describe the behavior of the `deployments` branch at the moment._

Deploying Huginn with Capistrano, Unicorn, and nginx is straight forward.

Follow these steps:

* Edit your Gemfile and add the following:

        group :production do
          gem 'unicorn'
        end
        
        group :development do
          gem 'capistrano'
          gem 'capistrano-unicorn', :require => false
          gem 'rvm-capistrano'
        end

* Setup a place for Huginn to run.  I recommend making a dedicated user on your server for Huginn, but this is not required.  Setup nginx or Apache to proxy pass to unicorn.  There is an example nginx script in `doc/deployment/nginx/production.conf`.
* Setup a production database on your server for Huginn.
* Copy `doc/deployment/unicorn/production.rb` to `config/unicorn/production.rb` and replace instances of *you* with the correct username for your server.
* Copy `doc/deployment/capistrano/deploy.rb` to `config/deploy.rb` and change all instances of `you` and `yourdomain` to the appropriate values for your server setup.  If you want RVM to be used and installed, uncomment the appropriate lines.
* Run `cap deploy:setup` to create the basic Capistrano directory structure on your server.
* Make a copy of your `.env` file, setup your production settings, create a directory called `/home/you/app/shared/config` on your server, and place your production `.env` file in this directory.
* Make a copy of your `Procfile`, set it up for production, and place the copy in `/home/you/app/shared/config` on your server, just like you did with the `.env` file for production.
* Run `cap deploy`.  SSH into your server, go to the deployment directory, and run `bundle exec foreman start` in a screen session.
* Run `RAILS_ENV=production bundle exec rake db:seed` to generate your admin user.  Immediately login to your new Huginn installation with the username of `admin` and the password of `password` and change your email and password!

If you have a better config for production foreman that doesn't use a screen session, please share!  I know upstart is a good option but haven't set it up yet on my box.