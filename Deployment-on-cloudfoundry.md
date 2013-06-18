### WARNING!  This is a work in progress ####

1. You will need an account with a Cloud Foundry v2 provider (eg, www.cloudfoundry.com), and the `cf` command line app correctly configured.

1. Clone the repo - `git clone git@github.com:cantino/huginn.git`

1. From the root of your repo working copy, run `cf push`, answering as below

```
~/Projects/huginn(master)]$ cf push
Name> <yourname>-huggin

Instances> 1

1: 64M
2: 128M
3: 256M
4: 512M
5: 1G
6: 2G
Memory Limit> 5   

Creating <yourname>-huggin... OK

1: <yourname>-huggin
2: none
Subdomain> 1                  

1: cfapps.io
2: none
Domain> 1        

Creating route <yourname>-huggin.cfapps.io... OK
Binding <yourname>-huggin.cfapps.io to <yourname>-huggin... OK

Create services for application?> y

1: blazemeter n/a, via blazemeter
2: cleardb n/a, via cleardb
3: cloudamqp n/a, via cloudamqp
4: elephantsql n/a, via elephantsql
5: mongolab n/a, via mongolab
6: rediscloud n/a, via garantiadata
7: treasuredata n/a, via treasuredata
What kind?> 2

Name?> <yourname>-huggin-mysql  

1: spark: Great for getting started and developing your apps
Which plan?> 1

Creating service <yourname>-huggin-mysql... OK
Binding <yourname>-huggin-mysql to <yourname>-huggin... OK
Create another service?> n

Bind other services to application?> n

Save configuration?> y

Saving to manifest.yml... OK
Uploading <yourname>-huggin... OK
Starting <yourname>-huggin... OK
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
-----> Preparing app for Rails asset pipeline
       Running: rake assets:precompile
       rake aborted!
       Can't connect to MySQL server on '127.0.0.1' (111)
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/mysql2-0.3.11/lib/mysql2/client.rb:44:in `connect'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/mysql2-0.3.11/lib/mysql2/client.rb:44:in `initialize'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/mysql2_adapter.rb:16:in `new'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/mysql2_adapter.rb:16:in `mysql2_connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:315:in `new_connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:325:in `checkout_new_connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:247:in `block (2 levels) in checkout'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:242:in `loop'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:242:in `block in checkout'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:239:in `checkout'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:102:in `block in connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:101:in `connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_pool.rb:410:in `retrieve_connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_specification.rb:171:in `retrieve_connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/connection_adapters/abstract/connection_specification.rb:145:in `connection'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/model_schema.rb:308:in `clear_cache!'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activerecord-3.2.13/lib/active_record/railtie.rb:104:in `block (2 levels) in <class:Railtie>'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/callbacks.rb:418:in `_run__3230982122533892411__prepare__3455260160334988728__callbacks'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/callbacks.rb:405:in `__run_callback'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/callbacks.rb:385:in `_run_prepare_callbacks'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/callbacks.rb:81:in `run_callbacks'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/actionpack-3.2.13/lib/action_dispatch/middleware/reloader.rb:74:in `prepare!'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/actionpack-3.2.13/lib/action_dispatch/middleware/reloader.rb:48:in `prepare!'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/application/finisher.rb:47:in `block in <module:Finisher>'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/initializable.rb:30:in `instance_exec'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/initializable.rb:30:in `run'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/initializable.rb:55:in `block in run_initializers'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/initializable.rb:54:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/initializable.rb:54:in `run_initializers'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/application.rb:136:in `initialize!'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/railtie/configurable.rb:30:in `method_missing'
       /tmp/staged/app/config/environment.rb:8:in `<top (required)>'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/dependencies.rb:251:in `require'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/dependencies.rb:251:in `block in require'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/dependencies.rb:236:in `load_dependency'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/activesupport-3.2.13/lib/active_support/dependencies.rb:251:in `require'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/application.rb:103:in `require_environment!'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/railties-3.2.13/lib/rails/application.rb:297:in `block (2 levels) in initialize_tasks'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `call'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `block in execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:184:in `block in invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:177:in `invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:170:in `invoke'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/actionpack-3.2.13/lib/sprockets/assets.rake:93:in `block (2 levels) in <top (required)>'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `call'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `block in execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:184:in `block in invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:177:in `invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:205:in `block in invoke_prerequisites'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:203:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:203:in `invoke_prerequisites'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:183:in `block in invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:177:in `invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:170:in `invoke'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/actionpack-3.2.13/lib/sprockets/assets.rake:60:in `block (3 levels) in <top (required)>'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `call'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `block in execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:184:in `block in invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:177:in `invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:170:in `invoke'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/actionpack-3.2.13/lib/sprockets/assets.rake:23:in `invoke_or_reboot_rake_task'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/actionpack-3.2.13/lib/sprockets/assets.rake:29:in `block (2 levels) in <top (required)>'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `call'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:246:in `block in execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:241:in `execute'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:184:in `block in invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:177:in `invoke_with_call_chain'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/task.rb:170:in `invoke'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:143:in `invoke_task'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:101:in `block (2 levels) in top_level'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:101:in `each'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:101:in `block in top_level'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:110:in `run_with_threads'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:95:in `top_level'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:73:in `block in run'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:160:in `standard_exception_handling'
       /tmp/staged/app/vendor/bundle/ruby/1.9.1/gems/rake-10.0.4/lib/rake/application.rb:70:in `run'
       Tasks: TOP => environment
       (See full trace by running task with --trace)
       Precompiling assets failed, enabling runtime asset compilation
       Injecting rails31_enable_runtime_asset_compilation
       Please see this article for troubleshooting help:
       http://devcenter.heroku.com/articles/rails31_heroku_cedar#troubleshooting
-----> Rails plugin injection
       Injecting rails_log_stdout
       Injecting rails3_serve_static_assets
-----> Uploading staged droplet (51M)
-----> Uploaded droplet
Checking <yourname>-huggin...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
  0/1 instances: 1 starting
Application failed to start.
```

1. Add the huginn openshift quickstart as your upstream:

    ```
    cd huginn
    git remote add upstream -m master git://github.com/ghelleks/huginn.git
    git pull -s recursive -X theirs upstream master
    ```

1. Push your new code

    ```
    git push
    ```

1. That's it! Enjoy Huginn!

You will need to ssh into your gear to run the background processes, of course.

Once it's running, you may want to alter `.env.openshift` to include the correct email configuration. You'll need to push that change back up to OpenShift.

## OpenShift Considerations

These are some special considerations you may need to keep in mind when running your application on OpenShift.

### Database
Your application is configured to use your OpenShift database in Production mode.  Because it addresses these databases based on [OpenShift Environment Variables](http://red.ht/NvNoXC), you will need to change these values in the `.env` file if you want to use your application in Production mode outside of OpenShift.

### Assets

Your application is set to precompile the assets every time you push to OpenShift. Any assets you commit to your repo will be preserved alongside those which are generated during the build.

### Security

Since these quickstarts are shared code, we had to take special consideration to ensure that security related configuration variables was unique across applications. To accomplish this, we modified some of the configuration files (shown in the table below). Now instead of using the same default values, your application will generate it's own value using the `initialize_secret` function from `lib/openshift_secret_generator.rb`.

<table>
  <tr>
    <th>File</th>
    <th>Variable</th>
  </tr>
  <tr>
    <td>config/initializers/secret_token.rb</td> 
    <td>Railsapp::Application.config.secret_token</td>
  </tr>
</table>