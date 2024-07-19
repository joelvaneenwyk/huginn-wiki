1. You will need an account with a [Cloud Foundry](http://www.cloudfoundry.com) v2 provider (eg, [run.pivotal.io](http://run.pivotal.io), [IBM Bluemix](https://console.ng.bluemix.net/) or [anynines.com](http://anynines.com)), and the `cf` command line app correctly configured.

1. Clone the repo - `git clone https://github.com/cantino/huginn.git`

1. Change to the root of your working copy
1. Copy `manifest.yml.sample` to `manifest.yml`, then edit the `name:` field replacing huginn with a unique name
1. Update `url:` field accordingly to your cloudfoundry provider.
1. Create database service (e.g. mysql) with name `huginn-db`
1. Run `cf push` - this will give output similar to:

```
[~/Projects/CloudFoundry/cf-demoapp-huginn(master)]$ cf push -f manifest.yml
Using manifest file manifest.yml

Updating app huginn in org test@test.com / space dev as test@test.com...
OK

Uploading huginn...
Uploading app files from: .
Uploading 3.3M, 880 files
Done uploading
OK
Binding service huginn-db to app huginn in org test@test.com / space dev as test@test.com...
OK

Stopping app huginn in org test@test.com / space dev as test@test.com...
OK

Starting app huginn in org test@test.com / space dev as test@test.com...
-----> Downloaded app package (4.4M)

...

-----> Preparing app for Rails asset pipeline
       Cleaning assets
       Running: rake assets:clean
###### WARNING:
       You have not declared a Ruby version in your Gemfile.
       ruby '2.0.0'
       # See https://devcenter.heroku.com/articles/ruby-versions for more information.


0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App huginn was started using this command `nohup foreman start --procfile Procfile.CF`

Showing health and status for app huginn in org test@test.com / space dev as test@test.com...
OK

requested state: started
instances: 1/1
usage: 512M x 1 instances
urls: test.mybluemix.net
last uploaded: Sat Mar 21 10:44:26 +0000 2015

     state     since                    cpu    memory           disk
#0   running   2015-03-21 11:46:27 AM   0.2%   375.2M of 512M   240.9M of 1G
```

1. Hurrah! Browse to http://<url> (The default invitation code is: `try-huginn`)

### NOTES:

1.  The initial db:migrate can take a long time, so you might need to use `cf log` to see when the migrate is done, then `cf restart`
