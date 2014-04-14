## Deploying on Openshift

1. Create an account at http://openshift.redhat.com/

1. Create a rails application with a mysql cartridge

    ```
    rhc app create -a huginn -t ruby-1.9 -t mysql-5.1
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

Once it's running, you may want to alter `.env` to include the correct email configuration. You'll need to push that change back up to OpenShift.

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