Mini-Tutorial for installing huginn on dokku

> A docker-powered PaaS that helps you build and manage the lifecycle of applications http://dokku.viewdocs.io/dokku/

# Prerequisites

- dokku version >= v0.4.9
- http://dokku.viewdocs.io/dokku/getting-started/installation/

# Create the app

Let's assume a dokku installation at "dokku.me". The ssh user is "root".

```
git clone https://github.com/cantino/huginn.git
cd huginn
ssh -t root@dokku.me dokku apps:create huginn
git remote add dokku dokku@dokku.me:huginn
```

# Install and link Postgresql

```
ssh -t root@dokku.me dokku plugin:install https://github.com/dokku/dokku-postgres.git
ssh -t root@dokku.me dokku postgres:create huginn
ssh -t root@dokku.me dokku postgres:link huginn huginn
```

# Environment Variables

- Replace `APP_SECRET_TOKEN=your-secret-token` with something secret and sane.
- `RAILS_SERVE_STATIC_FILES=true` is neccessary so lazy people do not have to create their own nginx configuration.

```
ssh -t root@dokku.me dokku config:set huginn DATABASE_ADAPTER=postgresql
ssh -t root@dokku.me dokku config:set huginn PROCFILE_PATH=deployment/heroku/Procfile.heroku
ssh -t root@dokku.me dokku config:set huginn APP_SECRET_TOKEN=your-secret-token
ssh -t root@dokku.me dokku config:set huginn RAILS_ENV=production
ssh -t root@dokku.me dokku config:set huginn RAILS_SERVE_STATIC_FILES=true
```

# Deploy the app and migrate the database

- After deployment huginn needs some time to "boot". Give it 30 seconds after deployment finishes before filing a complaint.

```
git push dokku master
ssh -t root@dokku.me dokku run huginn bundle exec rake db:migrate
ssh -t root@dokku.me dokku run huginn bundle exec rake db:seed
ssh -t root@dokku.me dokku ps:restart huginn
```
