### WARNING!  This is a work in progress ####

1. You will need an account with a Cloud Foundry v2 provider (eg, www.cloudfoundry.com), and the `cf` command line app correctly configured.

1. Clone the repo - `git clone https://github.com/cloudfoundry-community/cf-demoapp-huginn.git`

1. Change to the root of your working copy
1. Copy `manifest.yml.sample` to `manifest.yml`, then edit change `name:` field
1. Install dependancies - `bundle install`
1. Precompile assets - `rake assets:precompile`
1. Run `cf push` - will give output similar to:

```
[~/Projects/CloudFoundry/cf-demoapp-huginn(master)]$ cf push
Using manifest file manifest.yml

Creating *****-huginn... OK

1: *****-huginn
2: none
Subdomain> *****-huginn

1: cfapps.io
2: none
Domain> cfapps.io

Binding *****-huginn.cfapps.io to *****-huginn... OK
Binding *****-huginn-mysql to *****-huginn... OK
Uploading *****-huginn... OK
Starting *****-huginn... OK
-----> Downloaded app package (2.1M)
Installing ruby.
-----> Using Ruby version: ruby-1.9.2
-----> Installing dependencies using Bundler version 1.3.2
       Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin --deployment
       Fetching gem metadata from https://rubygems.org/.......
       Fetching gem metadata from https://rubygems.org/..
       Fetching https://github.com/wok/delayed_job
       Installing rake (10.0.4)
       Installing i18n (0.6.1)
       ...snip...
       Post-install message from httparty:
       When you HTTParty, you must party hard!
       Cleaning up the bundler cache.
-----> Writing config/database.yml to read from DATABASE_URL
-----> Rails plugin injection
       Injecting rails_log_stdout
       Injecting rails3_serve_static_assets
-----> Uploading staged droplet (51M)
-----> Uploaded droplet
Checking *****-huginn...
Staging in progress...
Staging in progress...
...snip...
Staging in progress...
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  ...snip...
  0/1 instances: 1 starting
  1/1 instances: 1 running
OK
```
1. Hurrah! Browse to http://*****-huginn.cfapps.io

1. TODO: Configure background processes...
