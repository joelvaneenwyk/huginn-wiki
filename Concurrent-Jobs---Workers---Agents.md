# Concurrent Jobs / Workers / Agents

This Page is a **rough** documentation with a focus on parallelized delay_job workers.

## Background
With a default config only one delay_job worker is running. If you'r server has multiple CPU sockets/cores/threads your limited to the performance of 1 of (virtual) core.

In case you have a lot of agents that run often or the delay_job workers always has work to do, you have to parallelize the delay_job workers, so multiple agents can run each time.

## Resources
After testing out various combination on how many delay_jobs to run, i found a good ratio is 2 delay_job workers per (virtual) core.

One worker needs around 187-203 MB, which is quite much. Running more workers but needing to swap to HDD/SDD/zRAM isn't a good idea!

## Setting it up
Unfortunately, foreman isn't happy with running multiple workers and errors out.

The Procfile i'm using has the following content
    # Procfile for development using the new threaded worker (scheduler, twitter stream and delayed job)
    #web: bundle exec rails server
    #jobs: bundle exec rails runner bin/threaded.rb
    
    # Possible Profile configuration for production:
    # web: bundle exec unicorn -c config/unicorn/production.rb
    # jobs: bundle exec rails runner bin/threaded.rb
    
    # Old version with separate processes (use this if you have issues with the threaded version)
    web: bundle exec rails server
    schedule: bundle exec rails runner bin/schedule.rb
    #twitter: bundle exec rails runner bin/twitter_stream.rb
    #dj: bundle exec script/delayed_job run

Run
    foreman start
Now you have to launch as many workers as you want with
    bundle exec rake jobs:work

That's it, you have are now capable to run multiple agents the same time.

## Scripts/MISC
I've created a bash script as i'm too lazy to do this manually, according to the current amount of CPU's. Just a simple script for use in /etc/rc.local which runs huginn inside screen and as another user.

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