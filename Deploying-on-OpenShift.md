We have ambitions for adding native OpenShift support to huginn, but in the meantime, we can use these instructions.

## Deploying on Openshift ##

First, create a basic Rails app:

   $ rhc app create -a huginn -t ruby-1.9

Then, add a MySQL cartridge:

   $ rhc cartridge add -a huginn -c mysql-5.1

Now, add the openshift branch as your upstream and slurp it down:

   $ git remote add upstream -m openshift git://github.com/ghelleks/huginn.git
   $ git pull -s recursive -X theirs upstream openshift

You may have to merge some things, but hopefully not. Once you're happy, push it up to OpenShift:

   $ git push

Now, grab a snack while all the gems are built.

You will need to ssh into your gear to run the background processes, of course.

## OpenShift Considerations ##
These are some special considerations you may need to keep in mind when
running your application on OpenShift.

### Database ###
Your application is configured to use your OpenShift database in Production mode.
Because it addresses these databases based on [OpenShift Environment
Variables](http://red.ht/NvNoXC), you will need to change these if you
want to use your application in Production mode outside of
OpenShift.

### Assets ###
Your application is set to precompile the assets every time you push to OpenShift. Any assets you commit to your repo will be preserved alongside those which are generated during the build.

### Security ###
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