_These instructions describe the behavior of the `capistrano` branch at the moment._

Deploying Huginn with Capistrano, Unicorn, and nginx is straight forward.

Follow these steps:

* Setup a place for Huginn to run.  I recommend making a dedicated user on your server for Huginn, but this is not required.  Setup nginx or Apache to proxy pass to unicorn.  There is an example nginx script in `doc/deployment/nginx/production.conf`.
* Setup a production database on your server for Huginn.
* Copy `doc/deployment/unicorn/production.rb` to `config/unicorn/production.rb` and replace instances of *you* with the correct username for your server.
* Copy `doc/deployment/capistrano/deploy.rb` to `config/deploy.rb` and change all instances of `you` and `yourdomain` to the appropriate values for your server setup.  If you want RVM to be used and installed, uncomment the appropriate lines.
* Run `cap deploy:setup` to create the basic Capistrano directory structure on your server.
* Make a copy of your `.env` file, setup your production settings, create a directory called `/home/you/app/shared/config` on your server, and place your production `.env` file in this directory.
* Run `cap deploy`.  If everything goes well, some unicorn workers on your server should be started to run the Huginn web app.
* After deploying with capistrano, SSH into your server, go to the deployment directory, and run `RAILS_ENV=production bundle exec rake db:seed` to generate your admin user.  Immediately login to your new Huginn installation with the username of `admin` and the password of `password` and change your email and password!
* You'll need to run `bin/schedule.rb` and `bin/twitter_stream.rb` in a daemonized way.  You can use foreman, screen sessions, or something better.

        RAILS_ENV=production bundle exec rails runner bin/schedule.rb
        RAILS_ENV=production bundle exec rails runner bin/twitter_stream.rb
