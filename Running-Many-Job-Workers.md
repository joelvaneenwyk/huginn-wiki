# The recommended way to run multiple DelayedJob workers is now documented in the [Procfile](https://github.com/cantino/huginn/blob/master/Procfile#L33-L50)

This Page is a **rough** documentation with a focus on parallelized delay_job workers.

## Background

With the default config, only one `delayed_job` worker is running, which limits you to one (virtual) core. If you have a lot of agents that run frequently, or the `delayed_job` worker is too busy, and you have a multi-core or multi-CPU setup, you can parallelize the `delayed_job` workers for more performance.

## Resources

After testing out various combination on how many delayed_jobs to run, @K1773R found a good ratio is 2 delayed_job workers per (virtual) core.

One worker needs around 187-203 MB, which is quite a lot. Don't run so many workers that you need to swap RAM!

## Setting it up

Unfortunately, `foreman` isn't happy with running multiple workers and errors out.

The Procfile I'm using has the following content

    # Procfile for development using the new threaded worker (scheduler, twitter stream and delayed job)
    #web: bundle exec rails server
    #jobs: bundle exec rails runner bin/threaded.rb

    # Possible Profile configuration for production:
    # web: bundle exec unicorn -c config/unicorn/production.rb
    # jobs: bundle exec rails runner bin/threaded.rb

    # Old version with separate processes (use this if you have issues with the threaded version)
    web: bundle exec rails server
    schedule: bundle exec rails runner bin/schedule.rb
    twitter: bundle exec rails runner bin/twitter_stream.rb
    #dj: bundle exec script/delayed_job run

Note that this has commented out the threaded jobs process and enabled the "old version", with only web, schedule, and twitter enabled. (You can disable twitter too if you don't want to use any TwitterStreamAgents.)

Run

    foreman start

Now you have to launch as many workers as you want with

    bundle exec rake jobs:work

That's it, you have are now capable to run multiple agents the same time.

## Scripts/MISC

@K1773R: I created a bash script as I'm too lazy to do this manually, according to the current amount of CPU's. Just a simple script for use in /etc/rc.local which runs huginn inside screen and as another user.

    #!/bin/bash
    cd /home/k1773r/git/huginn

    CORES=`nproc`
    WORKERS=`expr ${CORES} \* 2`

    sudo -u k1773r screen -dmS foreman foreman start

    for i in `seq 1 ${WORKERS}`;
    do
            sudo -u k1773r screen -dmS worker${i} bundle exec rake jobs:work
    done

Beware that not all linux distros have nproc, so you can specify it manually/set it otherwise.
You have to install screen too, but you probably already have it anyway.
