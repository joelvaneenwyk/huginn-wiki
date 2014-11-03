## Deploying on Openshift

1. Create an account at http://openshift.redhat.com/

1. Install the [rhc](https://developers.openshift.com/en/getting-started-client-tools.html) command line tool (could be as simple as `gem install rhc`) and then run `rhc setup`.

1. Run our OpenShift setup script!

    ```
    bin/setup_openshift
    ```

1. Optionally, setup [Pingdom](http://pingdom.com) to ping your app so that it doesn't spin down and keeps doing background processes.

1. Optionally, setup outbound email.  We suggest using Gmail.  See the 'Outgoing email settings' section in .env.example.  You'll need to set those environment variables in OpenShift using `rhc env set VARIABLE=VALUE`.  Something like:

    ```
    rhc env set SMTP_DOMAIN="gmail.com" SMTP_USER_NAME="johndoe@gmail.com" SMTP_PASSWORD="password" SMTP_SERVER="smtp.gmail.com" SMTP_PORT=587 SMTP_AUTHENTICATION=plain SMTP_ENABLE_STARTTLS_AUTO=true EMAIL_FROM_ADDRESS="johndoe@gmail.com"
    ```