## Deploying Huginn on C9 or Cloud 9

1- Create a cloud 9 ( [c9.io](https://c9.io) ) rails workspace and enter the following command one by one:

```

git clone git://github.com/cantino/huginn.git
cd huginn/
cp .env.example .env
bundle
mysql-ctl start
bundle exec rake db:create
bundle exec rake db:migrate
bundle exec rake db:seed

```

> bundle exec rake db:seed <-- cannot download sample.
> NOTE: The example 'SF Weather Agent' will not work until you edit it and put in a free API key from http://www.wunderground.com/weather/api/
> See the Huginn Wiki for more Agent examples! https://github.com/cantino/huginn/wiki

2- finally, you need to change the port number to $PORT and if still not work then change localhost to $IP in the following config file:
.env

3- And kick the app by entering:

```
bundle exec foreman start

```

now we see the login page. Good to go

![loginpage](https://cloud.githubusercontent.com/assets/7134947/14494462/07b2df86-019c-11e6-8bce-f3541920423c.jpg)
