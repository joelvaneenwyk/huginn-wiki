This is an addendum to the [Novice setup guide][novice-setup-guide] so that you can use [PostgreSQL][postgresql] in place of MySQL.

### Install PostgreSQL ###
This will get you up and going as fast as possible, but in production you shouldn't run your application under the `postgres` user. But out of the box it's the user that can run the create scripts on application launch.

    sudo apt-get install postgresql libpq-dev
    # allow password login
    sudo sh -c 'echo "local all postgres md5" >> /etc/postgresql/9.1/main/pg_hba.conf'
    # by default postgres user doesn't have one.
    sudo -u postgres psql -U postgres -d postgres -c "alter user postgres with password 'yourpassword';"

### Change Compilation Dependencies from MySQL to PostgreSQL ###

Option 1:

In the `Gemfile`, disable `mysql2` and add the `pg` gem.

    #gem 'mysql2'
    gem 'pg'

Option 2:

Set `DATABASE_ADAPTER=postgresql` in your `.env` file, which switches the Gemfile to use `pg`.

### Update Environment with Postgres Connection Info ###

In the `.env`, change the database setup section to the following:

    DATABASE_ADAPTER=postgresql
    DATABASE_ENCODING=utf8
    DATABASE_RECONNECT=true
    DATABASE_NAME=huginn_development
    DATABASE_POOL=5
    DATABASE_USERNAME=postgres
    DATABASE_PASSWORD="yourpassword" 
    DATABASE_HOST="127.0.0.1"
    DATABASE_PORT=5432

### Continue With Install ###
Everything else should continue as normal.

[novice-setup-guide]: https://github.com/cantino/huginn/wiki/Novice-setup-guide
[postgresql]: http://www.postgresql.org/

If you are developing new agent gem, after installation and subsequently when creating a new agent you may get following error:

Agent#8: Exception during check. PG::NotNullViolation: ERROR:  null value in column "id" violates not-null constraint

In this case you need to run following to auto increment id assuming you have no agents in the table:
   CREATE SEQUENCE agents_id_seq OWNED BY agents.id;
   ALTER SEQUENCE agents_id_seq RESTART WITH 1 INCREMENT BY 1;
   ALTER TABLE agents ALTER COLUMN id SET DEFAULT nextval('agents_id_seq');

Similarly you have to run for delayed_jobs, agent_logs and event table.