**Note: These are simply notes from a successful setup, not exact instructions**

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