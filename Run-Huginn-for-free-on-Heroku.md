## You can now run Huginn for free on Heroku

### Instructions

* Install the [Heroku Toolbelt](https://toolbelt.heroku.com/) and then run `heroku login`
* Go into your huginn directory and run the magic setup wizard: `bin/setup_heroku`

### Important things to keep in mind

* Heroku's free plan limits the number of database rows that you can have to 10,000, so you should be sure to set a low event retention schedule for your agents.
* The `setup_heroku` command points Heroku at a special Procfile (`deployment/heroku/Procfile.heroku`) that is designed to be run on only one Heroku web worker.  If you want to run multiple workers, change the Heroku config variable `PROCFILE_PATH` with `heroku config:set PROCFILE_PATH=./Procfile` and switch back to the standard Huginn Procfile configuration.

### Using your own mail server

```bash
# Outgoing email settings.  To use Gmail or Google Apps, put your Google Apps domain or gmail.com
# as the SMTP_DOMAIN and your Gmail username and password as the SMTP_USER_NAME and SMTP_PASSWORD.
heroku config:set SMTP_DOMAIN=your-domain-here.com
heroku config:set SMTP_USER_NAME=you@gmail.com
heroku config:set SMTP_PASSWORD=somepassword
heroku config:set SMTP_SERVER=smtp.gmail.com

# The address from which system emails will appear to be sent.
heroku config:set EMAIL_FROM_ADDRESS=from_address@gmail.com
```

### Example output from `bin/setup_heroku`

```
~/projects/oss/huginn (master)$ bin/setup_heroku 

Welcome andrew@example.com!  It looks like you're logged into Heroku.

It looks like you don't have a Heroku app set up yet for this repo.
You can either exit now and run 'heroku create', or I can do it for you.
Would you like me to create a Heroku app for you now in this repo? (y/n) y
Creating radiant-forest-1519... done, stack is cedar
http://radiant-forest-1519.herokuapp.com/ | git@heroku.com:radiant-forest-1519.git
Git remote heroku added
Your Heroku app name is radiant-forest-1519.  Is this correct? (y/n) y
Setting up APP_SECRET_TOKEN...
Setting config vars and restarting radiant-forest-1519... done, v3
APP_SECRET_TOKEN: 1cde7cd87d40be4f688319e0bcf0a1225ebb4b16b67becbc567f86ef587c032d7bc9e0bfeef4d4b61b8333c45df12ef8afbef97c7a5c592b3ecdbdbd558ba36f
Setting BUILDPACK_URL to https://github.com/ddollar/heroku-buildpack-multi.git
Setting config vars and restarting radiant-forest-1519... done, v4
BUILDPACK_URL: https://github.com/ddollar/heroku-buildpack-multi.git
Setting PROCFILE_PATH to deployment/heroku/Procfile.heroku
Setting config vars and restarting radiant-forest-1519... done, v5
PROCFILE_PATH: deployment/heroku/Procfile.heroku
Setting ON_HEROKU to true
Setting config vars and restarting radiant-forest-1519... done, v6
ON_HEROKU: true
Setting FORCE_SSL to true
Setting config vars and restarting radiant-forest-1519... done, v7
FORCE_SSL: true
Setting DOMAIN to radiant-forest-1519.herokuapp.com
Setting config vars and restarting radiant-forest-1519... done, v8
DOMAIN: radiant-forest-1519.herokuapp.com
You need to set an invitation code for your Huginn instance.  If you plan to share this instance, you will
tell this code to anyone who you'd like to invite.  If you won't share it, then just set this to something
that people will not guess.
What code would you like to use? 
What code would you like to use? something-secret
Setting INVITATION_CODE to something-secret
Setting config vars and restarting radiant-forest-1519... done, v9
INVITATION_CODE: something-secret
Okay, let's setup outgoing email settings.  The simplest solution is to use the free sendgrid Heroku addon.
If you'd like to use your own server, or your Gmail account, please see .env.example and set
SMTP_DOMAIN, SMTP_USER_NAME, SMTP_PASSWORD, and SMTP_SERVER with 'heroku config:set'.
Should I enable the free sendgrid addon? (y/n) y
Adding sendgrid on radiant-forest-1519... done, v10 (free)
Use `heroku addons:docs sendgrid` to view documentation.
Setting config vars and restarting radiant-forest-1519... done, v11
SMTP_SERVER: smtp.sendgrid.net
Setting config vars and restarting radiant-forest-1519... done, v12
SMTP_DOMAIN: heroku.com
Setting config vars and restarting radiant-forest-1519... done, v13
SMTP_USER_NAME: app27830035@heroku.com
Setting config vars and restarting radiant-forest-1519... done, v14
SMTP_PASSWORD: sflajgz0
What email address would you like email to appear to be sent from? andrew@example.com
Setting EMAIL_FROM_ADDRESS to andrew@example.com
Setting config vars and restarting radiant-forest-1519... done, v15
EMAIL_FROM_ADDRESS: andrew@example.com
Should I push your current branch (master) to heroku? (y/n) y
This may take a moment...
Initializing repository, done.

-----> Fetching custom git buildpack... done
-----> Multipack app detected
=====> Downloading Buildpack: https://github.com/cantino/heroku-selectable-procfile.git
=====> Detected Framework: Selectable Procfile
-----> Using deployment/heroku/Procfile.heroku as Procfile
=====> Downloading Buildpack: https://github.com/heroku/heroku-buildpack-ruby.git
=====> Detected Framework: Ruby
-----> Compiling Ruby/Rails
-----> Using Ruby version: ruby-2.0.0
-----> Installing dependencies using 1.6.3
       Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin -j4 --deployment
       Fetching source index from https://rubygems.org/
       Fetching git://github.com/cantino/twitter-stream.git
       Installing i18n 0.6.9
       Installing rake 10.3.2
       Installing minitest 5.3.5
       Installing ace-rails-ap 2.0.1
       Installing builder 3.2.2
       Installing thread_safe 0.3.4
       Installing erubis 2.7.0
       Installing rack 1.5.2
       Installing json 1.8.1
       Installing mime-types 1.25.1
       Installing arel 5.0.1.20140414130214
       Installing polyglot 0.3.5
       Installing extlib 0.9.16
       Installing multi_json 1.10.1
       Using bundler 1.6.3
       Installing addressable 2.3.6
       Installing hike 1.2.3
       Installing thor 0.19.1
       Installing tilt 1.4.1
       Installing buftok 0.2.0
       Installing bcrypt 3.1.7
       Installing simple_oauth 0.2.0
       Installing coffee-script-source 1.7.0
       Installing execjs 2.2.1
       Installing http_parser.rb 0.6.0
       Installing daemons 1.1.9
       Installing cookiejar 0.3.2
       Installing orm_adapter 0.5.0
       Installing dotenv-deployment 0.0.2
       Installing equalizer 0.0.9
       Installing multipart-post 2.0.0
       Installing eventmachine 1.0.3
       Installing hpricot 0.8.6
       Installing simple-rss 1.3.1
       Installing jwt 1.0.0
       Installing hashie 2.0.5
       Installing retriable 1.4.1
       Installing uuidtools 2.1.4
       Installing multi_xml 0.5.5
       Installing kramdown 1.3.3
       Installing libv8 3.16.14.3
       Installing liquid 2.6.1
       Installing systemu 2.6.4
       Installing mini_portile 0.6.0
       Installing mqtt 0.2.0
       Installing kgio 2.9.2
       Installing naught 1.0.0
       Installing mysql2 0.3.16
       Installing rails_serve_static_assets 0.0.2
       Installing rails_stdout_logging 0.0.3
       Installing ffi 1.9.3
       Installing ref 1.0.5
       Installing raindrops 0.13.0
       Installing slack-notifier 0.5.0
       Installing sass 3.2.19
       Installing xmpp4r 0.5.6
       Installing tzinfo 1.2.1
       Installing rack-test 0.6.2
       Installing memoizable 0.4.2
       Installing rest-client 1.6.7
       Installing warden 1.2.3
       Installing geokit 1.8.5
       Installing pg 0.17.1
       Installing treetop 1.4.15
       Installing jsonpath 0.5.6
       Installing launchy 2.4.2
       Installing autoparse 0.3.3
       Installing select2-rails 3.5.7
       Installing coffee-script 2.2.0
       Installing http 0.5.1
       Installing sprockets 2.11.0
       Installing uglifier 2.5.1
       Using cantino-twitter-stream 0.1.15 from git://github.com/cantino/twitter-stream.git (at master)
       Installing dotenv 0.11.1
       Installing faraday 0.9.0
       Installing feed-normalizer 1.5.2
       Installing em-socksify 0.3.0
       Installing macaddr 1.7.1
       Installing httparty 0.13.1
       Installing twilio-ruby 3.11.5
       Installing rails_12factor 0.0.2
       Installing ethon 0.7.1
       Installing unicorn 4.8.3
       Installing activesupport 4.1.4
       Installing rufus-scheduler 3.0.8
       Installing mail 2.5.4
       Installing erector 0.10.0
       Installing foreman 0.63.0
       Installing faraday_middleware 0.9.1
       Installing forecast_io 2.0.0
       Installing signet 0.5.1
       Installing nokogiri 1.6.2.1
       Installing oauth2 0.9.4
       Installing therubyracer 0.12.1
       Installing em-http-request 1.1.2
       Installing uuid 2.3.7
       Installing hipchat 1.2.0
       Installing wunderground 1.2.0
       Installing typhoeus 0.6.9
       Installing twitter 5.8.0
       Installing actionview 4.1.4
       Installing delayed_job 4.0.2
       Installing activemodel 4.1.4
       Installing weibo_2 0.1.6
       Installing ruby-growl 4.1
       Installing rturk 2.12.1
       Installing google-api-client 0.7.1
       Installing protected_attributes 1.0.8
       Installing actionpack 4.1.4
       Installing activerecord 4.1.4
       Installing actionmailer 4.1.4
       Installing kaminari 0.16.1
       Installing delayed_job_active_record 4.0.1
       Installing railties 4.1.4
       Installing sprockets-rails 2.1.3
       Installing coffee-rails 4.0.1
       Installing jquery-rails 3.1.1
       Installing devise 3.2.4
       Installing sass-rails 4.0.3
       Installing rails 4.1.4
       Installing bootstrap-kaminari-views 0.0.3
       Installing geokit-rails 2.0.1
       Your bundle is complete!
       Gems in the groups development and test were not installed.
       It was installed into ./vendor/bundle
       Post-install message from httparty:
       When you HTTParty, you must party hard!
       Post-install message from rufus-scheduler:
       ***
       Thanks for installing rufus-scheduler 3.0.8
       It might not be 100% compatible with rufus-scheduler 2.x.
       If you encounter issues with this new rufus-scheduler, especially
       if your app worked fine with previous versions of it, you can
       A) Forget it and peg your Gemfile to rufus-scheduler 2.0.24
       and / or
       B) Take some time to carefully report the issue at
       https://github.com/jmettraux/rufus-scheduler/issues
       For general help about rufus-scheduler, ask via:
       http://stackoverflow.com/questions/ask?tags=rufus-scheduler+ruby
       Cheers.
       ***
       
       Bundle completed (133.85s)
       Cleaning up the bundler cache.
-----> Preparing app for Rails asset pipeline
       Running: rake assets:precompile
       I, [2014-07-26T20:35:30.763511 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/odin-bd1a6485a1a73b259fabc8b3e49f9eec.jpg
       I, [2014-07-26T20:35:30.765615 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/spinner-arrows-c865833407a393f5300ad9a2bef406d9.gif
       I, [2014-07-26T20:35:41.204940 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/application-125526d5c6270132a1ec04d7bd2b90a8.js
       I, [2014-07-26T20:35:47.006480 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/graphing-eb1ecc32773a2096175d486de7e2c7b1.js
       I, [2014-07-26T20:35:56.539932 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/user_credentials-bb0cf097d9cf37f76d838e5cfb7249bb.js
       I, [2014-07-26T20:36:06.053766 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/application-7bbf63ee3d6dc80d5029e89b0c589029.css
       I, [2014-07-26T20:36:06.060882 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/glyphicons-halflings-regular-e43e2294f5b6b59c08ea467722b8d4e5.eot
       I, [2014-07-26T20:36:06.061456 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/glyphicons-halflings-regular-3a012ef2de81a578809f0f6d2dda3e4c.svg
       I, [2014-07-26T20:36:06.061932 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/glyphicons-halflings-regular-b46bef2dd633192ac2b4e9daf585613e.ttf
       I, [2014-07-26T20:36:06.062407 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/glyphicons-halflings-regular-3a10668bf19bf9f8c45cc2f3ffc8178d.woff
       I, [2014-07-26T20:36:06.065109 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/glyphicons-halflings-white-a830cae6e94f0d807cc3f28922588502.png
       I, [2014-07-26T20:36:06.067204 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/glyphicons-halflings-b2a9763a6eaaaad08bbd8a2b9db5ecb5.png
       I, [2014-07-26T20:36:06.067602 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/json-editor/add-8b77b4a87a6657cf01fab972bb209810.png
       I, [2014-07-26T20:36:06.068011 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/json-editor/delete-eb5f9a29bd90397f203fbeadc2ab46f0.png
       I, [2014-07-26T20:36:06.068380 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/select2-spinner-34f7cb4eea827c53ed3425adf362edf3.gif
       I, [2014-07-26T20:36:06.068774 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/select2-ce34df345845df0c2d1f035091fe184d.png
       I, [2014-07-26T20:36:06.069156 #5939]  INFO -- : Writing /tmp/build_7b0d30bd-3c35-46dc-b73d-b5f05754d340/public/assets/select2x2-ec4bf2b76c97838b357413d72a2f69cf.png
       Asset precompilation completed (42.28s)
       Cleaning assets
       Running: rake assets:clean

Using release configuration from last framework (Ruby).
-----> Discovering process types
       Procfile declares types     -> web
       Default types for Multipack -> console, rake, worker

-----> Compressing... done, 45.1MB
-----> Launching... done, v19
       http://radiant-forest-1519.herokuapp.com/ deployed to Heroku

To git@heroku.com:radiant-forest-1519.git
 * [new branch]      master -> master
Running database migrations...
Running `rake db:migrate` attached to terminal... up, run.3341

[...migrations run...]

I can make an admin user on your new Huginn instance and setup some example Agents.
Should I create a new admin user and some example Agents? (y/n) y
Okay, what is your email address? andrew@example.com
And what username would you like to login as? andrew
Finally, what password would you like to use? 
Just a moment...


Okay, you should be all set!  Visit https://radiant-forest-1519.herokuapp.com and login as 'andrew' with your password.

Done!
```