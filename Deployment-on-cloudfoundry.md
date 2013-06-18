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
       Installing multi_json (1.7.2)
       Installing activesupport (3.2.13)
       Installing builder (3.0.4)
       Installing activemodel (3.2.13)
       Installing erubis (2.7.0)
       Installing journey (1.0.4)
       Installing rack (1.4.5)
       Installing rack-cache (1.2)
       Installing rack-test (0.6.2)
       Installing hike (1.2.1)
       Installing tilt (1.3.6)
       Installing sprockets (2.2.2)
       Installing actionpack (3.2.13)
       Installing mime-types (1.22)
       Installing polyglot (0.3.3)
       Installing treetop (1.4.12)
       Installing mail (2.5.3)
       Installing actionmailer (3.2.13)
       Installing arel (3.0.2)
       Installing tzinfo (0.3.37)
       Installing activerecord (3.2.13)
       Installing activeresource (3.2.13)
       Installing addressable (2.3.3)
       Installing bcrypt-ruby (3.0.1)
       Installing kaminari (0.14.1)
       Using bundler (1.3.2)
       Installing rack-ssl (1.3.3)
       Installing json (1.7.7)
       Installing rdoc (3.12.2)
       Installing thor (0.18.1)
       Installing railties (3.2.13)
       Installing rails (3.2.13)
       Installing bootstrap-kaminari-views (0.0.2)
       Installing sass (3.2.7)
       Installing bootstrap-sass (2.3.1.0)
       Installing coffee-script-source (1.6.2)
       Installing execjs (1.4.0)
       Installing coffee-script (2.2.0)
       Installing coffee-rails (3.2.2)
       Installing cookiejar (0.3.0)
       Installing daemons (1.1.9)
       Using delayed_job (3.0.4) from https://github.com/wok/delayed_job (at master)
       Installing delayed_job_active_record (0.3.3)
       Installing orm_adapter (0.4.0)
       Installing warden (1.2.1)
       Installing devise (2.2.3)
       Installing eventmachine (1.0.3)
       Installing em-socksify (0.2.1)
       Installing http_parser.rb (0.5.3)
       Installing em-http-request (1.0.3)
       Installing ffi (1.3.1)
       Installing ethon (0.5.10)
       Installing multipart-post (1.2.0)
       Installing faraday (0.8.6)
       Installing sass-rails (3.2.6)
       Installing font-awesome-sass-rails (3.0.2.2)
       Installing foreman (0.62.0)
       Installing geokit (1.6.5)
       Installing geokit-rails3 (0.1.5)
       Installing haml (4.0.2)
       Installing multi_xml (0.5.3)
       Installing httparty (0.10.2)
       Installing jquery-rails (2.2.1)
       Installing jquery-ui-rails (3.0.1)
       Installing jsonpath (0.5.1)
       Installing jwt (0.1.8)
       Installing kramdown (0.14.2)
       Installing mysql2 (0.3.11)
       Installing nested_form (0.3.2)
       Installing nokogiri (1.5.9)
       Installing rack-pjax (0.7.0)
       Installing remotipart (1.0.5)
       Installing safe_yaml (0.9.0)
       Installing rails_admin (0.4.6)
       Installing rufus-scheduler (2.0.18)
       Installing select2-rails (3.3.1)
       Installing simple_oauth (0.1.9)
       Installing twilio-ruby (3.9.0)
       Installing twitter (4.4.0)
       Installing twitter-stream (0.1.16)
       Installing typhoeus (0.6.2)
       Installing uglifier (1.3.0)
       Installing wunderground (1.0.0)
       Your bundle is complete! It was installed into ./vendor/bundle
       Post-install message from rdoc:
       Depending on your version of ruby, you may need to install ruby rdoc/ri data:
       <= 1.8.6 : unsupported
       = 1.8.7 : gem install rdoc-data; rdoc-data --install
       = 1.9.1 : gem install rdoc-data; rdoc-data --install
       >= 1.9.2 : nothing to do! Yay!
       Post-install message from haml:
       HEADS UP! Haml 4.0 has many improvements, but also has changes that may break
       your application:
       * Support for Ruby 1.8.6 dropped
       * Support for Rails 2 dropped
       * Sass filter now always outputs <style> tags
       * Data attributes are now hyphenated, not underscored
       * html2haml utility moved to the html2haml gem
       * Textile and Maruku filters moved to the haml-contrib gem
       For more info see:
       http://rubydoc.info/github/haml/haml/file/CHANGELOG.md
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
