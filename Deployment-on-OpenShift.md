## Deploying on Openshift

1. Create an account at http://openshift.redhat.com/

1. Create a rails application with a mysql cartridge

    ```
    rhc app create -a huginn -t ruby-1.9 -t mysql-5.1
    ```

1. Add the huginn openshift quickstart as your upstream:

    ```
    cd huginn
    git remote add upstream -m openshift git://github.com/cantino/huginn.git
    git pull -s recursive -X theirs upstream master
    ```

1. Push your new code (this will take a very long time)

    ```
    git push
    ```

1. Seed the database (anyone care to figure out why this isn't happening automatically?)

   ```
   rhc ssh huginn
   cd $OPENSHIFT_REPO_DIR
   bundle exec rake db:seed
   exit
   ```

1. Add the Foreman cartridge, so the background processes run properly:

   ```
   rhc cartridge add -a huginn http://cartreflect-claytondev.rhcloud.com/reflect?github=ncdc/openshift-foreman-cartridge 
   ```

1. That's it! Enjoy Huginn!

Once it's running, you will want to create a `.env` to include the correct email configuration. You can use `.env.example.openshift` as a guide. You'll need to push that change back up to OpenShift.

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

## Installing as a scalable app

Installing as scalable will require 2 small gears - one for Ruby + WebProxy and one for MySQL. This works on the free OpenShift account, and the resulting app is noticeably faster (plus you have more storage for your SQL DB). 

Follow the above instructions except for these slight modifications:
* When creating the app, add the -s switch

    ```
    rhc app create -a huginn -t ruby-1.9 -t mysql-5.1 -s
    ```

* When you add the foreman cartridge, use this repo instead as I've modified the manifest to allow it to be installed on scalable apps as a domain scoped plugin.

    ```
    rhc cartridge add -a huginn http://cartreflect-claytondev.rhcloud.com/reflect?github=afro88/openshift-foreman-cartridge 
    ```