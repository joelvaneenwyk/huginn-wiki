**Note: These are simply notes from a multiple worker per dyno setup on Heroku, not exact instructions**

### Gemfile
    group :production do
      gem 'rack', '> 1.5.0'
      gem 'unicorn', '~> 4.9.0'
      gem 'redis'
      gem 'resque'
      gem 'resque-web', require: 'resque_web'
      gem 'resque-pool'
    end

### WorkerStatusController
Display jobs queue and failed counts on the navigation bar.

Replace this

    # Delayed job
    render json: {
      pending: Delayed::Job.pending.where("run_at <= ?", start).count,
      awaiting_retry: Delayed::Job.awaiting_retry.count,
      recent_failures: Delayed::Job.failed.where('failed_at > ?', 5.days.ago).count,
      event_count: count,
      max_id: max_id || 0,
      events_url: events_url,
      compute_time: Time.now - start
    }

With this

    # Resque
    render json: {
      pending: Resque.size('default'),
      awaiting_retry: 0, # no `Delayed::Job.awaiting_retry.count` equivalent
      recent_failures: Resque::Failure.count,
      event_count: count,
      max_id: max_id || 0,
      events_url: events_url,
      compute_time: Time.now - start
    }


### lib/resque.rake
    require 'resque/tasks' if Rails.env.production?
    require 'resque/pool/tasks' if Rails.env.production?

    # this task will get called before resque:pool:setup
    # and preload the rails environment in the pool manager
    task "resque:setup" => :environment do
      # generic worker setup, e.g. Hoptoad for failed jobs
    end

    task "resque:pool:setup" do
      # close any sockets or files in pool manager
      ActiveRecord::Base.connection.disconnect!
      # and re-open them in the resque worker parent
      Resque::Pool.after_prefork do |job|
        ActiveRecord::Base.establish_connection
      end
    end

### config/resque-pool.yml
    ---
    '*': <%= WORKER_CONCURRENCY %>

### config/routes.rb
Make the top of the routes file look like this:

    require "resque_web" if Rails.env.production?
    Huginn::Application.routes.draw do

      get '/jobs', to: redirect('/resque_web')
      resque_web_constraint = lambda do |request|
        current_user = request.env['warden'].user
        current_user.present?
      end
      constraints resque_web_constraint do
        mount ResqueWeb::Engine => "/resque_web"
      end

      resources :agents do
      ...


### config/initializers/resque.rb
    if Rails.env.production?
      Resque.redis = ENV["REDIS_URL"]
    end

### config/initializers/resque-pool.rb
    WORKER_CONCURRENCY = Integer(ENV["WORKER_CONCURRENCY"] || 2)

### Procfile
    web: bundle exec unicorn -p $PORT -c ./deployment/heroku/unicorn.rb
    schedule: bundle exec rails runner bin/schedule.rb
    twitter: bundle exec rails runner bin/twitter_stream.rb
    resque_pool_01: bundle exec resque-pool
    resque_pool_02: bundle exec resque-pool

